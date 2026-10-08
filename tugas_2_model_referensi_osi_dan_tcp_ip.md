<div align="center">

# KONSEP JARINGAN
## "Tugas 2 — Model Referensi OSI dan TCP/IP"

**DOSEN :**
Dr. Ferry Astika Saputra, ST, M.Sc. (197708232001121002)

**PENYUSUN :**
Fadil Nur Rahman Maulana (3125600034)

**PROGRAM STUDI SARJANA TERAPAN TEKNIK INFORMATIKA**
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**
**2026**

</div>

---

## Level A — Ingatan dan Pemahaman

**1. Jelaskan alasan komunikasi jaringan disusun berlapis.**
Pendekatan berlapis membagi proses komunikasi yang sangat kompleks menjadi modul-modul yang lebih kecil dengan tanggung jawab spesifik. Hal ini memberikan manfaat berupa modularitas, interoperabilitas (perangkat beda vendor dapat berkomunikasi), kemudahan evolusi (satu teknologi bisa diganti tanpa merombak seluruh sistem), mempermudah diagnosis gangguan, dan memungkinkan penggunaan kembali protokol secara efisien.

**2. Bedakan layanan, antarmuka, dan protokol.**
*   **Layanan:** Kemampuan atau hasil yang disediakan oleh sebuah lapisan kepada lapisan tepat di atasnya (berfokus pada *apa* yang diberikan).
*   **Antarmuka:** Cara/mekanisme agar lapisan di atas dapat mengakses layanan lapisan di bawahnya pada sistem yang sama (misalnya *socket API*).
*   **Protokol:** Aturan dan format komunikasi logis antara entitas sejawat (*peer*) pada lapisan yang sama di dua sistem yang berbeda.

**3. Sebutkan tujuh lapisan OSI dari bawah ke atas beserta fungsi utamanya.**
*   **Physical (Fisik):** Membawa bit melalui media fisik (sinyal, kabel, frekuensi radio).
*   **Data Link:** Mengatur pengiriman *frame* pada satu tautan/domain lokal, termasuk pengalamatan MAC dan deteksi kesalahan.
*   **Network (Jaringan):** Menyediakan pengalamatan logis (IP) dan menentukan rute (*routing*) paket melintasi berbagai jaringan.
*   **Transport:** Memfasilitasi komunikasi antaraplikasi (menggunakan port), melakukan *multiplexing*, serta bisa memberi fitur keandalan arus data.
*   **Session (Sesi):** Membentuk, memelihara, dan mengakhiri sesi/dialog komunikasi antaraplikasi.
*   **Presentation (Presentasi):** Menangani representasi, format, kompresi, dan enkripsi data agar dapat dipahami kedua pihak.
*   **Application (Aplikasi):** Menyediakan layanan komunikasi jaringan langsung bagi proses aplikasi pengguna (seperti HTTP, DNS).

**4. Sebutkan empat lapisan model TCP/IP.**
*Application*, *Transport*, *Internet*, dan *Network Access*.

**5. Mengapa model TCP/IP kadang disajikan sebagai lima lapisan?**
Untuk tujuan pembelajaran (pedagogis). Lapisan terbawah (*Network Access*) sering dipisah menjadi *Data Link* dan *Physical* agar perbedaan antara pengiriman bingkai logis (*framing/switching*) dengan transmisi sinyal pada media fisik menjadi lebih jelas.

**6. Apa perbedaan frame, IP packet, TCP segment, dan UDP datagram?**
*   **Frame:** Unit data Layer 2 (*Data Link*) yang berisi informasi pengiriman lokal seperti alamat MAC dan pengecekan galat (FCS).
*   **IP Packet (Datagram):** Unit data Layer 3 (*Network*) yang memiliki alamat IP logis untuk pengantaran lintas jaringan/router.
*   **TCP Segment:** Unit data TCP di Layer 4 (*Transport*) yang berorientasi koneksi, dilengkapi nomor urut untuk keandalan transmisi.
*   **UDP Datagram:** Unit data UDP di Layer 4 (*Transport*) yang lebih sederhana, ringan, dan dikirim tanpa mekanisme keandalan atau pembentukan koneksi.

