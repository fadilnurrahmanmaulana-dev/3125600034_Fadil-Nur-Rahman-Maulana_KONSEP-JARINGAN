<div align="center">

# KONSEP JARINGAN
## Latihan Konsep Dasar Jaringan Komputer

**DOSEN:**
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN:**
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**
**2026**

</div>

---

## Level A: Ingatan dan Pemahaman

**1. Jelaskan pengertian jaringan komputer dengan menyebutkan empat unsur pokoknya.**
Jaringan komputer adalah sekumpulan perangkat otonom yang terhubung melalui media komunikasi untuk bertukar pesan dan berbagi sumber daya. Empat unsur pokoknya meliputi: perangkat otonom (*host/end system*), media komunikasi, protokol pengatur, dan perangkat perantara.

**2. Apa yang dimaksud dengan perangkat otonom dalam definisi jaringan?**
Setiap perangkat yang terhubung (seperti laptop atau server) tetap memiliki fungsi, sistem operasi, dan kendali komputasinya sendiri. Perangkat tidak kehilangan identitasnya dan tidak dikendalikan sepenuhnya secara terpusat seolah-olah menjadi satu mesin tunggal.

**3. Bedakan data, sinyal, dan paket.**
*   **Data:** Representasi informasi (teks, suara, video) di tingkat aplikasi.
*   **Sinyal:** Bentuk fisik (tegangan listrik, cahaya, gelombang radio) yang membawa representasi bit data melalui media transmisi.
*   **Paket:** Unit pecahan data yang telah diberi informasi kendali (alamat asal, tujuan, dan nomor urut) untuk disalurkan melalui *packet switching*.

**4. Jelaskan perbedaan PAN, LAN, MAN, dan WAN tanpa hanya menggunakan ukuran jarak.**
*   **PAN:** Dikelola individu, fokus pada konektivitas perangkat pribadi (Bluetooth, NFC).
*   **LAN:** Dikelola oleh satu entitas/organisasi secara terpadu di dalam satu area administrasi (kampus, rumah).
*   **MAN:** Berskala wilayah kota, sering kali infrastrukturnya dikelola oleh operator penyedia layanan publik.
*   **WAN:** Menghubungkan berbagai jaringan lokal melewati batas wilayah menggunakan infrastruktur operator pihak ketiga.

**5. Apa perbedaan intranet, ekstranet, dan Internet publik?**
*   **Intranet:** Jaringan internal organisasi yang hanya dapat diakses oleh anggota organisasi tersebut.
*   **Ekstranet:** Jaringan internal yang sebagian aksesnya dibuka secara spesifik untuk pihak luar yang tepercaya (mitra, auditor).
*   **Internet Publik:** Keterhubungan jaringan global yang sumber dayanya dapat diakses secara terbuka oleh masyarakat umum.

**6. Mengapa Wi-Fi tidak dapat disamakan dengan Internet?**
Wi-Fi hanyalah teknologi media transmisi pada jaringan lokal (Layer 1 dan 2) sebagai pengganti kabel. Sebuah perangkat bisa terhubung ke Wi-Fi (LAN) untuk berbagi data internal tanpa memiliki rute keluar menuju Internet publik sama sekali.

**7. Jelaskan perbedaan client, server, dan peer.**
*   **Client:** Pihak yang meminta dan mengonsumsi layanan.
*   **Server:** Pihak yang menyediakan layanan dan diakses oleh banyak pihak secara terus-menerus.
*   **Peer:** Pihak yang dapat bertindak sebagai peminta (*client*) sekaligus penyedia (*server*) layanan secara bergantian atau bersamaan dalam satu jaringan.

**8. Apa perbedaan bandwidth, throughput, dan goodput?**
*   **Bandwidth:** Kapasitas maksimal teoretis dari sebuah kanal/tautan (misal: 100 Mbps).
*   **Throughput:** Kecepatan aktual transfer seluruh data yang berhasil dipindahkan, termasuk *overhead* protokol (*header* IP, TCP).
*   **Goodput:** Laju kecepatan aktual muatan data aplikasi murni yang diterima tanpa menghitung *header* protokol dan paket yang dikirim ulang.

