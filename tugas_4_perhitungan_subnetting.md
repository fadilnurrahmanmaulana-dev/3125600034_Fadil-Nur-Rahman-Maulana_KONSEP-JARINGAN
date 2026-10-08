# KONSEP JARINGAN

## "Tugas 4 - Perhitungan Subnetting"

**DOSEN:**
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN:**
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**
**2026**

---

## 1. SOAL I: Subnetting IP `192.168.1.0/24` ke dalam 4 Subnet

### A. Analisis dan Analisa Perhitungan

1. **Penentuan Bit Subnet ($n$):**
   * Target kebutuhan: $4$ subnet.
   * Rumus: $2^n \ge 4 \Rightarrow n = 2$ bit.

2. **Subnet Mask & CIDR Baru:**
   * Prefix awal: `/24`
   * Prefix baru: $24 + 2 = /26$
   * Desimal Subnet Mask: `255.255.255.192`

3. **Ukuran Blok Subnet (Interval):**
   * Nilai interval = $256 - 192 = 64$

4. **Jumlah Host Valid Per Subnet:**
   * Alokasi host = $2^{(32-26)} - 2 = 2^6 - 2 = 62$ IP usable.

---

### B. Tabel Distribusi Pengalamatan IP

| No. Subnet | Alamat Network (CIDR) | Rentang IP Host Valid | Alamat Broadcast |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `192.168.1.0/26` | `192.168.1.1` – `192.168.1.62` | `192.168.1.63` |
| **Subnet 2** | `192.168.1.64/26` | `192.168.1.65` – `192.168.1.126` | `192.168.1.127` |
| **Subnet 3** | `192.168.1.128/26` | `192.168.1.129` – `192.168.1.190` | `192.168.1.191` |
| **Subnet 4** | `192.168.1.192/26` | `192.168.1.193` – `192.168.1.254` | `192.168.1.255` |

---

### C. Visualisasi Topologi & Uji Konektivitas (Cisco Packet Tracer)

**Pengujian Ping:**

```text
C:\>ping 192.168.1.62

Pinging 192.168.1.62 with 32 bytes of data:
Request timed out.
Reply from 192.168.1.62: bytes=32 time<1ms TTL=127
Reply from 192.168.1.62: bytes=32 time<1ms TTL=127
Reply from 192.168.1.62: bytes=32 time=21ms TTL=127

Ping statistics for 192.168.1.62:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 21ms, Average = 7ms
```

---

## 2. SOAL II: Pembagian IP `132.10.0.0/16` menjadi 10 Segmen Jaringan

### A. Analisis dan Analisa Perhitungan

1. **Penentuan Bit Subnet ($n$):**
   * Target kebutuhan: $10$ segmen jaringan.
   * Rumus: $2^n \ge 10 \Rightarrow n = 4$ bit (menyediakan kapasitas hingga $2^4 = 16$ subnet).

2. **Subnet Mask & CIDR Baru:**
   * Prefix awal: `/16`
   * Prefix baru: $16 + 4 = /20$
   * Desimal Subnet Mask: `255.255.240.0`

3. **Ukuran Blok Subnet (Oktet Ke-3):**
   * Nilai interval = $256 - 240 = 16$

4. **Jumlah Host Valid Per Subnet:**
   * Alokasi host = $2^{(32-20)} - 2 = 2^{12} - 2 = 4.094$ IP usable.

---

### B. Tabel Distribusi Pengalamatan IP

| Segmen | Network ID | Rentang IP Host Valid | Broadcast IP |
| :--- | :--- | :--- | :--- |
| **Segmen 1** | `132.10.0.0/20` | `132.10.0.1` – `132.10.15.254` | `132.10.15.255` |
| **Segmen 2** | `132.10.16.0/20` | `132.10.16.1` – `132.10.31.254` | `132.10.31.255` |
| **Segmen 3** | `132.10.32.0/20` | `132.10.32.1` – `132.10.47.254` | `132.10.47.255` |
| **Segmen 4** | `132.10.48.0/20` | `132.10.48.1` – `132.10.63.254` | `132.10.63.255` |
| **Segmen 5** | `132.10.64.0/20` | `132.10.64.1` – `132.10.79.254` | `132.10.79.255` |
| **Segmen 6** | `132.10.80.0/20` | `132.10.80.1` – `132.10.95.254` | `132.10.95.255` |
| **Segmen 7** | `132.10.96.0/20` | `132.10.96.1` – `132.10.111.254` | `132.10.111.255` |
| **Segmen 8** | `132.10.112.0/20` | `132.10.112.1` – `132.10.127.254` | `132.10.127.255` |
| **Segmen 9** | `132.10.128.0/20` | `132.10.128.1` – `132.10.143.254` | `132.10.143.255` |
| **Segmen 10** | `132.10.144.0/20` | `132.10.144.1` – `132.10.159.254` | `132.10.159.255` |