**7. Definisikan header, trailer, dan payload.**
*   **Header:** Informasi kendali tambahan yang diletakkan *sebelum* data utama oleh suatu protokol.
*   **Trailer:** Informasi kendali yang ditambahkan *setelah* data utama (contohnya *Frame Check Sequence* pada Ethernet).
*   **Payload:** Data utama yang sedang dibawa atau dibungkus, yang biasanya merupakan keseluruhan PDU utuh dari lapisan di atasnya.

**8. Jelaskan enkapsulasi dan dekapsulasi.**
*   **Enkapsulasi:** Proses pengirim menambahkan informasi kendali (*header/trailer*) pada setiap lapisan saat data bergerak turun dari lapisan Aplikasi menuju lapisan Fisik.
*   **Dekapsulasi:** Proses penerima memeriksa dan melepas informasi kendali tersebut lapis demi lapis saat data bergerak naik menuju aplikasi tujuan.

**9. Apa fungsi multiplexing dan demultiplexing?**
*   **Multiplexing:** Proses di sisi pengirim untuk menggabungkan aliran data dari berbagai aplikasi berbeda agar bisa dikirim melalui layanan jaringan yang sama (menggunakan pengenal seperti nomor port).
*   **Demultiplexing:** Proses di sisi penerima untuk memisahkan lalu mendistribusikan data yang masuk ke proses/aplikasi yang tepat berdasarkan pengenal tersebut.

**10. Mengapa OSI tidak boleh dianggap sebagai spesifikasi implementasi?**
Model OSI dirancang oleh ISO sebagai kerangka referensi konseptual untuk memberikan bahasa dan pemahaman yang sama mengenai jaringan. Ia bukan sekumpulan perangkat lunak atau standar teknis kaku yang harus diimplementasikan secara mutlak ke dalam tujuh komponen terpisah di dunia nyata.

---

## Level B — Penerapan dan Analisis

**1. Petakan HTTP, TLS, TCP, UDP, QUIC, IPv6, ICMP, Ethernet, Wi-Fi, dan DNS ke model TCP/IP. Tandai protokol yang pemetaannya memerlukan penjelasan.**
*   **Application:** HTTP, DNS
*   **Transport:** TCP, UDP
*   **Internet:** IPv6
*   **Network Access:** Ethernet, Wi-Fi
*   **Memerlukan Penjelasan (*):**
    *   **TLS (*):** Secara konseptual berada di antara *Application* dan *Transport* (sering dipetakan ke fungsi *Presentation/Session* OSI), tetapi dalam TCP/IP biasanya dianggap bagian dari *Application* yang membungkus antarmuka transport.
    *   **QUIC (*):** Arsitekturnya adalah protokol *Transport* yang menyediakan keandalan dan kontrol kemacetan, tetapi ia berjalan di atas UDP (yang juga *Transport*) agar dapat menembus perangkat jaringan (NAT/Firewall) dengan mudah.
    *   **ICMP (*):** Dienkapsulasi di dalam IP (seolah-olah payload layer di atasnya), tetapi fungsinya adalah kontrol dan pelaporan kesalahan murni untuk lapisan *Internet*.

**2. Gambarkan enkapsulasi permintaan DNS melalui UDP, IPv4, dan Ethernet. Sebutkan pengenal yang digunakan pada setiap batas.**
*   **Application:** Pesan kueri DNS dibuat. Pengenal batas: Nama domain/Transaction ID.
*   **Transport:** Header UDP ditambahkan membungkus pesan DNS. Pengenal batas: Port Tujuan 53, Port Sumber acak.
*   **Internet:** Header IPv4 ditambahkan membungkus datagram UDP. Pengenal batas: Protocol = 17 (UDP), IP Sumber, IP Tujuan.
*   **Network Access:** Header dan Trailer (FCS) Ethernet ditambahkan membungkus paket IP. Pengenal batas: EtherType `0x0800` (IPv4), MAC Address Sumber dan Tujuan.