**9. Sebutkan empat komponen nodal delay.**
*   *Processing delay* (Waktu pemrosesan di router/switch)
*   *Queuing delay* (Waktu antre sebelum ditransmisikan)
*   *Transmission delay* (Waktu serialisasi/memasukkan bit ke dalam media fisik)
*   *Propagation delay* (Waktu rambat sinyal melalui jarak fisik media)

**10. Mengapa Web tidak sama dengan Internet?**
Internet adalah infrastruktur jaringan global dan protokol komunikasi dasar (TCP/IP). Web (*World Wide Web*) hanyalah salah satu layanan aplikasi (HTTP/HTTPS, HTML) yang berjalan di atas infrastruktur Internet tersebut.

---

## Level B: Penerapan dan Analisis

**1. Sebuah paket berukuran 1.000 byte dikirim melalui tautan 10 Mbps. Hitung transmission delay ideal paket tersebut. Jelaskan komponen delay yang belum tercakup.**
Perhitungan *Transmission Delay*:
Ukuran paket ($L$) = 1.000 byte = 8.000 bit.
Laju transmisi ($R$) = 10 Mbps = 10.000.000 bps.

$$d_{trans} = \frac{L}{R} = \frac{8.000}{10.000.000} = 0,0008 \text{ detik, atau } 0,8 \text{ ms}$$

Komponen yang belum tercakup: *Processing delay* (waktu router memproses paket), *queuing delay* (waktu antrean saat sibuk), dan *propagation delay* (waktu rambat sinyal).

**2. Sebuah kampus memiliki koneksi Internet 2 Gbps, tetapi pengguna di satu lantai hanya memperoleh throughput rendah. Susun sedikitnya lima hipotesis yang tidak langsung menyalahkan koneksi ISP.**
*   Kapasitas *uplink switch* di lantai tersebut menuju *core switch* hanya 100 Mbps (terjadi *bottleneck* lokal).
*   *Access point* Wi-Fi kelebihan beban kapasitas klien (terlalu padat pengguna).
*   Terjadi *looping* pada Layer 2 akibat salah colok kabel di *switch* lantai tersebut, menciptakan badai *broadcast*.
*   Terdapat interferensi sinyal radio yang parah pada saluran Wi-Fi di area tersebut.
*   Salah satu PC terinfeksi *malware* yang menghabiskan bandwidth jaringan lokal secara agregat di latar belakang.

**3. Bandingkan kebutuhan jaringan untuk transfer berkas cadangan dan panggilan video. Metrik apa yang paling penting bagi masing-masing aplikasi?**
*   **Transfer berkas cadangan:** Mengutamakan *throughput* berkapasitas besar dan integritas tinggi. Sangat toleran terhadap latensi atau *delay*, namun tidak menoleransi data yang korup (*loss*).
*   **Video konferensi:** Mengutamakan latensi dan *jitter* yang sangat rendah (waktu nyata). Aplikasi ini sanggup menoleransi sedikit *packet loss* (gambar buram sesaat lebih baik daripada terlambat).

**4. Sebuah organisasi mempunyai dua koneksi Internet dari dua operator. Keduanya melewati tiang dan jalur ducting yang sama. Evaluasi kualitas redundansinya.**
Konfigurasi tersebut memberikan redundansi secara logis (melindungi jaringan dari kegagalan *routing core* ISP tertentu), tetapi gagal memberikan keamanan secara fisik. Jika tiang rubuh atau saluran utilitas ekskavator memotong kabel *ducting*, kedua koneksi akan mati bersamaan (*Single Point of Failure* pada Layer 1).

