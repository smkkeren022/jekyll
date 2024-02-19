## PENJELASAN RADIUS SERVER

RADIUS (Remote Authentication Dial-In User Service) server adalah protokol dan sistem perangkat lunak jaringan yang menyediakan manajemen otentikasi, otorisasi, 
dan akuntansi terpusat untuk pengguna yang terhubung dan menggunakan layanan jaringan. RADIUS umumnya digunakan bersama dengan layanan akses jaringan seperti dial-up, 
virtual private network (VPN), nirkabel, dan layanan akses jaringan lainnya.
Berikut ini adalah gambaran singkat tentang aspek-aspek kunci dari sebuah server RADIUS:

1.	Otentikasi: Server RADIUS mengotentikasi pengguna yang mencoba mengakses jaringan. Ini melibatkan verifikasi kredensial pengguna, 
    seperti nama pengguna dan kata sandi, terhadap database atau sumber otentikasi lainnya.

2.	Otorisasi: Setelah pengguna diotentikasi, server RADIUS menentukan tingkat akses yang diberikan kepada pengguna. 
    Ini melibatkan pemeriksaan izin dan kebijakan pengguna untuk memastikan bahwa mereka memiliki hak yang diperlukan untuk mengakses sumber daya atau layanan tertentu.

3.	Akuntansi: Server RADIUS menyimpan informasi akuntansi terkait sesi pengguna. Ini termasuk mencatat waktu mulai dan berakhirnya sesi pengguna, 
    jumlah data yang ditransfer, dan detail relevan lainnya. Data akuntansi dapat digunakan untuk tujuan penagihan, pemantauan jaringan, dan analisis keamanan.

4.	Model Klien/Server: RADIUS beroperasi pada model klien/server. Perangkat jaringan, seperti router, switch, atau titik akses, 
    bertindak sebagai klien yang meneruskan permintaan otentikasi ke server RADIUS. Server memproses permintaan tersebut dan memberikan respons berupa penerimaan atau penolakan akses.

5.	Keamanan: RADIUS biasanya menggunakan rahasia bersama antara klien dan server untuk mengamankan komunikasi. 
    Rahasia bersama ini digunakan untuk mengenkripsi kata sandi dan informasi sensitif lainnya selama transmisi.

6.	Standar: RADIUS didefinisikan dalam beberapa dokumen Request for Comments (RFC), seperti RFC 2865 dan RFC 2866. 
    Standar ini mendefinisikan protokol dan atribut-atribut yang digunakan untuk otentikasi, otorisasi, dan akuntansi.

Server RADIUS secara luas digunakan dalam lingkungan perusahaan, penyedia layanan internet (ISP), dan organisasi lainnya untuk mengelola dan mengamankan akses jaringan. 
Implementasi server RADIUS yang populer termasuk FreeRADIUS, Microsoft Network Policy Server (NPS), dan Cisco Secure ACS (Access Control Server).

## CARA MENGGUNAKAN RADIUS SERVER

Cara menggunakan server RADIUS melibatkan konfigurasi dan pengaturan pada perangkat jaringan yang akan menggunakannya, seperti router, switch, atau titik akses.
Berikut adalah panduan umum untuk menggunakan server RADIUS:

1.	Persiapkan Server RADIUS:

    •	Instal dan konfigurasi perangkat lunak server RADIUS yang Anda pilih, seperti FreeRADIUS.

    •	Tentukan sumber otentikasi, seperti database pengguna atau layanan otentikasi lainnya, yang akan digunakan oleh server RADIUS untuk memverifikasi pengguna.

2.	Konfigurasi Klien RADIUS:

    •	Pada perangkat jaringan yang akan berfungsi sebagai klien RADIUS (misalnya, router atau titik akses), konfigurasikan parameter koneksi ke server RADIUS.

    •	Atur alamat IP server RADIUS, serta rahasia bersama yang akan digunakan untuk mengamankan komunikasi antara klien dan server.

3.	Otentikasi Pengguna:

    •	Setiap kali pengguna mencoba mengakses jaringan, klien RADIUS akan mengirimkan permintaan otentikasi ke server RADIUS.

    •	Server RADIUS akan memverifikasi kredensial pengguna dan memberikan respons positif atau negatif ke klien.

4.	Otorisasi Akses:

    •	Jika otentikasi berhasil, server RADIUS menentukan tingkat akses yang diberikan kepada pengguna berdasarkan kebijakan dan izin yang telah ditentukan.

    •	Konfigurasikan parameter otorisasi yang diperlukan pada perangkat klien.

5.	Akuntansi:

    •	Server RADIUS mencatat informasi akuntansi terkait sesi pengguna, seperti waktu mulai dan berakhirnya sesi, jumlah data yang ditransfer, dll.

    •	Pastikan untuk mengonfigurasi perangkat klien untuk mengirimkan informasi akuntansi ke server RADIUS.

6.	Uji Coba:

    •	Lakukan uji coba dengan mencoba mengakses jaringan menggunakan kredensial pengguna yang telah dikonfigurasi.

    •	Periksa log di server RADIUS untuk memastikan bahwa otentikasi, otorisasi, dan akuntansi berfungsi seperti yang diharapkan.

Perlu diingat bahwa langkah-langkah di atas mungkin bervariasi tergantung pada perangkat dan perangkat lunak yang digunakan.
Dokumentasi resmi dari server RADIUS dan perangkat jaringan yang Anda gunakan dapat memberikan panduan yang lebih rinci sesuai dengan konfigurasi spesifik yang Anda terapkan.

## CARA INSTALL RADIUS SERVER

Proses instalasi server RADIUS bisa bervariasi tergantung pada perangkat lunak yang Anda pilih. Di sini, saya akan memberikan panduan umum untuk menginstal FreeRADIUS, 
salah satu implementasi server RADIUS yang populer pada sistem Linux (contoh menggunakan distribusi Ubuntu). 
Pastikan untuk menyesuaikan langkah-langkah sesuai dengan distribusi Linux atau perangkat lunak yang Anda gunakan.

## Instalasi FreeRADIUS di Ubuntu:

1. Buka Terminal:

   Buka terminal pada sistem Ubuntu.

2. Perbarui Paket:

   Pastikan paket sistem Anda diperbarui dengan menjalankan perintah:

        sudo apt update

3. Instal FreeRADIUS:

   Instal FreeRADIUS dengan perintah:    

        sudo apt install freeradius

4. Konfigurasi:

    Setelah instalasi selesai, Anda perlu mengkonfigurasi FreeRADIUS. 
  
    File konfigurasi utama adalah /etc/freeradius/3.0/radiusd.conf. 

    Edit file ini sesuai kebutuhan Anda dengan menggunakan editor teks seperti nano atau vim.

       sudo nano /etc/freeradius/3.0/radiusd.conf

5. Mulai Layanan:

    Setelah mengonfigurasi, mulai layanan FreeRADIUS:

       sudo service freeradius start

6. Uji Coba:

    Lakukan uji coba dengan menggunakan perintah radtest. Contoh:

        radtest username password 127.0.0.1 0 testing123

    Gantilah username dan password sesuai dengan kredensial pengguna yang ingin Anda uji.

7. Periksa Log:

    Periksa log untuk melihat apakah ada masalah atau pesan kesalahan:

        sudo tail -f /var/log/freeradius/radius.log












