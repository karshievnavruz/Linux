## LINUX NETWORK

- Kerakli vositalarni o'rnatib olish `ipcalc`<br>
`sudo apt install ipcalc`

**1-qism. ipcalc vositasi**
- Tarmoqlar va maskalar
1. Tarmoq manzilini aniqlash:
192.167.38.54/13 manzilini ipcalc bilan aniqlash uchun quyidagi buyruqni kiritdim. <br>

![Alt text](./rasmlar/1.png "Optional Title")<br>

2. Niqobni prefiks va ikkilik shaklga aylantirish:

Niqob 255.255.255.0 ning prefiks va ikkilik ko'rinishini aniqladim. <br>

 - 255.255.255.0 ni prefiksga va ikkilik shaklga aylantirish: <br>
`ipcalc 0.0.0.0/24` <br>
 - 15 prefiksning oddiy va ikkilik shaklini ko'rish. <br>
`ipcalc 0.0.0.0/15` <br>
 - Ikkilik shaklni prefiks va normal shaklga aylantirish uchun. <br>
`ipcalc 0.0.0.0/20` <br>

![Alt text](./rasmlar/2.png "Optional Title")<br>

`ipcalc 255.255.255.0`

![Alt text](./rasmlar/3.png "Optional Title")<br>

3. Maskali 12.167.38.4 tarmog'idagi minimal va maksimal xost: /8 , 11111111.11111111.00000000.00000000 , 255.255.254.0 va /4

- Minimal va Maximal hostlar ko'rsatilgan 

![Alt text](./rasmlar/4.png "Optional Title")<br>

1. 2. localhos
- 194.34.23.100 - Yo'q. Ochiq IP manzil, localhost bilan bog'liq emas. <br>
- 127.0.0.2 - Ha. Localhost subnetida, kompyuterga mahalliy ilovalar orqali kirish mumkin. <BR>
- 127.1.0.1 - Ha. Localhost subnetida, kompyuterga mahalliy ilovalar orqali kirish mumkin. <br>
- 128.0.0.1 - Yo'q. Ochiq IP manzil, localhost bilan bog'liq emas.<br>


1. 3. Tarmoq diapazonlari va segmentlari 

1) Ochiq va shaxsiy IP manzillarni aniqlash <br>

| IP Manzil       | Holati   | Izoh                                                                       |
|------------------|----------|---------------------------------------------------------------------------|
| 10.0.0.45        | Shaxsiy  | 10.x.x.x diapazonida joylashgan, shaxsiy IP manzil.                     |
| 134.43.0.2       | Ochiq    | Ochiq IP manzil, internetga ulanish uchun mo'ljallangan.                 |
| 192.168.4.4      | Shaxsiy  | 192.168.x.x diapazonida joylashgan, shaxsiy IP manzil.                  |
| 172.0.2.1        | Ochiq    | Ochiq IP manzil, 172.16.0.0 - 172.31.255.255 diapazoniga kirmaydi.      |
| 192.176.2.2      | Ochiq    | Ochiq IP manzil, 192.168.0.0 - 192.168.255.255 diapazoniga kirmaydi.     |
| 10.10.10.10      | Shaxsiy  | 10.x.x.x diapazonida joylashgan, shaxsiy IP manzil.                     |
| 192.169.168.1    | Ochiq    | Ochiq IP manzil, 192.168.0.0 - 192.168.255.255 diapazoniga kirmaydi.     | 

IP manzillarni ushbu saytdan `https://ipinfo.io/` izladim va boshqa manbalardan ham foydalandim. 

2) 10.10.0.0/18 tarmog'i uchun IP manzillarini aniqlash

| IP Manzil       | Holati   |
|------------------|----------|
| 10.0.0.1         | Yo'q     |
| 10.10.0.2       | Mavjud   |
| 10.10.10.10      | Mavjud   |
| 10.10.100.1      | Yo'q     |
| 10.10.1.255      | Mavjud   |


## Part 2. Ikki mashina o'rtasida statik marshrutlash.
- Ikkita virtual mashinani ishga tushirdim. <br>
`ip a (ws1, ws2)`<br>
![Alt text](./rasmlar/5.png "Optional Title")<br>
![Alt text](./rasmlar/6.png "Optional Title")<br>

- Ikkala mashinada ham ichki tarmoqqa mos keladigan tarmoq interfeysini tavsiflangan va quyidagi manzillar va maskalarni o'rnatilgan ws1 - 192.168.100.10, maska ​​/16, ws2 - 172.24.116.8, maska ​​/12 <br>


