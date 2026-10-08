# KONSEP JARINGAN
## "MEKANISME TRACEROUTE & PERAN TTL"

**DOSEN:**  
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN:**  
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**  
**2026**

---

## I. Landasan & Fokus Eksperimen

* Membedah alur identifikasi rute jaringan memakai perintah `tracert`.
* Menganalisis peran parameter Time-to-Live ($TTL$) sebagai penangkal perulangan rute tanpa batas (*infinite routing loop*).
* Mengklasifikasikan respons Internet Control Message Protocol (ICMP) selama proses pemeriksaan jaringan.
* Merekam pergeseran jalur transmisi saat jaringan dialihkan dari jalur utama ke jalur alternatif.

---

## II. Arsitektur Jaringan & Distribusi IP

Sistem dibangun menggunakan topologi segitiga beranggotakan 3 buah Router Cisco dan 2 unit PC.

### Pemetaan Perangkat & Interface:
* **PC0 (`Fa0`):** `192.168.10.10/24` — **Gateway:** `192.168.10.1`
* **PC1 (`Fa0`):** `192.168.20.10/24` — **Gateway:** `192.168.20.1`
* **Router0:** 
  * `Fa0/0`: `192.168.10.1/24`
  * `Gig2/0`: `10.10.20.2/30` (ke Router Atas)
  * `Gig3/0`: `10.10.10.2/30` (ke Router2)
* **Router Atas:** 
  * `Gig2/0`: `10.10.20.1/30` (ke Router0)
  * `Gig3/0`: `10.10.30.1/30` (ke Router2)
* **Router2:** 
  * `Fa0/0`: `192.168.20.1/24`
  * `Gig2/0`: `10.10.30.2/30` (ke Router Atas)
  * `Gig3/0`: `10.10.10.1/30` (ke Router0)

---

## III. Hasil Observasi & Penelusuran Rute

### 1. Lintasan Langsung / Jalur Bawah (3 Hop)

```
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms     0 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.10.1
  3     0 ms     0 ms     0 ms  192.168.20.10

Trace complete.
```

* **Tahap 1:** PC0 memancar paket awal ($TTL = 1$). Router0 memotong nilainya jadi $0$, menggugurkan paket, lalu membalas dengan sinyal ICMP Time Exceeded (Type 11).
* **Tahap 2:** Paket kedua dikirim dengan $TTL = 2$. Paket sukses melewati Router0 (sisa $TTL = 1$) lalu habis di Router2, yang kemudian merespons lewat ICMP Time Exceeded (Type 11).
* **Tahap 3:** Paket ketiga dikirim dengan $TTL = 3$. Paket berhasil menyentuh PC1 sebelum $TTL$ habis, diakhiri balasan ICMP Echo Reply (Type 0) (*Trace complete*).

---

### 2. Lintasan Memutar / Transit Router Atas (4 Hop)

```
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms    16 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.20.1
  3     0 ms     *        0 ms  10.10.30.2
  4     *        0 ms     *     Request timed out.

Trace complete.
```

**Kendala Awal:** Sempat terjadi `Request timed out` pada hop ke-4 akibat adanya bentrok tabel rute (*dual route*) pada jalur balik Router2.

```
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms     0 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.20.1
  3     0 ms     0 ms     0 ms  10.10.30.2
  4     0 ms     0 ms     0 ms  192.168.20.10

Trace complete.
```

**Kondisi Setelah Perbaikan:** Setelah entri rute balik dirapikan, trajektori paket terpetakan secara runtut:
* **Hop 1 (`192.168.10.1`):** Balasan ICMP Type 11 dari Gateway Router0.
* **Hop 2 (`10.10.20.1`):** Balasan ICMP Type 11 dari Router Atas.
* **Hop 3 (`10.10.30.2`):** Balasan ICMP Type 11 dari Router2.
* **Hop 4 (`192.168.20.10`):** Diterima PC1 dengan balasan penutup ICMP Echo Reply (Type 0).

---

## IV. Rangkuman Analisis

* **Mekanisme Inkremental TTL:** `tracert` menaikkan nilai $TTL$ secara bertahap ($1, 2, 3,$ dst.) untuk memancing tiap router transit menghentikan paket dan memicu laporan ICMP.
* **Pola Sinyal Umpan Balik:** Router perantara yang dilewati selalu merespons dengan ICMP Type 11, sedangkan node tujuan akhir membalas dengan ICMP Type 0.
* **Dinamika Pemetaan Rute:** Utilitas ini mampu mendeteksi dan menggambarkan pergeseran alur data secara presisi saat terjadi perubahan jalur pada *static routing*.