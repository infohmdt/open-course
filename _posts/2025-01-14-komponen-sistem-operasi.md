---
title: Komponen Sistem Operasi
categories: [OS, Learning Materials]
tags: [operating system]
author: rical
---

## Pendahuluan
---

Komponen sistem operasi berfungsi untuk memastikan bahwa berbagai bagian dari komputer dapat bekerja sama secara efektif. Semua perangkat lunak pengguna harus melalui sistem operasi untuk dapat berinteraksi dengan perangkat keras, baik itu perangkat sederhana seperti mouse dan keyboard, maupun komponen yang lebih kompleks seperti koneksi internet.

## Kernel
---

Kernel adalah komponen yang menghubungkan perangkat lunak aplikasi dengan perangkat keras komputer. Dengan bantuan firmware dan device driver, kernel menyediakan kontrol dasar atas semua perangkat keras. Fungsi utama kernel meliputi:

- Mengatur akses memori untuk program yang berjalan di RAM.
- Menentukan program mana yang mendapatkan akses ke sumber daya perangkat keras.
- Mengatur kondisi operasi CPU untuk memastikan kinerja optimal.
- Mengelola penyimpanan data jangka panjang pada media non-volatile melalui sistem file.

## Eksekusi Program
---

Sistem operasi menyediakan antarmuka antara program aplikasi dan perangkat keras, memungkinkan program aplikasi untuk berinteraksi dengan perangkat keras dengan mematuhi aturan dan prosedur yang telah diprogram. Eksekusi program aplikasi melibatkan:

- Pembuatan ruang memori dan alokasi sumber daya oleh kernel.
- Penetapan prioritas untuk proses dalam sistem multi-tasking.
- Memasukkan kode biner program ke dalam memori dan memulai eksekusi.

## Interupsi
---

Interupsi adalah mekanisme penting dalam sistem operasi yang memungkinkan interaksi efisien dengan lingkungan. Interupsi dapat berasal dari perangkat keras atau program yang berjalan. Ketika interupsi diterima, perangkat keras menunda semua program yang sedang berjalan, menyimpan statusnya, dan menjalankan kode terkait interupsi. Proses ini mirip dengan menandai halaman buku saat menerima panggilan telepon.

Kernel sistem operasi bertanggung jawab untuk menangani interupsi, yang dapat berasal dari perangkat keras atau program. Penanganan interupsi biasanya didelegasikan kepada device driver, yang dapat menjadi bagian dari kernel atau program lain. Program juga dapat memicu interupsi untuk meminta akses ke perangkat keras atau sumber daya tambahan.

## Mode
---

Terdapat dua mode utama dalam sistem operasi: **Mode Protected** dan **Mode Supervisor**. 

- **Mode Supervisor** digunakan oleh kernel untuk tugas-tugas yang memerlukan akses penuh ke perangkat keras, seperti pengelolaan memori dan komunikasi dengan perangkat.
- **Mode Protected** digunakan untuk aplikasi yang beroperasi dengan akses terbatas ke perangkat keras, melalui komunikasi dengan kernel.

Ketika komputer dinyalakan, ia secara otomatis berjalan dalam mode supervisor. Namun, setelah sistem operasi mengalihkan kontrol ke program lain, CPU dapat diatur ke mode protected.

## Manajemen Memori
---

Kernel sistem operasi multiprogramming bertanggung jawab untuk mengelola memori yang digunakan oleh program, memastikan bahwa program tidak saling mengganggu. Ada dua metode utama dalam manajemen memori:

1. **Cooperative Memory Management**: Metode ini mengandalkan program untuk secara sukarela menggunakan manajer memori kernel. Namun, metode ini jarang digunakan karena dapat menyebabkan program mengalokasikan memori melebihi batas yang ditentukan, berpotensi mengganggu program lain.

2. **Memory Protection**: Metode ini membatasi akses proses ke memori komputer. Terdapat berbagai teknik, termasuk segmentasi dan paging, yang memerlukan dukungan perangkat keras tertentu. Upaya untuk mengakses alamat memori yang tidak diizinkan akan memicu interupsi, yang mengembalikan kontrol ke kernel.