![Alt text](./rasmlar/7.png "Optional Title")<br>

![Alt text](./rasmlar/8.png "Optional Title")<br>

`netplan apply`<br>

![Alt text](./rasmlar/11.png "Optional Title")<br>
![Alt text](./rasmlar/12.png "Optional Title")<br>

2. 1. Statik marshrutni qo'lda qo'shish

- ```Statik marshrutni qo'shish uchun buyruqlar, ping```<br>

![Alt text](./rasmlar/13.png "Optional Title")<br>
![Alt text](./rasmlar/14.png "Optional Title")<br>

2. 2. Statik marshrut qo'shish Saqlash

- ```O'zgartirilgan fayllar etc/netplan/00-installer-config.yaml```<br>

![Alt text](./rasmlar/15.png "Optional Title")<br>

![Alt text](./rasmlar/16.png "Optional Title")<br>
- Yana pinglandi.
![Alt text](./rasmlar/17.png "Optional Title")<br>

![Alt text](./rasmlar/18.png "Optional Title")<br>

**Part 3. Utilita iperf3**

3. 1. Ulanish tezligi

- 8 Mbps = 1 MB/s<br>
- 100 MB/s = 819200 Kbps<br>
- 1 Gbps = 1024 Mbps<br>

`sudo apt instal iperf3` yuklab olindi. <br>

![Alt text](./rasmlar/19.png "Optional Title")<br>
![Alt text](./rasmlar/20.png "Optional Title")<br>

3. 2. Utilita iperf3

- ```O'rtasidagi ulanish tezligi ws1 и ws2```<br>
![Alt text](./rasmlar/21.png "Optional Title")<br>
![Alt text](./rasmlar/22.png "Optional Title")<br>

**Part 4. Xavfsizlik devori**

4. 1. Utilita iptables

- ```Qoidalar /etc/firewall.sh```<br>

![Alt text](./rasmlar/23.png "Optional Title")<br>
![Alt text](./rasmlar/24.png "Optional Title")<br>

- ```Ikkala mashinada ham fayllarni ishga tushirish```<br>
![Alt text](./rasmlar/25.png "Optional Title")<br>
![Alt text](./rasmlar/26.png "Optional Title")<br>

- Agar avval taqiqlovchi qoida bo'lsa, u keyingi ruxsat beruvchi qoidadan ustun bo'ladi.

4. 2. Utilita nmap
 - ```Ping + nmap```<br>
<br>

![Alt text](./rasmlar/27.png "Optional Title")<br>


## 5-qism: Statik tarmoq marshrutlash

- 5. 1. Mashina manzillarini sozlash

1. Virtual mashinalaringizni ishga tushirildi: 3 ish stantsiyasi (ws11, ws21, ws22) va 2 router (r1, r2). <br>

2. Mashina konfiguratsiyasini sozlang:
/etc/netplan/00-installer-config.yaml faylini tahrirlandi. <br>

- ws11 <br>
![Alt text](./rasmlar/28.png "Optional Title")<br>

- r1 <br>
![Alt text](./rasmlar/29.png "Optional Title")<br>

- ws21 <br>
![Alt text](./rasmlar/30.png "Optional Title")<br>

- ws22 <br>
![Alt text](./rasmlar/31.png "Optional Title")<br>

- r2 <br>
![Alt text](./rasmlar/32.png "Optional Title")<br>

3. Tarmoq xizmatini qayta ishga tushirildi. <br>

- ws11 <br>
![Alt text](./rasmlar/33.png "Optional Title")<br>

- r1 <br>
![Alt text](./rasmlar/34.png "Optional Title")<br>

- ws21 <br>
![Alt text](./rasmlar/35.png "Optional Title")<br>

- ws22 <br>
![Alt text](./rasmlar/36.png "Optional Title")<br>

- r2 <br>
![Alt text](./rasmlar/37.png "Optional Title")<br>


4. Ping tstlari 

- ws22 dan ws21 ga ping qilindi: <br>
![Alt text](./rasmlar/38.png "Optional Title")<br>

- r1 dan ws11 ga ham: <br>
![Alt text](./rasmlar/39.png "Optional Title")<br>

**5. 2. IP yo'naltirishni yoqish**

`sudo sysctl -w net.ipv4.ip_forward=1` <br>
![Alt text](./rasmlar/40.png "Optional Title")<br>

![Alt text](./rasmlar/41.png "Optional Title")<br>