---

### C. Visualisasi Topologi & Uji Konektivitas (Cisco Packet Tracer)

**Pengujian Ping:**

```text
C:\>ping 132.10.144.10

Pinging 132.10.144.10 with 32 bytes of data:
Request timed out.
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127

Ping statistics for 132.10.144.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

---

## 3. SOAL III: Subnetting IP Kelas A `17.8.0.0/16` menjadi 4 Subnet

### A. Analisis dan Analisa Perhitungan

1. **Penentuan Bit Subnet ($n$):**
   * Target kebutuhan: $4$ subnet.
   * Rumus: $2^n \ge 4 \Rightarrow n = 2$ bit dipinjam.

2. **Subnet Mask & CIDR Baru:**
   * Prefix awal: `/16`
   * Prefix baru: $16 + 2 = /18$
   * Desimal Subnet Mask: `255.255.192.0`

3. **Ukuran Blok Subnet (Oktet Ke-3):**
   * Nilai interval = $256 - 192 = 64$

4. **Jumlah Host Valid Per Subnet:**
   * Alokasi host = $2^{(32-18)} - 2 = 2^{14} - 2 = 16.382$ IP usable.

---

### B. Tabel Distribusi Pengalamatan IP

| Subnet | IP Network / Prefix | IP Host Valid Range | IP Broadcast |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `17.8.0.0/18` | `17.8.0.1` – `17.8.63.254` | `17.8.63.255` |
| **Subnet 2** | `17.8.64.0/18` | `17.8.64.1` – `17.8.127.254` | `17.8.127.255` |
| **Subnet 3** | `17.8.128.0/18` | `17.8.128.1` – `17.8.191.254` | `17.8.191.255` |
| **Subnet 4** | `17.8.192.0/18` | `17.8.192.1` – `17.8.255.254` | `17.8.255.255` |

---

### C. Visualisasi Topologi & Uji Konektivitas (Cisco Packet Tracer)

**Pengujian Ping:**

```text
C:\>ping 17.8.0.10

Pinging 17.8.0.10 with 32 bytes of data:
Request timed out.
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127

Ping statistics for 17.8.0.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

---

## 4. SOAL IV: Subnetting IP Kelas A `8.32.0.0/12` menjadi 6 Subnet

### A. Analisis dan Analisa Perhitungan

1. **Penentuan Bit Subnet ($n$):**
   * Target kebutuhan: $6$ subnet.
   * Rumus: $2^n \ge 6 \Rightarrow n = 3$ bit (menyediakan kapasitas hingga $2^3 = 8$ subnet).

2. **Subnet Mask & CIDR Baru:**
   * Prefix awal: `/12`
   * Prefix baru: $12 + 3 = /15$
   * Desimal Subnet Mask: `255.254.0.0`

3. **Ukuran Blok Subnet (Oktet Ke-2):**
   * Nilai interval = $256 - 254 = 2$

4. **Jumlah Host Valid Per Subnet:**
   * Alokasi host = $2^{(32-15)} - 2 = 2^{17} - 2 = 131.070$ IP usable.

---

### B. Tabel Distribusi Pengalamatan IP

| Subnet | Alamat Jaringan (Network) | Rentang IP Host Yang Dapat Dipakai | Alamat Broadcast |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `8.32.0.0/15` | `8.32.0.1` – `8.33.255.254` | `8.33.255.255` |
| **Subnet 2** | `8.34.0.0/15` | `8.34.0.1` – `8.35.255.254` | `8.35.255.255` |
| **Subnet 3** | `8.36.0.0/15` | `8.36.0.1` – `8.37.255.254` | `8.37.255.255` |
| **Subnet 4** | `8.38.0.0/15` | `8.38.0.1` – `8.39.255.254` | `8.39.255.255` |
| **Subnet 5** | `8.40.0.0/15` | `8.40.0.1` – `8.41.255.254` | `8.41.255.255` |
| **Subnet 6** | `8.42.0.0/15` | `8.42.0.1` – `8.43.255.254` | `8.43.255.255` |

---

### C. Visualisasi Topologi & Uji Konektivitas (Cisco Packet Tracer)

**Pengujian Ping:**

```text
C:\>ping 8.32.0.10

Pinging 8.32.0.10 with 32 bytes of data:
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127

Ping statistics for 8.32.0.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```