Kesalahan segmentasi, yang sering muncul di Windows sebagai layar biru, adalah contoh dari pelanggaran akses memori yang dapat terjadi ketika program mencoba mengakses alamat yang tidak dialokasikan. Kernel biasanya akan menghentikan program yang menyebabkan kesalahan ini dan melaporkan kesalahan yang terjadi.

## Memori Virtual
---

Banyak sistem operasi memiliki kemampuan untuk "menipu" program agar menggunakan memori yang tersebar di seluruh hard disk dan RAM seolah-olah itu adalah satu blok kontinu memori, yang dikenal sebagai memori virtual.

Penggunaan pengalamatan memori virtual, seperti paging atau segmentasi, memungkinkan kernel untuk memilih memori yang digunakan oleh setiap program pada waktu tertentu. Hal ini memungkinkan sistem operasi untuk memanfaatkan lokasi memori yang sama untuk berbagai keperluan.

Jika sebuah program mencoba mengakses memori yang tidak berada dalam rentang yang dapat diakses, tetapi tetap telah dialokasikan untuk program tersebut, kernel akan mengalami interupsi dengan cara yang sama seperti ketika program melebihi batas memori yang dialokasikan. Dalam sistem UNIX, interupsi jenis ini disebut sebagai kesalahan halaman (page fault).

Ketika kernel mendeteksi kesalahan halaman, ia umumnya akan menyesuaikan rentang memori virtual bagi program yang memicunya, memberikan akses ke memori yang diminta. Ini memberikan kekuatan kepada kernel untuk menentukan di mana memori dari aplikasi tertentu disimpan, serta apakah memori tersebut sudah dialokasikan atau belum.

Dalam sistem operasi modern, memori yang jarang diakses dapat disimpan sementara di disk atau media lain untuk membuat ruang yang tersedia bagi program lain. Proses ini disebut swapping, di mana daerah memori dapat digunakan oleh beberapa program, dan isi memori di daerah tersebut dapat ditukar (swap) sesuai permintaan.

"Memori virtual" memberikan persepsi kepada programmer dan pengguna bahwa terdapat RAM dalam jumlah yang jauh lebih besar daripada yang sebenarnya ada di komputer.

## Multitasking
---

Multitasking adalah kemampuan untuk menjalankan beberapa program komputer secara independen pada komputer yang sama, memberikan kesan bahwa komputer dapat melakukan beberapa tugas secara bersamaan. Karena kebanyakan komputer hanya dapat melakukan satu atau dua hal pada satu waktu, multitasking biasanya dilakukan menggunakan metode time-sharing, di mana setiap program menggunakan sebagian dari waktu CPU saat dieksekusi.

Kernel sistem operasi dilengkapi dengan perangkat lunak yang disebut scheduler, yang menentukan berapa banyak waktu yang dapat digunakan setiap program selama eksekusi. Kontrol eksekusi diberikan kepada sebuah proses oleh kernel, yang memungkinkan program untuk mengakses CPU atau memori. Setelah itu, kontrol dikembalikan ke kernel melalui mekanisme tertentu, sehingga program lain dapat menggunakan CPU. Proses pemberian kontrol antara kernel dan aplikasi biasanya disebut sebagai context switch.

Model awal yang mengatur alokasi waktu untuk program disebut cooperative multitasking. Dalam model ini, ketika kontrol diberikan kepada program oleh kernel, program dapat berjalan selama yang diinginkan sebelum secara eksplisit mengembalikan kontrol ke kernel. Hal ini berarti bahwa program yang tidak berfungsi atau berperilaku buruk dapat mencegah program lain dari menggunakan CPU, bahkan dapat menggantung seluruh sistem jika memasuki infinite loop.

Sistem operasi modern memperluas konsep preemption ke device driver dan kode kernel, sehingga sistem operasi memiliki kontrol preemptive atas runtime internal juga.