**5. Jelaskan mengapa penambahan bandwidth tidak selalu mengurangi waktu akses ke server yang sangat jauh.**
Menambah kapasitas bandwidth hanya membantu mengatasi hambatan pada *transmission delay* antrean lokal. Hal ini tidak dapat membengkokkan hukum fisika terkait *propagation delay* (kecepatan perambatan cahaya jarak jauh antarbenua).

**6. Sebuah layanan tersedia 99,9% selama satu tahun. Hitung perkiraan maksimum durasi ketidaktersediaannya. Bandingkan dengan target 99,99%.**
*   $99,9\%$ ketersediaan $= 0,1\%$ *downtime* tahunan $= 0,001 \times 8.760 = 8,76$ jam ketidaktersediaan dalam setahun.
*   $99,99\%$ ketersediaan $= 0,01\%$ *downtime* tahunan $= 0,0001 \times 8.760 = 0,876$ jam (sekitar 52 menit) dalam setahun.

**7. Analisis kelebihan dan kelemahan client-server serta P2P untuk distribusi berkas berukuran besar kepada ribuan pengguna.**
*   **Client-Server:** Menawarkan pengelolaan terpusat, kontrol versi, dan keamanan akses yang konsisten. Kelemahannya, apabila ribuan klien mengunduh secara bersamaan, server pusat akan mengalami *bottleneck* ekstrim.
*   **P2P:** Skalabilitas luar biasa karena setiap klien yang menerima paket data otomatis ikut menjadi pengirim, mereduksi beban server asal. Kelemahannya ada pada keamanan integritas data yang rawan disusupi (*tampering*) dan kinerja yang tidak terprediksi.

**8. Berikan contoh ketika topologi fisik dan topologi logis pada jaringan kampus berbeda.**
Secara fisik, laboratorium kampus mungkin menggunakan topologi Star di mana seluruh komputer dicolokkan menggunakan kabel UTP ke sebuah *switch* fisik yang sama. Secara logis, administrator membaginya menjadi dua VLAN berbeda. PC dari kelompok A tidak bisa berinteraksi di Layer 2 dengan PC kelompok B, seolah-olah mereka ditancapkan ke perangkat *switch* yang berbeda sama sekali.

---

## Level C: Evaluasi dan Sintesis

**1. Rancang klasifikasi kebutuhan jaringan kampus untuk mahasiswa, staf administrasi, tamu, kamera pengawas, dan laboratorium riset. Jelaskan alasan segmentasi dan aturan komunikasi utamanya.**
Rancangan Segmentasi Kampus:
*   **VLAN Mahasiswa:** Memiliki throughput sedang, dengan fitur *AP isolation* agar antar-klien tidak bisa saling berkomunikasi langsung. Akses penuh difokuskan ke Internet publik dan portal akademik.
*   **VLAN Staf:** Memerlukan akses khusus ke basis data operasional internal (intranet). Disaring sangat ketat melalui *firewall*.
*   **VLAN Tamu:** Dibatasi secara bandwidth, menggunakan autentikasi identitas berbatas waktu (*Captive Portal*), dan ditutup total rutenya menuju sistem internal kampus.
*   **VLAN Kamera Pengawas:** Sangat tertutup. Hanya diizinkan berkomunikasi secara lokal menuju server NVR (*Network Video Recorder*) tanpa membutuhkan rute ke Internet.
*   **VLAN Lab Riset:** Terisolasi sepenuhnya dari VLAN operasional utama kampus untuk mencegah eksperimen mahasiswa (seperti konflik DHCP atau simulasi *routing*) mengganggu jaringan staf.