**3. Ulangi soal sebelumnya untuk HTTP/3 melalui QUIC. Jelaskan mengapa QUIC tetap dapat dianggap transport meskipun menggunakan UDP.**
*   **Application:** HTTP/3 payload disiapkan.
*   **Transport (QUIC & UDP):** Frame QUIC (yang menangani keamanan/sesi/keandalan) ditambahkan, lalu dibungkus lagi ke dalam datagram UDP. Pengenal batas: Port UDP (biasanya 443) dan Connection ID pada QUIC.
*   **Internet & Network Access:** Berlanjut ke IP lalu Ethernet/Wi-Fi (seperti soal sebelumnya).
*   **Alasan QUIC dianggap transport:** Meskipun "menumpang" di atas UDP, QUIC secara mandiri mengimplementasikan fungsi sejati Layer 4 seperti pembentukan koneksi, pengurutan, kontrol aliran, dan retransmisi paket yang hilang, yang secara fungsional menggantikan TCP.

**4. Dua host berada pada subnet berbeda. Jelaskan header mana yang berubah dan tetap ketika paket melewati satu router, dengan mengabaikan NAT.**
*   **Berubah:** Header dan Trailer Layer 2 (MAC Address diganti total menyesuaikan tautan keluar), serta TTL (*Time to Live*) pada Header IP berkurang 1 dan IP Checksum dihitung ulang.
*   **Tetap:** Alamat IP Sumber dan Tujuan (Layer 3), seluruh header Transport (Port Layer 4), dan muatan data (Payload).

**5. Jelaskan perubahan analisis apabila router tersebut juga melakukan NAT/PAT.**
Selain perubahan pada Layer 2 dan TTL, router juga akan mengubah IP Sumber (pada *Source NAT*) atau IP Tujuan (pada *Destination NAT*). Karena menggunakan PAT (*Port Address Translation*), router juga mengubah Port Sumber atau Port Tujuan pada header TCP/UDP. Akibatnya, Checksum Transport juga wajib dihitung ulang.

**6. Sebuah capture menunjukkan checksum TCP salah pada paket keluar, tetapi tidak ada gangguan komunikasi. Ajukan hipotesis yang berkaitan dengan NIC offload.**
Fitur NIC Offload (*Tx Checksum Offload*) sedang aktif. Aplikasi *packet sniffer* (seperti Wireshark) menangkap paket di tingkat sistem operasi perangkat pengirim sebelum paket tersebut diserahkan ke kartu jaringan (NIC) fisik. OS membiarkan field checksum kosong atau diisi data acak, dan perangkat keras NIC-lah yang menghitung lalu menyisipkan checksum yang benar sesaat sebelum paket masuk ke kabel/udara.

**7. Pengguna dapat membuka portal dengan alamat IP, tetapi tidak dengan nama. Gunakan model lapisan untuk menyusun diagnosis.**
*   **Layer 1-3 (Fisik hingga Internet):** Normal. Konektivitas dasar (routing, sinyal fisik, IP) terbukti berfungsi karena alamat IP bisa diakses.
*   **Layer 4 (Transport):** Normal. TCP berjalan lancar ke web server.
*   **Layer 7 (Application):** Terjadi kegagalan DNS. Klien tidak dapat menerjemahkan nama domain ke alamat IP karena salah konfigurasi server DNS lokal, server DNS *down*, atau rekor domain tersebut belum dipublikasikan.