- /etc/sysctl.conf Faylini Tahrirlash <br>

![Alt text](./rasmlar/42.png "Optional Title")<br>
![Alt text](./rasmlar/43.png "Optional Title")<br>
![Alt text](./rasmlar/43.png "Optional Title")<br>



**5.3. Birlamchi Marshrutni Konfiguratsiya Qilish**


1. Ish stantsiyalari uchun standart marshrutni (shlyuzni) sozlash: <br>

`/etc/netplan/00-installer-config.yaml`

- ws11 <br>
![Alt text](./rasmlar/44.png "Optional Title")<br>

- ws21 <br>
![Alt text](./rasmlar/45.png "Optional Title")<br>

- ws22 <br>
![Alt text](./rasmlar/46.png "Optional Title")<br>

 -  Natijada marshrutlar ro'yxati ko'rinishi kerak <br>

![Alt text](./rasmlar/47.png "Optional Title")<br>
![Alt text](./rasmlar/48.png "Optional Title")<br>
![Alt text](./rasmlar/49.png "Optional Title")<br>


- ws11 dan r2 ga ping qilindi: <br> 
![Alt text](./rasmlar/50.png "Optional Title")<br>
![Alt text](./rasmlar/51.png "Optional Title")<br>


**5.4. Statik marshrutlarni qo'shish**

R1 va R2 routerlariga statik marshrutlarni qo'shishingiz kerak. Masalan, R1 uchun 10.20.0.0/26 tarmog'iga statik marshrut qo'shish quyidagicha bo'ladi
- netplan <br>

![Alt text](./rasmlar/52.png "Optional Title")<br>
![Alt text](./rasmlar/53.png "Optional Title")<br>


- Statik marshrutlarning kiritilganligini tekshirish uchun, R1 va R2 routerlarida quyidagi buyruqni bajaring: <br>
Bu yerda siz statik marshrutlarni ko'rishingiz kerak. Masalan, R1 uchun marshrut jadvali quyidagicha ko'rinishi mumkin: <br>

![Alt text](./rasmlar/54.png "Optional Title")<br>
![Alt text](./rasmlar/55.png "Optional Title")<br>

`ip r list 10.10.0.0/[netmask]` <br>
`ip r list 0.0.0.0/0` <br>

![Alt text](./rasmlar/56.png "Optional Title")<br>


- 0.0.0.0/0 marshrut — bu standart marshrut bo'lib, barcha noma'lum yo'nalishlar uchun ishlatiladi. <br>
 - 10.10.0.0/[netmask] marshrut — bu ma'lum bir tarmoq uchun ishlatiladigan marshrut. Agar manzil ma'lum bir tarmoqqa tegishli bo'lsa, tizim ushbu marshrutdan foydalanadi. <br>

 - Bu marshrut aniqroq (spesifik) bo'lganligi sababli, tizim avval ushbu marshrutdan foydalanadi. Standart marshrut esa (0.0.0.0/0) faqat hech qanday boshqa mos marshrut topilmaganda ishlatiladi. <br>
**5.5 Router ro'yxatini tuzish**
 - R1-da tcpdump ishga tushiring<br>
 - ws dan ws21 ga traceroute buyrug'i<br>
 `traceroute 10.20.0.10` <br>
 ![Alt text](./rasmlar/58.png "Optional Title")<br>
  ![Alt text](./rasmlar/57.png "Optional Title")<br>


 **Traceroute yordam dasturi** ICMP so'rovining o'rniga maqsadli xostning ma'lum bir portiga 3 ta UDP paket yuboradi va ushbu portning mavjud emasligi haqida javobni kutadi. Birinchi paket TTL=1 bilan yuboriladi, ikkinchisi TTL=2 bilan va shu tarzda davom etadi, to so'rov manzilga yetib borguncha. ICMP so'rovi o'rniga UDP so'rovi yuborilgani sababli, har bir so'rovda jo'natuvchi va qabul qiluvchining portlari mavjud bo'ladi. Standart bo'yicha, so'rov 34434 yopiq portga yuboriladi. So'rov maqsadli xostga yetib borganida, bu xost «Destination port unreachable» (manzil porti mavjud emas) xabarini jo'natadi. Bu esa so'rov qabul qiluvchi tomonidan olinganini bildiradi. Traceroute ushbu javobni kuzatuv jarayonining tugaganligini bildiruvchi sifatida qabul qiladi.<br>