**2. Evaluasi pernyataan: "Jaringan internal tidak memerlukan enkripsi karena sudah dilindungi firewall." Gunakan prinsip kerahasiaan, integritas, dan ketersediaan.**
Pernyataan bahwa jaringan internal tidak memerlukan enkripsi adalah keliru. Pendekatan keamanan modern menggunakan prinsip *Zero Trust*. Ancaman tingkat lanjut justru sering kali merangsek dari dalam jaringan (seperti kredensial pengguna yang disusupi serangan *phishing* atau infeksi *malware* pada perangkat *endpoint*). Enkripsi ujung-ke-ujung (TLS/HTTPS) tetap mutlak diperlukan untuk menjaga aspek kerahasiaan dan integritas data meskipun ketersediaan lalu lintasnya telah diizinkan oleh *firewall*.

**3. Diskusikan mengapa Internet dapat berkembang tanpa otoritas teknis pusat tunggal. Jelaskan manfaat serta risikonya.**
Internet dapat bertumbuh secara organik karena bergantung pada konsensus standar terbuka (RFC) yang dikeluarkan lembaga independen seperti IETF. Manfaatnya adalah inovasi yang tidak dimonopoli korporasi tunggal dan arsitektur yang tahan terhadap hantaman kegagalan global. Risikonya, pembaruan standar teknis (seperti migrasi ke IPv6) berjalan lambat dan tidak terkoordinasi secara absolut karena tidak ada lembaga eksekutif yang bisa "memaksa" kepatuhan operasional seluruh jaringan.

**4. Bandingkan circuit switching dan packet switching untuk layanan suara. Jelaskan mengapa suara modern tetap dapat berjalan pada jaringan paket.**
*Circuit switching* lama mendedikasikan jalur konstan bebas antrean khusus untuk satu panggilan telepon, yang menghadirkan stabilitas absolut namun sangat boros karena kapasitas terbuang saat lawan bicara sedang diam. *Packet switching* mengemas potongan-potongan suara menjadi paket dinamis (VoIP) dan berebut jalur transmisi. Suara tetap bisa mengalir lancar di jaringan packet modern berkat pengaturan *Quality of Service* (QoS) di router dan penahanan paket sesaat di *jitter buffer* aplikasi untuk mengeliminasi variasi kedatangan.

**5. Ambil satu keluhan nyata atau hipotetis berupa "Internet lambat". Susun prosedur pengumpulan bukti, pengujian hipotesis, dan kriteria keberhasilan perbaikannya.**
*   **Tentukan Scope:** Lokalisasi area. Apakah lambat di satu *host*, satu lab, atau satu kampus?
*   **Ping Gateway Lokal:** Lakukan pengujian konektivitas dasar menuju gerbang router ruangan untuk mengisolasi potensi isu di Layer 1/2.
*   **Resolusi DNS:** Tes menggunakan `nslookup` untuk memastikan server nama kampus sanggup merespons secara mulus.
*   **Cek Throughput & Packet Loss Eksternal:** Gunakan `traceroute` (atau MTR) menuju sasaran Internet publik guna mendeteksi *hop* yang menunjukkan akumulasi antrean tertinggi.
*   **Tentukan Kriteria Keberhasilan:** Dianggap selesai apabila rata-rata RTT kembali normal (misal stabil di bawah 50ms secara regional) tanpa *packet loss* yang konsisten.

**6. Kunjungi statistik IPv6 Google atau sumber pengukuran APNIC. Catat tanggal, definisi metrik, populasi yang diukur, dan nilai untuk Indonesia. Jelaskan mengapa angka dari dua sumber dapat berbeda.**
Nilai persentase adopsi sering kali bervariasi bergantung pada metodologi sumber pengambilannya. Statistik Google mengumpulkan data dari sisi server, yakni rasio pengguna harian yang menyentuh layanan infrastruktur Google menggunakan tumpukan protokol IPv6. Sementara APNIC menyebarkan skrip *tracker* pasif melalui jaringan iklan global, memicu peramban klien untuk melakukan resolusi ke IPv6 sebagai bahan eksperimen aktif.