**8. Ping ke server berhasil, tetapi HTTPS gagal. Susun sedikitnya enam hipotesis pada lapisan Transport hingga Application.**
1.  **(Transport)** Port TCP 443 diblokir oleh Firewall di klien, router perantara, atau server.
2.  **(Transport)** Layanan/Daemon Web Server sedang mati (*down*) sehingga tidak ada yang mendengarkan (*Listen*) di Port 443.
3.  **(Application/TLS)** Konfigurasi sertifikat SSL/TLS kedaluwarsa, tidak valid, atau *mismatch*, membuat peramban memutus koneksi.
4.  **(Application/TLS)** Klien dan Server tidak memiliki kesepakatan *Cipher Suite* atau versi protokol TLS yang sama (misal server hanya menerima TLS 1.3, klien hanya mendukung TLS 1.0).
5.  **(Application/HTTP)** Server kelebihan beban (*overload*) sehingga menolak pembentukan koneksi TCP baru.
6.  **(Application)** *Reverse proxy* atau *Load balancer* di depan server salah melakukan *routing* untuk *virtual host* HTTPS tersebut.

**9. Bandingkan sesi aplikasi dengan koneksi TCP. Berikan contoh ketika sesi bertahan setelah koneksi berubah.**
Koneksi TCP (Layer 4) bersifat jaringan murni, mengandalkan *handshake*, nomor urut, dan akan putus jika IP/jaringan berubah. Sesi aplikasi (Layer 7) bersifat logis di tingkat perangkat lunak, menggunakan token, *cookie*, atau *Session ID*.
*   **Contoh:** Anda masuk (*login*) ke sebuah aplikasi *e-commerce* melalui Wi-Fi. Anda berjalan keluar dan berpindah ke jaringan seluler. Koneksi TCP terputus, lalu perangkat membentuk koneksi TCP baru dengan IP seluler. Namun, karena peramban masih menyimpan dan mengirimkan *Cookie* Sesi, Anda tetap dalam keadaan masuk (*logged in*) tanpa perlu mengetik kata sandi lagi.

**10. Jelaskan mengapa enkripsi tidak dapat selalu ditempatkan secara mutlak pada Presentation layer.**
Penempatan enkripsi bergantung pada batas kepercayaan dan kebutuhan spesifik aplikasi. Jika enkripsi dikunci mutlak di Layer 6, kita tidak bisa melakukan pelindungan menyeluruh. Misalnya, IPsec (*Network Layer*) digunakan untuk mengenkripsi jaringan antar-kantor secara transparan; MACsec (*Data Link*) melindungi dari penyadapan kabel fisik antar-switch; sedangkan enkripsi pada ujung-ke-ujung (E2EE seperti WhatsApp) dilakukan murni oleh aplikasi (*Application Layer*) sebelum data diserahkan ke tumpukan OS jaringan. Fleksibilitas lapisan ini penting untuk keamanan yang bertingkat.

---

## Level C — Evaluasi dan Sintesis

**1. Evaluasi pernyataan: “Model OSI tidak lagi relevan karena Internet menggunakan TCP/IP.” Susun argumen akademik yang membedakan model, protokol, dan kegunaan pedagogis.**
Pernyataan tersebut kurang tepat. Walaupun *protocol suite* OSI kalah bersaing secara komersial dari tumpukan TCP/IP pada arsitektur Internet nyata, Model OSI tetap sangat relevan sebagai model referensi konseptual dan kerangka pedagogis:
*   **Model vs. Protokol:** OSI adalah kerangka acuan teoritis, sedangkan TCP/IP adalah implementasi protokol praktis.
*   **Kegunaan Pedagogis & Terminologi:** OSI menyediakan abstraksi 7 lapisan yang membantu memisahkan fungsi sistem dengan jelas. Istilah industri seperti “Layer 2 Switch”, “Layer 4 Load Balancer”, atau “Layer 7 Firewall” semuanya mengacu pada taksonomi OSI.
*   **Diagnosis & Analisis:** Pemisahan fungsional OSI (khususnya pembagian *Physical/Data Link* serta *Session/Presentation*) mempermudah insinyur mengisolasi titik kegagalan sistem secara tersusun.