Filosofi di balik preemptive multitasking adalah untuk memastikan bahwa semua program mendapatkan waktu di CPU. Ini menunjukkan bahwa semua program harus dibatasi dalam berapa banyak waktu yang diizinkan untuk dihabiskan di CPU tanpa interupsi. Untuk mencapai hal ini, kernel sistem operasi modern menggunakan interupsi berjangka. Sebuah timer dalam mode protected diatur oleh kernel yang memicu pengembalian ke mode supervisor setelah waktu yang ditentukan berlalu.

Pada banyak sistem operasi single user, cooperative multitasking cukup memadai, karena umumnya komputer rumah (PC) menjalankan sejumlah program yang telah teruji. AmigaOS adalah pengecualian, karena menggunakan preemptive multitasking sejak versi pertamanya. Windows NT merupakan versi pertama dari Microsoft Windows yang menerapkan preemptive multitasking, tetapi tidak mencapai pasar pengguna rumah hingga Windows XP, karena Windows NT ditujukan untuk profesional.

## Akses Disk dan Sistem File
---

Sistem file memungkinkan pengguna dan program untuk mengatur dan menata file pada komputer, biasanya melalui penggunaan direktori (atau "folder"). Akses ke data yang tersimpan pada disk adalah fitur utama dari semua sistem operasi. Komputer menyimpan data pada disk menggunakan file yang terstruktur sedemikian rupa untuk memungkinkan akses yang cepat, keandalan yang lebih tinggi, dan untuk memaksimalkan penggunaan ruang yang tersedia pada disk. Cara khusus di mana file tersebut disimpan pada disk disebut sistem file, yang memungkinkan file memiliki nama dan atribut, serta disimpan dalam hirarki direktori yang terorganisir.

Sistem operasi awal umumnya mendukung satu jenis disk drive dan hanya satu jenis sistem file. Sistem file awal terbatas dalam kapasitas, kecepatan, dan dalam jenis nama file serta struktur direktori yang dapat mereka gunakan. Keterbatasan ini sering kali mencerminkan keterbatasan dalam desain sistem operasi, sehingga sangat sulit bagi sebuah sistem operasi untuk mendukung lebih dari satu sistem file.

Sementara banyak sistem operasi sederhana mendukung berbagai pilihan terbatas untuk mengakses sistem penyimpanan, sistem operasi seperti UNIX dan Linux mendukung teknologi yang dikenal sebagai Virtual File System (VFS). Sistem operasi seperti UNIX mendukung beragam perangkat penyimpanan, terlepas dari desain atau sistem file, yang memungkinkan akses melalui Application Programming Interface (API) yang sama. Hal ini menghilangkan kebutuhan bagi program untuk memiliki pengetahuan tentang perangkat yang mereka akses. VFS memungkinkan sistem operasi untuk menyediakan program dengan akses ke sejumlah perangkat yang tidak terbatas dengan berbagai sistem file terinstal, melalui penggunaan driver perangkat tertentu dan driver sistem file.

Perangkat penyimpanan yang terhubung, seperti hard drive, diakses melalui driver yang sama. Driver ini memahami cara berkomunikasi dengan drive dan mampu menerjemahkan perintah ke dalam bahasa standar yang digunakan oleh sistem operasi untuk mengakses semua disk drive. Di UNIX, ini adalah bahasa dari block device.

Ketika kernel memiliki driver yang tepat, ia dapat mengakses isi disk drive dalam format mentah, yang mungkin berisi satu atau lebih sistem file. Driver sistem file digunakan untuk menerjemahkan perintah yang digunakan untuk mengakses setiap sistem file tertentu ke dalam satu set standar perintah yang dapat digunakan oleh sistem operasi untuk berkomunikasi dengan semua sistem file. Program kemudian dapat menangani sistem file ini berdasarkan nama file dan direktori/folder yang berada dalam struktur hirarkis. Mereka dapat membuat, menghapus, membuka, dan menutup file, serta mengumpulkan berbagai informasi tentang file, termasuk hak akses, ukuran, ruang bebas, dan tanggal pembuatan serta tanggal modifikasi.