**7. Buat argumen mengenai penggunaan satelit orbit rendah sebagai koneksi utama atau cadangan bagi kampus di wilayah terpencil. Nilai kinerja, biaya, ketergantungan cuaca, pengelolaan, dan keamanan.**
Infrastruktur LEO (seperti Starlink) sangat potensial berkat metrik latensi (RTT) yang kompetitif di kisaran 30-50ms (berbanding >500ms pada satelit GEO), dilengkapi bandwidth gigabit. Biaya instalasi perangkat keras di awal cukup menguras modal, tetapi *overhead* operasional per bulannya kompetitif. Kelemahan teknis terbesarnya adalah kerentanan terhadap redaman curah hujan ekstrem (*rain fade*). Ideal diposisikan sebagai pilar koneksi primer pada daerah nol kabel optik, atau diintegrasikan sebagai SD-WAN sekunder pendamping rute terestrial.

**8. Jelaskan bagaimana otomatisasi jaringan dapat meningkatkan konsistensi sekaligus memperbesar dampak kesalahan. Usulkan kontrol teknis dan proses untuk mengurangi risiko tersebut.**
Otomatisasi menjamin keseragaman penyebaran kebijakan namun secara simultan menyematkan risiko fatal melipatgandakan kesalahan ketik (*typo script*) yang bisa meruntuhkan *routing* ribuan gawai seketika. Guna menjinakkan risiko ini, organisasi wajib memposisikan sistem CI/CD, mengaplikasikan *dry run* sebelum dieksekusi secara nyata, merilis konfigurasi perlahan per segmen jaringan (*canary release*), dan merancang *trigger* otomatis untuk melakukan *auto-rollback* andai alat pengelolaan mendadak kehilangan koneksi akses.

---

## TUGAS KONSEP JARINGAN

1.  Mencatat tentang kabel UTP cat 1 sampai cat 9
2.  Standard wifi yang ada cari tau berapa abgn nya
3.  Mencari detail sejarah dan timeline internet
4.  Menginterpretasikan detail internet yang muncul pada fast.com

### 1. Spesifikasi Kabel Twisted Pair (Cat 1 hingga Cat 9)
Kabel jaringan *twisted pair* berevolusi untuk mendukung kapasitas bandwidth dan frekuensi yang lebih tinggi guna menekan interferensi silang (*crosstalk*). Secara teknis, standar resmi dari TIA/EIA saat ini hanya mencapai Cat 8.

| Kategori | Frekuensi | Kecepatan Maksimal | Penggunaan Utama | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| **Cat 1** | < 1 MHz | < 1 Mbps | Jalur telepon analog | Tidak standar untuk data jaringan komputasi. |
| **Cat 2** | 4 MHz | 4 Mbps | Jaringan Token Ring | Usang. Digunakan pada awal 1980-an. |
| **Cat 3** | 16 MHz | 10 Mbps | 10BASE-T Ethernet | Usang untuk data, masih sering ditemukan untuk sistem telepon PABX. |
| **Cat 4** | 20 MHz | 16 Mbps | Token Ring | Sangat jarang digunakan, digantikan dengan cepat oleh Cat 5. |
| **Cat 5** | 100 MHz | 100 Mbps | 100BASE-TX (Fast Ethernet) | Usang. Kabel data standar pertama untuk jaringan 100 Mbps. |
| **Cat 5e** | 100 MHz | 1 Gbps | 1000BASE-T (Gigabit Ethernet) | Standar minimal jaringan modern saat ini. Pengurangan *crosstalk* signifikan dibanding Cat 5. |
| **Cat 6** | 250 MHz | 10 Gbps (hingga 55m)<br>1 Gbps (hingga 100m) | 10GBASE-T, Jaringan Kampus/Kantor | Memiliki separator plastik di tengah kabel (spline) untuk memisahkan pasangan lilitan. |
| **Cat 6a** | 500 MHz | 10 Gbps (hingga 100m) | 10GBASE-T, Data Center | Huruf "a" berarti *augmented*. Perisai pelindung lebih tebal, kabel lebih kaku. |
| **Cat 7** | 600 MHz | 10 Gbps (hingga 100m) | Infrastruktur Enterprise | Standar ISO/IEC (bukan TIA/EIA). Selalu menggunakan pelindung penuh (S/FTP) pada setiap lilitan dan selimut luar. Menggunakan konektor khusus (GG45/TERA), bukan RJ45 biasa. |
| **Cat 8** | 2000 MHz | 25 Gbps / 40 Gbps (hingga 30m) | Switch-to-Server di Data Center | Diakui oleh TIA/EIA. Didesain khusus untuk jarak pendek berkapasitas sangat masif. |
| **Cat 9** | - | - | - | Belum ada standar resmi ISO/TIA. Saat ini, istilah "Cat 9" sering digunakan sebagai *gimmick* pemasaran oleh vendor kabel atau merujuk pada kabel *heavy-duty* industrial, tetapi bukan standar jaringan komunikasi data yang terverifikasi. |