**2. Analisis keuntungan dan kerugian *strict layering*. Kapan *cross-layer information* dapat membantu dan kapan ia merusak modularitas?**
*   **Keuntungan *Strict Layering*:** Mendukung modularitas tinggi, *encapsulation*, kemudahan pengembangan mandiri (*independent evolution*), serta interoperabilitas antar-vendor.
*   **Kerugian *Strict Layering*:** Menimbulkan overhead header berulang, potensi duplikasi fungsi (misal deteksi galat di L2, L3, L4, dan L7), serta menutupi kondisi jaringan bawah dari lapisan atas.
*   **Penggunaan *Cross-Layer Information*:**
    *   **Membantu:** Pada jaringan nirkabel/seluler, mengumpankan indikator sinyal (RSSI/BER dari L1/L2) ke L4 (TCP) membantu TCP membedakan paket hilang akibat interferensi sinyal vs. kemacetan jaringan (*congestion*). Pada *streaming* video (DASH/QUIC), aplikasi L7 memanfaatkan estimasi *bandwidth* L3/L4 untuk menyesuaikan bitrate secara dinamis.
    *   **Merusak:** Ketika menciptakan *tight coupling* (keterikatan kuat). Jika aplikasi L7 dirancang bergantung langsung pada parameter fisik L1/L2 tertentu, aplikasi tersebut akan gagal berfungsi saat dipindahkan ke media transmisi lain (misal dari Ethernet ke Satelit/Wi-Fi).

**3. Buat prosedur penelusuran gangguan untuk kasus video konferensi yang tersendat hanya pada Wi-Fi kampus saat jam sibuk. Hubungkan bukti pada sedikitnya empat lapisan.**
*   **Layer 1 (Physical):** Memeriksa kualitas sinyal dan interferensi frekuensi radio. *Bukti:* Indikator RSSI rendah, *Noise Floor* meningkat, serta *Channel Utilization* pada pita 2.4 GHz mencapai 100% akibat akumulasi perangkat aktif.
*   **Layer 2 (Data Link):** Memeriksa persaingan akses media Wi-Fi (802.11 MAC). *Bukti:* Persentase *Frame Retry Rate* tinggi dan durasi *Contention Window/Backoff* membengkak pada Access Point (AP) akibat tingginya angka kolisi udara.
*   **Layer 3 (Network):** Memeriksa ketersendatan pengiriman paket dan latensi. *Bukti:* Lonjakan variasi waktu tempuh bolak-balik (*jitter*) dan terjadinya pembuangan paket (*bufferbloat/packet drop*) pada antrean L3 router/AP saat jam sibuk.
*   **Layer 4 / 7 (Transport & Application):** Memeriksa statistik aliran video *real-time* (UDP/RTP/QUIC). *Bukti:* Tingginya *Packet Loss Rate* pada aplikasi (Zoom/WebRTC) yang memicu *jitter buffer overrun*, ditandai dengan penurunan resolusi otomatis atau video membeku (*skipping/freezing*).

**4. Rancang skenario laboratorium perekaman paket yang menunjukkan Ethernet, IP, TCP atau UDP, TLS, dan protokol aplikasi tanpa mengumpulkan data sensitif.**
*   **Skenario:** Klien menjalankan perintah kueri web publik non-autentikasi: `curl -v https://example.com` sembari mengaktifkan penganalisis paket (Wireshark/tshark) dengan filter penangkapan spesifik `host example.com and port 443`.
*   **Elemen PDU yang Diamati:**
    *   **Ethernet (L2):** MAC Sumber (Klien), MAC Tujuan (Gateway), EtherType `0x0800` (IPv4).
    *   **IP (L3):** Alamat IP Sumber, IP Tujuan, TTL, Protocol 6 (TCP).
    *   **TCP (L4):** Port Sumber acak, Port Tujuan 443, Flags (SYN, ACK), Sequence Number.
    *   **TLS (L6/L7):** TLS Record Layer, pesan Handshake (Client Hello, Server Hello), indikator SNI (Server Name Indication).
    *   **Application (L7):** Data terenkripsi (*Encrypted Application Data*).
