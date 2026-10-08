# KONSEP JARINGAN

## "Tugas 3 - Visualisasi Sinyal Harmonisa & Pengalamatan IP"

**DOSEN:**  
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN:**  
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**  
**2026**

---

## A. Pengalamatan IP

Hitung dan tentukan komponen pengalamatan IP dari daftar IP address berikut:
- IP Network
- IP Gateway
- Host Pertama
- Host Terakhir
- Broadcast

### Tabel Hasil Perhitungan IP Address

| No | IP Address | Kelas | Network Address | Gateway | Host Pertama | Host Terakhir |
| :---: | :--- | :---: | :--- | :--- | :--- | :--- |
| **1** | `21.26.8.5` | A | `21.0.0.0` | `21.0.0.1` | `21.0.0.2` | `21.255.255.254` |
| **2** | `212.6.8.3` | C | `212.6.8.0` | `212.6.8.1` | `212.6.8.2` | `212.6.8.254` |
| **3** | `103.24.56.32` | A | `103.0.0.0` | `103.0.0.1` | `103.0.0.2` | `103.255.255.254` |
| **4** | `1.1.1.1` | A | `1.0.0.0` | `1.0.0.1` | `1.0.0.2` | `1.255.255.254` |
| **5** | `172.31.16.8` | B | `172.31.0.0` | `172.31.0.1` | `172.31.0.2` | `172.31.255.254` |

---

## B. Visualisasi Sinyal Harmonisa ($1, 3, 5, 7, 9, 10$)

### Kode Python Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

t = np.linspace(0, 2 * np.pi, 1000)
harmonisa = [1, 3, 5, 7, 9, 10]
sinyal_gabungan = np.zeros_like(t)

plt.figure(figsize=(10, 6))

for n in harmonisa:
  sinyal = (1 / n) * np.sin(n * t)
  sinyal_gabungan += sinyal
  plt.plot(t, sinyal, label=f'Harmonisa ke-{n}', linestyle='dashed', alpha=0.6)

plt.plot(
    t, sinyal_gabungan, label='Sinyal Gabungan', color='black', linewidth=2.5
)
plt.title('Visualisasi Sinyal dan Harmonisa (1, 3, 5, 7, 9, 10)')
plt.xlabel('Waktu')
plt.ylabel('Amplitudo')
plt.axhline(0, color='gray', linewidth=1)
plt.legend(loc='upper right')
plt.grid(True)
plt.show()
```

---

### Analisis Sinyal

* **Amplitudo vs Frekuensi Berbanding Terbalik:** Semakin tinggi orde harmonisa $n$, frekuensinya makin rapat tetapi amplitudonya $\frac{1}{n}$ makin kecil. Harmonisa ke-1 (dasar) memiliki puncak tertinggi, sedangkan harmonisa ke-10 paling rendah.
* **Pembentukan Sinyal Kotak:** Penjumlahan harmonisa ganjil ($1, 3, 5, 7, 9$) membuat Sinyal Gabungan mulai membentuk pola gelombang kotak dengan sisi yang lebih curam.
* **Efek Riak (*Gibbs Phenomenon*):** Puncak Sinyal Gabungan tidak mendatar melainkan bergelombang karena jumlah harmonisa yang digabungkan masih terbatas.
* **Distorsi Harmonisa Genap:** Kehadiran harmonisa ke-10 (orde genap) memberikan sedikit distorsi asimetris pada riak sinyal gabungan, karena gelombang kotak ideal seharusnya hanya tersusun dari harmonisa ganjil.