### 2. Standar Wi-Fi

| Generasi | Standar IEEE | Tahun Rilis | Frekuensi | Kecepatan Teoretis Maksimal | Fitur Utama |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Wi-Fi 1** | 802.11b | 1999 | 2.4 GHz | 11 Mbps | Standar komersial pertama yang diadopsi secara luas. Rentan interferensi microwave/Bluetooth. |
| **Wi-Fi 2** | 802.11a | 1999 | 5 GHz | 54 Mbps | Dirilis bersamaan dengan "b", tetapi beroperasi di frekuensi 5 GHz yang lebih bersih namun jarak jangkauannya lebih pendek. |
| **Wi-Fi 3** | 802.11g | 2003 | 2.4 GHz | 54 Mbps | Menggabungkan jangkauan 2.4 GHz dengan kecepatan 54 Mbps menggunakan modulasi OFDM. |
| **Wi-Fi 4** | 802.11n | 2009 | 2.4 GHz & 5 GHz | 600 Mbps | Memperkenalkan teknologi MIMO (*Multiple Input Multiple Output*) menggunakan lebih dari satu antena. |
| **Wi-Fi 5** | 802.11ac | 2014 | 5 GHz | 3.5 Gbps | Memperkenalkan *Beamforming* dan MU-MIMO (pengiriman data ke beberapa klien sekaligus secara *downlink*). |
| **Wi-Fi 6** | 802.11ax | 2019 | 2.4 GHz & 5 GHz | 9.6 Gbps | Memperkenalkan OFDMA untuk mengurangi latensi pada jaringan yang sangat padat perangkat. |
| **Wi-Fi 6E**| 802.11ax | 2021 | 6 GHz | 9.6 Gbps | Perluasan Wi-Fi 6 ke pita frekuensi 6 GHz yang sepenuhnya kosong dari perangkat jaringan lama. |
| **Wi-Fi 7** | 802.11be | 2024 | 2.4, 5, & 6 GHz | 46 Gbps | Mampu menggunakan beberapa frekuensi sekaligus untuk satu perangkat (*Multi-Link Operation* / MLO). |
| **Wi-Fi 8** | 802.11bn | 2028 *(Estimasi Ratifikasi Standar)* | 2.4, 5, & 6 GHz | ~46 Gbps | Secara resmi ditunjuk sebagai standar *Ultra High Reliability* (UHR). Kecepatan teoretisnya sengaja dipertahankan sama persis dengan Wi-Fi 7. Fokus utamanya bergeser pada keandalan dan stabilitas koneksi, bukan sekadar angka kecepatan maksimal. Wi-Fi 8 memperkenalkan fitur inovatif *Multi-AP Coordination (Coordinated Spatial Reuse, Coordinated Beamforming*, dan *Coordinated OFDMA)* agar titik akses yang berdekatan saling bekerja sama mengelola sinyal alih-alih saling mengganggu. Pembaruan ini menargetkan penurunan latensi drastis untuk skenario *real-time* dan transisi perpindahan (*roaming*) yang sangat mulus antar-ruangan. |