*   **Pencegahan Data Sensitif:** Pengujian dilakukan pada Domain Publik Datar (tanpa form *login*, *cookie*, atau token) dan kunci enkripsi TLS (SSLKEYLOGFILE) tidak diekspor, sehingga isi payload tetap aman terenkripsi.

**5. Sebuah organisasi menggunakan VXLAN di atas UDP dan IPsec tunnel. Gambarkan kemungkinan urutan header dan jelaskan risiko MTU.**
*   **Urutan Header (dari luar ke dalam):**
    Outer Ethernet $\rightarrow$ Outer IP (IPsec/Underlay) $\rightarrow$ ESP Header $\rightarrow$ Outer UDP (Port 4789) $\rightarrow$ VXLAN Header $\rightarrow$ Inner Ethernet (Overlay) $\rightarrow$ Inner IP $\rightarrow$ Payload
*   **Risiko MTU & Fragmentasi:**
    Penambahan header VXLAN (~50 byte) dan enkapsulasi IPsec ESP (~50–73+ byte) menghasilkan *overhead* akumulatif hingga >120 byte. Jika paket *overlay* diinisialisasi pada MTU standar 1500 byte, total ukuran frame akan melebihi batas MTU *underlay* fisik. Hal ini memicu fragmentasi IP di tingkat *underlay* (meningkatkan beban CPU router) atau pembuangan paket (*packet drop*) jika bit *Don't Fragment* (DF) aktif.
*   **Solusi:** Mengonfigurasi *Jumbo Frames* (MTU $\geq 1600$ byte) pada seluruh infrastruktur *underlay* fisik.

**6. Bandingkan perlindungan MACsec, IPsec, TLS, dan enkripsi end-to-end aplikasi dari sisi cakupan kepercayaan dan titik terminasi.**

| Parameter | MACsec (802.1AE) | IPsec (Tunnel/Transport) | TLS | Enkripsi E2E Aplikasi |
| :--- | :--- | :--- | :--- | :--- |
| **Lapisan Protocol** | Layer 2 (*Data Link*) | Layer 3 (*Network*) | Layer 4.5 / *Application* | Layer 7 (*Application*) |
| **Cakupan Kepercayaan** | *Hop-by-hop* (antar-antarmuka fisik terhubung) | *Network-to-Network* / *Host-to-Network* | *Process-to-Process* (Client ke Server) | *User-to-User* (*Endpoint* Pengirim ke Penerima) |
| **Titik Terminasi** | Port NIC / Switch terdekat | Gateway VPN / Firewall / Router | Socket Aplikasi pada Server/Proxy | Aplikasi pada perangkat pengguna akhir |
| **Metadata Terlihat** | Hanya *preamble* fisik L1 | MAC Address L2 | MAC & IP Address L3, Port L4 | MAC, IP, Port L4, TLS Metadata |

**7. Jelaskan bagaimana firewall, proxy, dan load balancer menantang anggapan bahwa setiap perangkat hanya membaca header lapisannya.**
Perangkat modern seperti Firewall, Proxy, dan Load Balancer mendobrak asumsi bahwa perangkat perantara hanya membaca headernya sendiri:
*   **Next-Generation Firewall (NGFW):** Memeriksa L3/L4 untuk filter koneksi, namun sekaligus melakukan *Deep Packet Inspection* (DPI) hingga L7 untuk mengenali jenis aplikasi dan memblokir *malware*.
*   **Reverse Proxy & L7 Load Balancer (misal Nginx):** Menerima koneksi TCP dan menghentikan (*terminate*) sesi TLS (L4–L6), dekapsulasi data hingga *payload* HTTP (L7) untuk membaca Header/Cookie/URL, lalu membuat koneksi TCP baru ke server *backend*.
*   **Implikasi Arsitektural:** Perangkat-perangkat ini melanggar prinsip *end-to-end transparency* demi fungsi keamanan, pemantauan, dan optimasi performa.

