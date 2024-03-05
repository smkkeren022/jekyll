## Troubleshooting Keamanan Jaringan Pada Jaringan WAN
Troubleshooting Jaringan adalah melakukan serangkaian langkahlangkah untuk mengeliminir potensi-potensi masalah satu persatu sebelum menemukan sumber masalah tersebut yang mengakibatkan jaringan rusak. 2. TUJUAN  Mengidentifikasi alat-alat apa saja yang digunakan untuk melakukan

troubleshooting keamanan jaringan pada jaringan WAN  Menjelaskan cara kerja troubleshooting keamanan jaringan pada jaringan WAN  Mengkonfigurasi troubleshooting keamanan jaringan pada jaringan WAN 3. ALAT DAN BAHAN  Handpone

Laptop  Router  Akses point  Kabel UTP 

# PROSEDUR PRATIKUM
     
A. Konfigurasi wifi router  DNS = sesuai dengan DNS yang diberikan  NTP = YES  Web proxy dengan cache administrator = desta@sekolah.sch.id 
     
B. jaringan internet  Ip Address = sesuai dengan network yang di berikan ISP (eth1)  Gateaway = sesuai dengan IP yang diberikan oleh ISP 
    
C. Jaringan lokal  IP Address = 192.168.40.1/25 (eth2)  DHCP Pool sebanyak 99 client  Buat firewal agar IP 192.168.40.2-192.168.40.50 tidak dapat ping ke router  Buat firewal agar IP 192.168.50.51-192.168.50.100 tidak dapat ping ke client wireles  Buat rule agar setiap akses ke router tercatat di logging dan tersimpan di disk 
    
D. Jaringan wireles IP Address = 192.168.200.1/24 (eth3) SSID = peserta@proxyUKK DHCP Pool sebanyak 99 client Membuat 20 account hotspot secara randon di RADIUS Account hotspot hanya bisa mengunakan internet pada pukul 07.00-16.00 E. Buat firewal yang memblokir  Blocking site = https://www.linux.org  Blocking file = .mp3, .mkv     

# LANGKAH KERJA

Setting akses point untuk client hotspot 

1. Reset access pointnya terlebih dahulu
   
2. Buka browser dan ketikkan “tplinkwifi.net
  
3. Ketikkan pada password:desta1234 dan confirm password:desta1234

4. Setelah itu akan muncul tampilan quick setup, kemudian klik next
Pilih access poin, kemudian next
Masukkan SSID : Desta →security mode:disable wreles security→next
Pilih LAN type: static IP→ DHCP server: disable→ next
Kemudian klik finis
And please wait

5. Ketika sudah selesai mereset access point kemudian pindah ke winbox untuk mereset router dan setting IP address pada router 6. Masuk ke aplikasi winbox kemudian klik IP adddres yang ada di bawah lalu klik connect

6. Ketikkan sesten reset-cinfiguration→ enter→ y Jika sudah muncul seperti gambar dibawah ini Kemudian klik remove configuration

7. Setting ip address pada mikrotik, konfigurasi ip address pada eth1 Klik menu IP→ DHCP Client→ (+)→ Interface: eth1→ apply→ok

8. Konfigurasi ip address pada eth2 dan eth3 Klik menu IP→ address→ (+)→ ketikkan pada address: 192.168.40.1/25→ interface: eth2→ apply→ ok Klik menu IP→ address→ (+)→ ketikkan pada address: 192.168 200.1/24→ interface: eth3→ apply→ ok

9. Konfigurasin DHCP server pada eth2 dan eth3 Klik menu ipDHCP serverDHCPDHCP setupDHCP server interface=ether3nextadddress to give out=192.168.200.1-192.168.200.100next

10. Setting NAT dan NTP I. Setting NAT Klik menu ipfirewalNAT + generalchain=srcnatout interface=ether1action=masquarade

       I. setting zona waktu mikrotik Klik menu systemclocktimetime zone name=asia/jakartaapplayok

      II. setting NTP client Klik systemSNTP clientcentang enabledprimary NTP server=id.pool.ntp.orgsecondary NTP server=asia.pool.ntp.org

11. setting web proxy Klik menu ipweb proxy+generalcentang enabledcentang anoerymouschache administrator=desta@sekolah.sch.idcentang chache on disk

12. setting hotspot mikrotik pada interface eth3 Klik menu iphotspotserverhotspot setuphotspot interface=ether3nextDNS server=8.8.8.8-8.8.4.4nextDNS name=ukk2022.hotspotnext

13. setting radius server (userman) Klik menu RADIUSgeneralcentang hotspotaddress=127.0.0.1applayokRADIUS incomingcentang accep Klik menu iphotspotserverklik dua kali hotspot1centang use RADIUSapplayok

14. Klik menu new terminalketikkan=tool user-manager database clearentery kemudian akan muncul tulisan=user-manager-database-cleared

15. konfigurasi pada sisi server radius Kemudian beralih ke website ketikkan alamat ip ether2=192.168.40.1/usermanenterlogin=adminno passwordlog in

16. membuat profil server radius setelah terbuka tampilan user manager di browser kita, Klik menu routersaddnewname=UKKip address=127.0.0.1time zone=+7add

17. membuat profil user di userman Klik menu profiles+nameprofile UKKcreatelimitationname limit1addkembali ke menu profileklik add new limitationtime=07.00.0016.00.00centang limit1add

18. membuat user di userman Klik menu usersaddbatch number of users=3username length=3password length=3add

19. setting firewal Klik menu ipfirewalfilter rules+generalchain=inputsrc address=192.168.40.2-192.168.40.50protocol=icmpaction=dropapplayok Klik menu ipfirewalfilter rules+generalchain=inputsrc address=192.169.50.1-192.168.50.100Dst address=192.168,200.0/24protocol=icmpaction=drop

21. blok situs dan file Block apk yang tidak diizinkan tersambung pada internet yaitu linux.org,.mp3,.mkv Klik menu ipfirewalfilter rules+generalchain=fowardadvancedcontent=linux.orgaction=drop Klik menu ipfirewalfilter rules+generalchain=fowardadvancedcontent=.mp3action=drop Klik menu ipfirewalfilter rules+generalchain=fowardadvancedcontent=.mkvaction=drop

22. membuat logging access Klik menu ipfirewalfilter lures+generalchain=inputaction=logcentang loglog prefix=akses-kerouterapplayok

23. Klik menu systemlogginrules+prefix=akses-kerouteraction=diskapplayok

24. Pengujian client pada jaringan LAN klik pada keyboard anda windows+Rketik pada open=cmd klik ok

Jika sudah muncul seperti gambar dibawah ini kemudian ping kan dengan ip anda=192.168.40.1 hinga hasilnya akan muncul RTO(request timed out)