### 3. Sejarah dan Timeline Internet
Internet berawal dari proyek jaringan militer dan riset akademis yang dirancang untuk memiliki ketahanan tinggi tanpa pusat kendali (*decentralized*).

*   **1969 - Lahirnya ARPANET:** Departemen Pertahanan AS mendanai ARPANET. Empat *node* komputer pertama terhubung (UCLA, Stanford, UC Santa Barbara, dan University of Utah). Pesan pertama yang dikirim adalah "LO", niatnya mengetik "LOGIN" tetapi sistem *crash*.
*   **1971 - Penemuan Email:** Ray Tomlinson mengembangkan program untuk mengirim pesan antar komputer di ARPANET dan memilih simbol `@` untuk memisahkan nama pengguna dari nama komputer.
*   **1974 - Konsep TCP/IP:** Vint Cerf dan Bob Kahn menerbitkan desain *Transmission Control Protocol* (TCP), yang mendefinisikan bagaimana paket data dikirim, dirutekan, dan disusun kembali secara terstandardisasi melintasi jaringan yang berbeda.
*   **1 Januari 1983 - Hari Lahir Internet Modern:** ARPANET secara resmi bermigrasi dari protokol NCP lama ke protokol TCP/IP. Semua jaringan riset kini berbicara dengan "bahasa" yang sama.
*   **1984 - Pengenalan DNS:** *Domain Name System* (DNS) diciptakan untuk menerjemahkan alamat IP numerik (seperti `192.168.1.1`) menjadi nama yang mudah diingat (seperti `pens.ac.id`).
*   **1989-1990 - Penemuan World Wide Web:** Tim Berners-Lee di lembaga riset CERN menciptakan World Wide Web (WWW), HTML, HTTP, dan web *browser* pertama, menjadikan informasi mudah diakses secara visual.
*   **1993 - Peramban Mosaic:** Rilis peramban web grafis pertama yang populer, membawa internet keluar dari ranah akademis dan militer menuju masyarakat umum.
*   **1998 - Komersialisasi & ICANN:** Google didirikan. ICANN (*Internet Corporation for Assigned Names and Numbers*) dibentuk untuk mengatur tata kelola penamaan domain dan IP global.
*   **2004-2006 - Era Web 2.0:** Lahirnya Facebook, YouTube, dan Twitter. Internet bergeser dari halaman baca-saja (*read-only*) menjadi partisipasi interaktif pengguna (media sosial).
*   **2007 - Era Mobile Internet:** Peluncuran iPhone memicu lonjakan masif penggunaan internet nirkabel (3G/4G).
*   **2012 - Peluncuran IPv6:** IP versi 4 mulai kehabisan alamat. IPv6 diluncurkan secara global untuk menyediakan triliunan alamat IP baru untuk mengakomodasi tren *Internet of Things* (IoT).

### 4. Interpretasi Metrik Jaringan pada Fast.com
Fast.com adalah alat ukur jaringan berbasis web milik Netflix yang berjalan langsung di atas server pengiriman konten (CDN) Netflix. Ketika tombol "Show more info" diklik, fast.com menyajikan beberapa metrik analitik mendalam:

1.  **Kecepatan Unduh (Download Speed)**
    *   **Metrik:** Megabit per detik (Mbps).
    *   **Interpretasi:** Seberapa besar kapasitas data yang dapat ditarik perangkat dari server dalam satu detik. Nilai ini sangat memengaruhi kualitas streaming video. Netflix merekomendasikan minimal 5 Mbps untuk HD (1080p) dan 15 Mbps untuk 4K.
2.  **Kecepatan Unggah (Upload Speed)**
    *   **Metrik:** Megabit per detik (Mbps).
    *   **Interpretasi:** Kapasitas data yang dapat dikirim dari perangkat menuju server. Penting untuk aplikasi seperti Zoom, unggah video, dan *live streaming*. Umumnya pada koneksi rumahan (Indihome/Biznet), kecepatan unggah lebih kecil dari unduh (asimetris).