**5.6. Marshrutlashda ICMP protokolidan foydalanish**

 Birinchi navbatda, R1 marshrutizatorida tcpdump yordamida ICMP trafigini yozib olindi.. Bu bizga ping buyruqining chiqishini kuzatishga imkon beradi. <br>

 - Ping va tcpdump natijalari: <br>
  ![Alt text](./rasmlar/59.png "Optional Title")<br>
  ![Alt text](./rasmlar/60.png "Optional Title")<br>


 **6-qism. DHCP yordamida dinamik IP konfiguratsiyasi**

 - /etc/dhcp/dhcpd.conf: <br>
  ![Alt text](./rasmlar/61.png "Optional Title")<br>
- /etc/resolv.conf filini tahrirlash. resolv.conf faylida DNS-server sifatida 8.8.8.8 ko'rsatildi. Bu DNS-server Google'ga tegishli bo'lib, keng tarqalgan global DNS-server hisoblanadi. <br>
   ![Alt text](./rasmlar/62.png "Optional Title")<br>
 - DHCP xizmatini qayta ishga tushirish uchun quyidagi buyruqni ishlatish: <br>
   ![Alt text](./rasmlar/63.png "Optional Title")<br>

- Ws21-ni qayta yuklash va terminalda ip a ni tekshirish <br>
   ![Alt text](./rasmlar/71.png "Optional Title")<br>
- ws22 dan 21 ga ping yuborish <br>
   ![Alt text](./rasmlar/72.png "Optional Title")<br>

- ws11 uchun MAC manzili qo'shilgan `/etc/netplan/00-installer-config.yaml` faylining mazmuni: <br>
   ![Alt text](./rasmlar/73.png "Optional Title")<br>

- R1 uchun MAC manziliga mustahkam bog'langan shunga o'xshash sozlama<br>
- `/etc/dhcp/dhcpd.conf`<br>
   ![Alt text](./rasmlar/74.png "Optional Title")<br>
   - DNS:<br>
      ![Alt text](./rasmlar/75.png "Optional Title")<br>

   - ws21: <br>
      ![Alt text](./rasmlar/77.png "Optional Title")<br>

- Ushbu buyruqlar `dhclient` yordamida tarmoq interfeysini boshqarish uchun ishlatiladi. <br>
      ![Alt text](./rasmlar/78.png "Optional Title")<br>


**7-qism. NAT**

- Apache2 Serverini Konfiguratsiya Qilish<br>
1. Fayl ochilgandan so'ng, Listen 80 qatorini Listen 0.0.0.0:80 ga o'zgartirildi<br>
      ![Alt text](./rasmlar/79.png "Optional Title")<br>
      ![Alt text](./rasmlar/81.png "Optional Title")<br>

- Apache Veb-Serverini Ishga Tushirish
      ![Alt text](./rasmlar/82.png "Optional Title")<br>
      ![Alt text](./rasmlar/83.png "Optional Title")<br>

      - r2-da Xavfsizlik Devori Qoidalarini O'rnatish
      [Alt text](./rasmlar/84.png "Optional Title")<br>
[Alt text](./rasmlar/85.png "Optional Title")<br>


- ping yuborish <br>
      ![Alt text](./rasmlar/86.png "Optional Title")<br>
      ![Alt text](./rasmlar/87.png "Optional Title")<br>

      - ICMP Protokoli Paketlarini Marshrutlashga Ruxsat Berish, SNAT va DNAT Qo'shish<br>

      ![Alt text](./rasmlar/89.png "Optional Title")<br>

- TCP Ulanishlarini Tekshirish <br>
1. ws22 dan r1 ga SNAT orqali TCP ulanishini tekshirish: <br>
      ![Alt text](./rasmlar/90.png "Optional Title")<br>

2. r1 dan ws22 ga DNAT orqali TCP ulanishini tekshirish: <br>
      ![Alt text](./rasmlar/91.png "Optional Title")<br>
**8-qism. SSH tunnellariga kirish**
- Apapche veb-serverini ws22-da faqat localhost-da ishga tushiring (ya'ni /etc/apache2/ports.conf faylida qatorni Listen 80ga o'zgartirildi Listen localhost:80)<br>
      ![Alt text](./rasmlar/92.png "Optional Title")<br>
- ws21-dan ws22-da veb-serverga kirish uchun ws21-dan ws22-ga mahalliy TCP yo'nalishidan foydalanildi <br>
      ![Alt text](./rasmlar/93.png "Optional Title")<br>
      - telnet 127.0.0.1 [local port]
            ![Alt text](./rasmlar/94.png "Optional Title")<br>

