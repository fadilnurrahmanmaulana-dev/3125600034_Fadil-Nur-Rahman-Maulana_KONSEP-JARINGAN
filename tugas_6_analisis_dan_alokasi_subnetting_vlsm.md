# KONSEP JARINGAN

## "TUGAS 6: ANALISIS DAN ALOKASI SUBNETTING VLSM"

**DOSEN:**  
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN:**  
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**  
**2026**

---

## DESKRIPSI KASUS & SPESIFIKASI JARINGAN KAMPUS

Sebuah institusi kampus merancang ulang infrastruktur jaringan lokal pada gedung utama menggunakan alokasi IP induk `10.252.108.0/24` dengan total ruang 256 alamat IP. Pembagian alokasi alamat menggunakan metode *Variable Length Subnet Mask* (VLSM) untuk menyesuaikan kapasitas setiap unit kerja dan mencegah pemborosan IP Address.

### Identifikasi Segmen & Kebutuhan Operasional:

* **Laboratorium A:** Melayani kegiatan praktikum komputasi skala besar dengan kebutuhan **90 unit host**.
* **Laboratorium B:** Melayani praktikum pendukung dan kegiatan riset dengan kebutuhan **60 unit host**.
* **Ruang Administrasi:** Melayani operasional tata usaha, layanan mahasiswa, dan kerja staf/dosen dengan kebutuhan **14 unit host**.
* **Tautan Point-to-Point (P2P):** Jalur komunikasi khusus antar-router/switch utama kampus dengan kebutuhan **4 endpoint**.

---

## RINCIAN PARAMETER DAN PERHITUNGAN SUBNETTING (VLSM)

### 1. Segmen Laboratorium A (Kebutuhan: 90 Host)

* **IP Network:** `10.252.108.0`
* **Subnet Mask (Prefix Baru):** `255.255.255.128` (`/25`)
* **Host Pertama (First Usable):** `10.252.108.1`
* **Host Terakhir (Last Usable):** `10.252.108.126`
* **Broadcast Address:** `10.252.108.127`
* **Jumlah Host Tersedia:** 126 Alamat IP Valid
* **Rentang Host Terpakai:** `10.252.108.1` – `10.252.108.90`

---

### 2. Segmen Laboratorium B (Kebutuhan: 60 Host)

* **IP Network:** `10.252.108.128`
* **Subnet Mask (Prefix Baru):** `255.255.255.192` (`/26`)
* **Host Pertama (First Usable):** `10.252.108.129`
* **Host Terakhir (Last Usable):** `10.252.108.190`
* **Broadcast Address:** `10.252.108.191`
* **Jumlah Host Tersedia:** 62 Alamat IP Valid
* **Rentang Host Terpakai:** `10.252.108.129` – `10.252.108.189`

---

### 3. Segmen Administrasi (Kebutuhan: 14 Host)

* **IP Network:** `10.252.108.192`
* **Subnet Mask (Prefix Baru):** `255.255.255.240` (`/28`)
* **Host Pertama (First Usable):** `10.252.108.193`
* **Host Terakhir (Last Usable):** `10.252.108.206`
* **Broadcast Address:** `10.252.108.207`
* **Jumlah Host Tersedia:** 14 Alamat IP Valid
* **Rentang Host Terpakai:** `10.252.108.193` – `10.252.108.206`

---

### 4. Tautan Point-to-Point (Kebutuhan: 4 Endpoint)

* **IP Network:** `10.252.108.208`
* **Subnet Mask (Prefix Baru):** `255.255.255.248` (`/29`)
* **Host Pertama (First Usable):** `10.252.108.209`
* **Host Terakhir (Last Usable):** `10.252.108.214`
* **Broadcast Address:** `10.252.108.215`
* **Jumlah Host Tersedia:** 6 Alamat IP Valid
* **Rentang Host Terpakai:** `10.252.108.209` – `10.252.108.212`

---

## TABEL REKAPITULASI MATRIKS ALOKASI IP

| Segmen | IP Network | Subnet Mask (Prefix) | Rentang IP Valid (Usable Host) | IP Broadcast | Total Valid | Host Terpakai |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Lab A (90)** | `10.252.108.0` | `255.255.255.128` (`/25`) | `10.252.108.1` - `10.252.108.126` | `10.252.108.127` | 126 | `10.252.108.1-90` |
| **Lab B (60)** | `10.252.108.128` | `255.255.255.192` (`/26`) | `10.252.108.129` - `10.252.108.190` | `10.252.108.191` | 62 | `10.252.108.129-189` |
| **Admin (14)** | `10.252.108.192` | `255.255.255.240` (`/28`) | `10.252.108.193` - `10.252.108.206` | `10.252.108.207` | 14 | `10.252.108.193-206` |
| **P2P (4)** | `10.252.108.208` | `255.255.255.248` (`/29`) | `10.252.108.209` - `10.252.108.214` | `10.252.108.215` | 6 | `10.252.108.209-212` |

---

## SISA ALOKASI IP (UNALLOCATED SPACE)

* **Rentang IP Cadangan:** `10.252.108.216` – `10.252.108.255`
* **Sisa Kapasitas:** 40 Alamat IP
* **Perencanaan Kedepan:** Blok IP cadangan ini dapat diproyeksikan untuk pengembangan jaringan Wi-Fi laboratorium atau penambahan segmen server tanpa merusak struktur pengalamatan yang ada.