Berbagai perbedaan antara sistem file membuat dukungan untuk semua sistem file menjadi sulit. Karakter yang diperbolehkan dalam nama file, perbedaan huruf besar/kecil, dan adanya berbagai jenis atribut berkas membuat implementasi satu antarmuka untuk setiap sistem file menjadi tugas yang menantang. Sistem operasi cenderung merekomendasikan penggunaan (dan mendukung secara native) sistem file yang dirancang khusus untuk mereka, misalnya, NTFS di Windows dan ext3 serta ReiserFS di Linux. Namun, dalam praktiknya, ada pihak ketiga yang menyediakan driver untuk memberikan dukungan bagi sistem file yang paling banyak digunakan di sebagian besar sistem operasi (misalnya, NTFS tersedia di Linux melalui NTFS-3g, dan ext2/3 serta ReiserFS tersedia di Windows melalui perangkat lunak pihak ketiga).

Dukungan untuk sistem file sangat bervariasi di antara sistem operasi modern, meskipun ada beberapa sistem file yang sama di hampir semua sistem operasi, termasuk dukungan dan driver. Sistem operasi bervariasi dalam dukungan sistem file dan format disk tempat mereka dapat diinstal. Di Windows, setiap sistem file biasanya terbatas pada aplikasi untuk media tertentu, misalnya, CD harus menggunakan ISO 9660 atau UDF, dan pada Windows Vista, NTFS adalah sistem file di mana sistem operasi dapat diinstal. Berbeda dengan Windows, sangat mungkin untuk menginstal Linux ke berbagai jenis sistem file. Tidak seperti sistem operasi lain, Linux dan UNIX memungkinkan sistem file digunakan terlepas dari media tempat mereka disimpan, apakah itu hard drive, disk (CD, DVD, dll.), USB flash drive, atau bahkan berada dalam file yang terletak di sistem file lain.

## Device Driver
---

Device driver adalah perangkat lunak spesifik yang dikembangkan untuk memungkinkan interaksi antara perangkat keras dan sistem operasi. Biasanya, ini merupakan antarmuka untuk berkomunikasi dengan perangkat melalui bus komputer tertentu atau subsistem komunikasi yang terhubung ke perangkat keras, memberikan perintah dan/atau menerima data dari perangkat, serta menyediakan antarmuka yang diperlukan untuk operasi sistem dan aplikasi perangkat lunak. Device driver adalah program komputer khusus yang tergantung pada perangkat keras dan sistem operasi tertentu, yang memungkinkan program lain, biasanya sistem operasi atau aplikasi yang berjalan di bawah kernel sistem operasi, untuk berinteraksi secara transparan dengan perangkat keras. Driver ini juga biasanya menyediakan penanganan interupsi yang diperlukan untuk perangkat yang bersifat asinkron dan bergantung pada waktu.

### Tujuan dan Desain Device Driver

Tujuan utama dari desain device driver adalah untuk menyediakan abstraksi. Setiap model perangkat keras, bahkan dalam kelas perangkat yang sama, dapat berbeda. Model-model baru sering kali dirilis oleh produsen yang menawarkan performa yang lebih baik, dan cara pengendalian perangkat tersebut juga dapat berbeda. Oleh karena itu, komputer dan sistem operasi tidak dapat diharapkan untuk mengetahui cara mengontrol setiap perangkat, baik yang ada saat ini maupun yang akan datang. Untuk mengatasi masalah ini, sistem operasi mendikte bagaimana setiap jenis perangkat harus dikontrol. Fungsi dari device driver adalah untuk menerjemahkan perintah dari sistem operasi menjadi panggilan fungsi yang sesuai untuk perangkat tertentu. Dalam teori, perangkat baru yang dikendalikan dengan cara baru seharusnya dapat berfungsi dengan baik jika driver yang sesuai tersedia. Driver baru ini memastikan bahwa perangkat yang baru muncul dapat beroperasi dengan baik dari sudut pandang sistem operasi.

### Eksekusi Driver dan Preemption

