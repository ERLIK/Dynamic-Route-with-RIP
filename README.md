![dynamic_routing](https://user-images.githubusercontent.com/102908626/201543750-5176c400-cc0b-4c37-a877-f409b5a175ea.png)


# Dynamic-Routing
Cisco Packet Tracer'da <b>RIP</b> protokolü ile <b>Dynamic Routing</b> Yapılandırması.

Yönlendirme, veri paketinin kaynak sistemden hedef sisteme aktarılmasıdır. Bu işlemi ağ iletişim kurallarını kullanarak, ağlar arasından veri paketi iletimini sağlayan Yönlendirici (Router) yapar.

Router üzeride tuttuğu <b>Routing Table</b> sayesinde çeşitli algoritmalar ile verilein aktarılmasına olanak sağlar. Yönlendirma algoritmaları bu tablo sayesinde paketler üzerinde işlem gerçekleştirebilirler.

Routerların zaten temelde olan iki görevi, kaynak ve hedef arasındaki en uygun yolu belirtmek ve veriyi bu yol üzerinden hedef cihaza göndermek. 

Router'ın içerisinde <b>"Static"</b> ve <b>"Dynamic"</b> olmak üzere iki adet tablo bulunmakta. Bu tabloları açıklamak gerekirse;

<h3>Static Routing Table;</h3>
  Ağ içerisindeki bütün subnetleri, el ile konfigüre edilmesi <b>Static Routing</b> yapısıdır. Bu durum ağ içerisinde bir değişiklik sırasında taboda olan tüm statik değerlerin silinmesi demektir, böyle bir durumda yapıyı tekrar yapılandırmak gerekecektir. Yani kısaca bir router'dan diğer routere gitmek için yol belirlenen yol önceden belirlenmiştir. Trafiğin değişmesi durumunda kendisini yinelemez.
  
  Küçük ölçekli networkler için uygun olabilir, çünkü router daha az işlem kullanacaktır, döngü oluşma riski yoktur, basit ve güncelleme gerektirmez. Ancak bazı zamanlarda belirli noktalarda oluşacak tıkanıklıklar durumunda trafiği farklı routerlere yönlendirilemediği için network'ünüzün kalitesi düşecektir ve hatların kopması durumunda trafik farklı yollara yönlendirilemediği için bağlantı kaybı yaşanabilir.
  
<h3>Dynamic Routing Table;</h3>
  Dynamic routing table zaman içinde, ağ topolojisinde, trafiğe ya da bağlantılarda meydana gelen değişimlerde kendini güncelleyecektir. Ağ üzerinden meydana gelen değişimlerde, geliştirici kurum ya da personel olmamasına rağmen kendi alternatif yollarını üretecektir.
  
  Gelişmiş ağlarda trafik yükü ile birlikte belirli noktalarda sıkışıklık yapmaması ya da hatta olabilecek kopukluklara çözüm üretmek için alternatif yollar bulması sayesinde ağ kalitesini arttırır. Routing protocols kullanılabilir ve tüm yollar öğrenilir ve en iyi yolu routing table'ye yerleştirir, geçerli olmayan yolları kaldırır.
  
<h5>RIP Dynamic Routing</h5>
  <b>RIP (Routing Information Protocol)</b>: Bir TCP/IP ağındaki router’ların birbirini otomatik olarak tanımasında kullanılan bir iç yönlendirme protokoldür. RIP routing, RFC 1058'de tanımlanmıştır. Routerların routing tablosunu aktif bağlantısından 30 saniyede bir gönderir ve hop count tutar. Bu değer maksimum 15 olabilir.
  
<h3>Dynamic Routing Configuration</h3>
  Farklı networklerdeki 8 adet bilgisayar ve 1 adet sunucuyu birbirleri ile konuşturmak için bir kaç yol var. Statik ya da dinamik olanı seçebiliriz RIP için bu ön hazırlık laboratuarını tasarlamak gerekirse;
  
![a1](https://user-images.githubusercontent.com/102908626/201548097-923060b0-1de2-4698-ad50-0b56a1e52e46.png)
![a2](https://user-images.githubusercontent.com/102908626/201548127-1d57930b-2731-4b60-b2b5-8f4b2f087fbf.png)

Kısaca tüm cihazları birbirlerine bağlayıyoruz (Switc - Router, Router, Router).

  Sırada RIP protokolünün devreye girmesinde. Cisco Packet Tracer üzerindeki tüm routerlerda RIP protokolü yüklü bir şekilde geliyor. RIP'in yaptığı iş ise bir routerin kendisine bağlı networkleri diğer routerlara söylemesi oluyor. Bu haberleşmeyi resimle anlatmak gerekirse;
  
  
![a5](https://user-images.githubusercontent.com/102908626/201550431-db54d723-6da6-4beb-8325-cc6abd1b3a35.jpeg)

Görüldüğü üzere bir router diğerine hangi ağa bağlı olduğu söyleyebiliyor. Bu sayede paket bir routere geldiğinde direkt olarak sıradaki hedefini routerdan öğrenebiliyor. Bu konfigürasyonu yapmak için;

<b>Router>en<br>
Router#conf t<br>
Enter configuration commands, one per line.  End with CNTL/Z.<br>
Router(config-router)#<br></b>

Artık seçtiği router'ın rip konfigürasyon interfacesindeyim. Tek yapmanız gereken o routerın bağlı olduğu networkleri rip protokolüne sormak. Paylaştığım pkt doyasındaki <b>"Router Z"</b>'yi ele alırsak;

<b>Router>en<br>
Router#conf t<br>
Router(config)#router rip<br>
Router(config-router)#network 21.0.0.0<br>
Router(config-router)#network 19.0.0.0<br>
Router(config-router)#network 22.0.0.0<br>
Router(config-router)#network 20.0.0.0<br>
Router(config-router)#network 14.0.0.0<br></b>

Artık bir paketin otomatik bir şekilde hedefe gittiğini tespit edebiliriz. Denemek için Router A'dan Server 0'a ping atıyorum...

Router>ping 14.0.0.10

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 14.0.0.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/1 ms

Tüm routerlarıma bu konfigürasyonları sizler için yaptım. Herhangi bir routerı ya da yolunu silmenizde bile paket bağlantı olduğu sürece iletişime devam edecektir.

Herkere iyi çalışmalar...

ERLIK