3.  **Latensi (Unloaded Latency / Ping Tanpa Beban)**
    *   **Metrik:** Milidetik (ms).
    *   **Interpretasi:** Waktu yang dibutuhkan satu paket data untuk pergi dari perangkat ke server dan kembali lagi saat jaringan sedang sepi/tidak dipakai. Menandakan jarak geografis dan kualitas rute dasar kabel ISP. Angka di bawah 20 ms dianggap sangat baik.
4.  **Latensi (Loaded Latency / Ping Berbeban)**
    *   **Metrik:** Milidetik (ms).
    *   **Interpretasi:** Waktu respons (ping) ketika jaringan sedang ditekan secara maksimal oleh aktivitas unduh/unggah berat. Metrik ini mengukur fenomena *Bufferbloat*. Jika nilai Unloaded 20 ms tetapi nilai Loaded melonjak hingga 400 ms, artinya router kewalahan mengatur antrean paket (*buffer* terlalu penuh). Pengguna akan merasakan game *online* tiba-tiba *lag* parah ketika ada anggota keluarga lain yang sedang mengunduh fail besar.
5.  **Informasi Client & Server**
    *   **Client:** Menampilkan alamat IP publik, lokasi kota, dan nama ISP yang sedang digunakan.
    *   **Server:** Menunjukkan lokasi server fisik (CDN Netflix) terdekat tempat pengujian dilakukan, memastikan pengukuran tidak bias karena jarak geografis yang terlalu jauh.

---

**Interpretasi Hasil Screenshot Fast.com (Halaman Terakhir PDF):**

> **Hasil:** Kecepatan Unduh: 1.4 Mbps | Kecepatan Unggah: 2.5 Mbps | Latensi Unloaded: 21 ms | Latensi Loaded: 398 ms

Berikut adalah interpretasi detail dari hasil tersebut:
*   **Kecepatan Unduh (Download Speed) - 1.4 Mbps:** Kapasitas tarikan data ini tergolong sangat rendah untuk standar saat ini. Kecepatan ini hanya cukup untuk *browsing* teks ringan atau membalas pesan obrolan. Jika digunakan untuk streaming video, resolusi akan turun drastis ke kualitas SD (misalnya 360p atau 480p) dan rentan mengalami *buffering*.
*   **Kecepatan Unggah (Upload Speed) - 2.5 Mbps:** Menariknya, pada pengujian ini kecepatan unggah lebih tinggi daripada unduh. Meskipun masih tergolong lambat, 2.5 Mbps sudah memenuhi batas minimal untuk melakukan panggilan video standar (seperti Zoom atau Google Meet), mengirim dokumen, atau mengunggah foto berukuran sedang tanpa waktu tunggu yang terlalu lama.
*   **Latensi Tanpa Beban (Unloaded Latency) - 21 ms:** Angka 21 ms menunjukkan kualitas rute dasar yang sangat baik dan sehat. Saat jaringan sedang tidak dipakai oleh siapa pun, paket data hanya membutuhkan waktu 21 milidetik untuk bolak-balik dari perangkat Anda (melalui ISP Telkom) menuju server terdekat.
*   **Latensi Berbeban (Loaded Latency) - 398 ms:** Terdapat lonjakan drastis dari 21 ms menjadi 398 ms. Ini adalah indikator kuat terjadinya masalah *Bufferbloat*. Saat jaringan digunakan secara maksimal (dalam hal ini menarik bandwidth penuh yang hanya 1.4 Mbps), *buffer* atau antrean paket di dalam modem/router Anda menjadi sangat penuh. Akibatnya, jika Anda mencoba bermain game online atau melakukan *video call* tepat saat pengujian ini berlangsung (atau saat ada orang lain yang sedang mengunduh file), koneksi Anda akan terasa sangat *lag* atau patah-patah.