Pada versi Windows sebelum Vista dan versi Linux sebelum 2.6, semua eksekusi driver bersifat kooperatif, yang berarti bahwa jika driver memasuki infinite loop, sistem dapat mengalami freeze. Revisi lebih baru dari sistem operasi menggabungkan preemption kernel, di mana kernel dapat menginterupsi driver untuk memberikan tugas lain, dan kemudian melepaskan diri dari proses tersebut sampai menerima tanggapan dari device driver, atau memberikan lebih banyak tugas yang dapat dilakukan.

## Jaringan
---

Saat ini, sebagian besar sistem operasi mendukung berbagai protokol jaringan, perangkat keras, dan aplikasi untuk memanfaatkan jaringan tersebut. Hal ini memungkinkan komputer yang menjalankan sistem operasi yang berbeda untuk berpartisipasi dalam jaringan komputer guna berbagi sumber daya seperti komputasi, file, printer, dan pemindai, baik melalui koneksi kabel maupun nirkabel. Jaringan komputer pada dasarnya memungkinkan sistem operasi untuk mengakses sumber daya dari komputer remote, mendukung fungsi yang sama seolah-olah sumber daya tersebut terhubung langsung ke komputer lokal. Ini mencakup segala sesuatu dari komunikasi sederhana hingga penggunaan sistem file jaringan atau berbagi grafis komputer lain serta perangkat keras suara. Beberapa layanan jaringan memungkinkan akses transparan ke sumber daya dari komputer, seperti SSH yang memungkinkan pengguna jaringan untuk mengakses antarmuka baris perintah di komputer remote.

Jaringan client/server memungkinkan sebuah program pada komputer, yang disebut klien, untuk berhubungan melalui jaringan ke komputer lain, yang disebut server. Server menawarkan (atau meng-host) berbagai layanan untuk komputer jaringan lainnya dan pengguna. Layanan ini biasanya diberikan melalui port atau nomor jalur akses yang terpisah dari alamat jaringan server. Setiap nomor port biasanya dikaitkan dengan satu program atau aplikasi yang bertanggung jawab untuk menangani permintaan untuk port tersebut. Daemon adalah program yang berjalan di server dan dapat mengakses sumber daya perangkat keras lokal dengan meneruskan permintaan ke kernel sistem operasi.

Banyak sistem operasi mendukung satu atau lebih protokol jaringan, baik yang proprietary maupun yang open, seperti SNA untuk sistem IBM, DECnet untuk sistem dari Digital Equipment Corporation, dan protokol spesifik Microsoft (SMB) pada Windows. Protokol khusus untuk tugas tertentu juga mungkin didukung, seperti NFS untuk akses file. Protokol seperti esound (esd) dapat dengan mudah diperluas melalui jaringan untuk menyediakan suara dari aplikasi lokal pada perangkat keras suara remote.

Internet adalah salah satu jenis protokol jaringan yang memiliki standar terbuka yang dapat dijalankan di berbagai sistem operasi. Standar Internet dibuat secara kolaboratif oleh banyak pihak dan dapat diakses melalui web dengan kata kunci "Request For Comment" (RFC).

## Keamanan
---

Keamanan komputer bergantung pada sejumlah teknologi yang bekerja dengan baik. Sistem operasi modern menyediakan akses ke berbagai sumber daya yang tersedia untuk perangkat lunak yang berjalan pada sistem, serta perangkat eksternal seperti jaringan melalui kernel.

Sistem operasi harus mampu membedakan antara permintaan yang harus diproses dan yang tidak. Sementara beberapa sistem mungkin hanya membedakan antara "privileged" dan "non-privileged", sistem umumnya memiliki bentuk identitas pemohon, seperti nama pengguna. Untuk menentukan identitas, mungkin ada proses autentikasi. Seringkali, nama pengguna harus diikuti dengan password. Metode autentikasi lain, seperti kartu magnetik atau data biometrik, mungkin digunakan sebagai alternatif. Dalam beberapa kasus, khususnya koneksi dari jaringan, sumber daya dapat diakses tanpa autentikasi sama sekali (seperti membaca file melalui berbagi jaringan). Konsep identitas pemohon juga mencakup otorisasi; layanan tertentu dan sumber daya diakses oleh pemohon setelah login ke sistem yang terikat pada salah satu akun pengguna pemohon atau grup yang dikonfigurasi terkait dengan akun pengguna tersebut.