**8. Gunakan prinsip end-to-end untuk mengevaluasi penempatan fungsi pemeriksaan integritas berkas pada router, transport, atau aplikasi.**
Berdasarkan *End-to-End Principle* (Saltzer et al.), pemeriksaan integritas berkas harus ditempatkan pada **Lapisan Aplikasi**:
*   **Di Router (L3):** Hanya memeriksa integritas transmisi lokal antar-hop. Router tidak dapat mendeteksi jika berkas rusak pada memori/disk pengirim sebelum dikirim.
*   **Di Transport (L4 - TCP Checksum):** Hanya menjamin segmen tidak mengalami korupsi bit saat transit di jaringan. Tidak melindungi data dari kegagalan sistem berkas atau korupsi memori internal pada OS.
*   **Di Aplikasi (L7 - Hash SHA-256):** Klien menghitung *hash* dari berkas utuh yang diterima lalu membandingkannya dengan nilai hash resmi dari sumber. Ini memberikan jaminan integritas menyeluruh (*end-to-end*) dari *storage-to-storage*.

**9. Analisis potensi retry storm ketika aplikasi, service mesh, dan client sama-sama melakukan pengulangan. Jelaskan mengapa masalah ini bersifat lintas lapisan.**
*   **Mekanisme Pemicu & Amplifikasi:** Saat terjadi keterlambatan singkat pada server tujuan, percakapan diulang secara independen oleh tiga tingkatan: Transport L4 melakukan *TCP Retransmission*, Service Mesh L7 (seperti Envoy) melakukan HTTP *Retry*, dan Aplikasi/Klien L7 mengirim ulang *request*. Akibatnya, jumlah panggilan membengkak secara eksponensial: $(N_{klien} \times N_{mesh} \times N_{TCP})$.
*   **Mengapa Lintas Lapisan:** Masalah ini terjadi akibat ketiadaan koordinasi antar-lapisan. Setiap lapisan mencoba mengatasi kegagalan secara mandiri tanpa menyadari bahwa lapisan lain juga melakukan hal yang sama, sehingga justru memperparah tingkat kemacetan server (*Cascading Failure*).
*   **Mitigasi:** Menerapkan *exponential backoff with jitter*, penentuan *retry budgets* terpusat pada Service Mesh, dan *circuit breakers*.

**10. Susun argumen apakah materi jaringan pemula sebaiknya memakai model OSI tujuh lapisan, TCP/IP empat lapisan, atau model lima lapisan. Nyatakan tujuan pembelajaran, manfaat, dan keterbatasan pilihan Anda.**
*   **Pilihan Terbaik:** Model 5-Lapisan (*Physical, Data Link, Network/Internet, Transport, Application*).
*   **Tujuan Pembelajaran:** Memberikan pemahaman yang selaras dengan arsitektur Internet modern tanpa mengabaikan pemisahan perangkat keras fisik.
*   **Manfaat:**
    *   **Memisahkan *Physical* dan *Data Link*:** Membantu pemula membedakan media transmisi/sinyal (kabel vs radio) dari pengalamatan fisik logis (MAC Address/Switching), hal yang sering membingungkan jika digabung menjadi "*Network Access*" pada model TCP/IP 4-lapisan.
    *   **Menyatukan Lapisan Atas:** Mengagregasi *Session*, *Presentation*, dan *Application* menjadi satu lapisan *Application*, sesuai dengan kenyataan bahwa fungsi format data dan sesi pada tumpukan Internet dikelola oleh aplikasi/pustaka *software*.
*   **Keterbatasan:** Tidak menjelaskan pemisahan teoritis *Session* dan *Presentation* milik OSI, namun keterbatasan ini tidak mengganggu pemahaman praktis jaringan komputer modern.