Selain model keamanan yang berbentuk mengizinkan atau melarang, sistem dengan tingkat keamanan yang tinggi juga akan menawarkan opsi audit. Ini memungkinkan pelacakan permintaan akses ke sumber daya (misalnya, "siapa yang telah membaca file ini?"). Keamanan internal, atau keamanan dari program yang sedang berjalan, hanya mungkin jika semua permintaan yang mungkin berbahaya dilakukan melalui interupsi ke kernel sistem operasi. Jika program dapat langsung mengakses perangkat keras dan sumber daya, mereka tidak dapat diamankan.

Keamanan eksternal melibatkan permintaan dari luar komputer, seperti login di konsol atau beberapa jenis koneksi jaringan. Permintaan eksternal sering melewati device driver ke kernel sistem operasi, di mana mereka dapat diteruskan ke aplikasi atau dilakukan secara langsung. Keamanan sistem operasi telah lama menjadi perhatian karena data yang sangat sensitif yang ada di komputer, baik yang bersifat komersial maupun militer. Departemen Pertahanan Amerika Serikat (DoD) mengusulkan Trusted Computer System Evaluation Criteria (TCSEC), yang merupakan standar yang menetapkan persyaratan dasar untuk menilai efektivitas keamanan. Hal ini menjadi sangat penting bagi para pembuat sistem operasi, karena TCSEC digunakan untuk mengevaluasi, mengklasifikasikan, dan memilih sistem operasi yang dipercaya untuk penyimpanan, pengolahan, dan pengambilan informasi sensitif atau rahasia.

Layanan jaringan mencakup banyak hal seperti berbagi file, layanan pencetakan, email, situs web, dan protokol transfer file (FTP), yang semuanya dapat membahayakan keamanan. Di garis depan keamanan perangkat keras terdapat firewall dan sistem deteksi/pencegahan intrusi. Pada tingkat sistem operasi, terdapat sejumlah firewall perangkat lunak yang tersedia, serta sistem deteksi/pencegahan intrusi. Sebagian besar sistem operasi modern menyertakan perangkat lunak firewall yang diaktifkan secara default. Sebuah perangkat lunak firewall dapat dikonfigurasi untuk mengizinkan atau menolak lalu lintas jaringan ke atau dari suatu layanan atau aplikasi yang berjalan pada sistem operasi. Dengan demikian, pengguna dapat menginstal dan menjalankan layanan yang tidak aman, seperti Telnet atau FTP, tanpa harus khawatir akan pelanggaran keamanan, karena firewall akan menolak semua lalu lintas yang mencoba terhubung ke layanan pada port tersebut.

Strategi alternatif untuk meningkatkan keamanan adalah dengan tidak menjalankan program pengguna sebagai kode native, melainkan dengan mengemulasi prosesor atau menyediakan host untuk sistem berbasis kode seperti Java. Pendekatan ini dapat membantu mengisolasi aplikasi dari sistem operasi dan perangkat keras, sehingga mengurangi risiko potensi kerentanan.

Keamanan internal sangat relevan untuk sistem multi-user, yang memungkinkan setiap pengguna sistem untuk memiliki file pribadi yang tidak dapat diakses atau diubah oleh pengguna lain. Keamanan internal juga penting jika audit akan digunakan, karena program berpotensi dapat melewati sistem operasi, termasuk melewati audit. Dengan demikian, sistem operasi harus dirancang untuk memastikan bahwa semua akses ke sumber daya dan data dapat dilacak dan diaudit, sehingga menjaga integritas dan kerahasiaan informasi yang ada.

## Antarmuka Pengguna
---

Setiap komputer yang akan dioperasikan oleh individu memerlukan antarmuka pengguna. Antarmuka pengguna, yang biasanya disebut sebagai shell, sangat penting untuk mendukung interaksi antara manusia dan komputer. Antarmuka pengguna berfungsi untuk menampilkan struktur direktori dan melayani permintaan dari sistem operasi untuk memperoleh data dari perangkat keras input, seperti pembaca kartu, keyboard, dan mouse, serta untuk menampilkan prompt, pesan status, dan informasi pada perangkat output, seperti monitor video atau printer.

Dua bentuk antarmuka pengguna yang paling umum secara historis adalah **Command Line Interface (CLI)**, di mana perintah komputer diketik baris demi baris, dan **Graphical User Interface (GUI)**, yang menampilkan tampilan visual.

### Command Line Interface (CLI)
---

CLI memungkinkan pengguna untuk berinteraksi dengan sistem operasi melalui perintah yang diketikkan di baris perintah. Setiap perintah ditulis setelah 'prompt', dan output akan ditampilkan di layar di bawahnya. Command prompt biasanya terletak di bagian bawah layar.

### Graphical User Interface (GUI)
---

Sebagian besar sistem komputer modern mendukung antarmuka grafis (GUI) dan sering kali mengintegrasikan GUI sebagai bagian dari sistem operasi. Dalam beberapa sistem komputer, seperti implementasi awal dari Mac OS, GUI terintegrasi ke dalam kernel.

Secara teknis, GUI bukan merupakan layanan sistem operasi. Menggabungkan dukungan untuk GUI ke dalam kernel sistem operasi dapat meningkatkan responsivitas GUI dengan mengurangi jumlah context switch yang diperlukan untuk menjalankan fungsi tampilan. Beberapa sistem operasi bersifat modular, memisahkan subsistem grafis dari kernel dan sistem operasi. Pada tahun 1980-an, UNIX, VMS, dan banyak sistem lainnya dibangun dengan cara ini. Linux dan Mac OS X juga mengikuti pendekatan ini. Rilis modern Microsoft Windows, seperti Windows Vista, menerapkan subsistem grafis sebagian besar di user-space, meskipun subrutin menggambar grafis dalam versi antara Windows NT 4.0 dan Windows Server 2003 sebagian besar berada dalam kernel. Windows 9x memiliki perbedaan yang sangat sedikit antara antarmuka dan kernel.

Banyak sistem operasi komputer memungkinkan pengguna untuk menginstal atau membuat antarmuka pengguna yang mereka inginkan. **X Window System**, dalam hubungannya dengan **GNOME** dan **KDE Plasma Desktop**, adalah setup yang umum ditemukan pada kebanyakan sistem GUI di Unix dan sistem Unix-like (BSD, Linux, Solaris). Sejumlah pengganti shell Windows telah dirilis untuk Microsoft Windows, menawarkan alternatif untuk shell Windows, tetapi shell itu sendiri tidak dapat dipisahkan dari Windows.

Banyak GUI di Unix telah berkembang dari waktu ke waktu, sebagian besar berasal dari X11. Persaingan di antara berbagai vendor Unix (HP, IBM, Sun) menyebabkan fragmentasi yang luas. Upaya untuk membakukan pada tahun 1990-an menuju COSE dan CDE gagal karena berbagai alasan, dan akhirnya dikalahkan dengan diadopsinya GNOME dan K Desktop Environment. Sebelum adanya toolkit dan lingkungan desktop berbasis perangkat lunak bebas, Motif digunakan sebagai toolkit/desktop yang menjadi dasar bagi pengembangan CDE.

Antarmuka Pengguna Grafis (GUI) telah berkembang dari waktu ke waktu. Sebagai contoh, Windows telah mengubah antarmuka pengguna hampir setiap kali versi baru dirilis, dan Mac OS GUI juga mengalami perubahan dramatis dengan pengenalan Mac OS X pada tahun 1999.

## Referensi
---

- [ricalWiki: Komponen Sistem Operasi](https://risnandapascal.github.io/ricalwiki.html)