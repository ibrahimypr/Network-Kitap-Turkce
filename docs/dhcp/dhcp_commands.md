**<span style="color:red">dhclient:</span>** Bu komut, sistemdeki bir ethernet kartına DHCP üzerinden otomatik olarak bir IP adresi almasını söyler. Örneğin, sudo dhclient eth0 komutu, eth0 adlı ağ arabirimine DHCP aracılığıyla bir IP adresi atar.


**<span style="color:red">tcpdump:</span>** Ağ paketlerini yakalamak ve analiz etmek için kullanılır. Örneğin, **<span style="color:#339511"> sudo tcpdump -i eth0 port 67 or port 68 -e -n</span>** komutu, DHCP trafiğini dinlemek için kullanılabilir.</br>
**sudo tcpdump -i eth0 port 67 or port 68 -e -n** komutu, DHCP tarafından kullanılan **UDP portları 67 veya 68**'ye giden veya bu portlardan gelen paketleri eth0 arayüzünde yakalamak için kullanılır.</br>
**-i eth0**, ağ arayüzünü belirtir (bu durumda, eth0).</br>
**port 67 or port 68**, yalnızca port 67'yi (DHCP sunucusu) veya port 68'i (DHCP istemcisi) kullanan paketleri göstermek üzere paketleri filtreler.</br>
**-e**, Ethernet başlığını içerir (MAC adreslerini içerir).
**-n**, IP adreslerinden ana bilgisayar adlarının çözülmemesini sağlar, yalnızca IP'leri görüntüler.

## Linux bir sunucyu dhcp server haline getirme

**<span style="color:red">dhcpd:</span>** Bu, bir DHCP sunucusunu başlatmak için kullanılan bir komuttur. Linux sistemlerinde, genellikle ISC DHCP sunucusu paketi olarak bulunur ve sistem yöneticileri tarafından DHCP sunucusu olarak yapılandırılabilir.
servisi başlatmak için **<span style="color:#339511">sudo systemctl start dhcpd.service</span>**, durdurmak için **<span style="color:#339511">sudo systemctl stop dhcpd.service</span>** ve otomatik başlatma ayarını yapmak için **<span style="color:#339511">sudo systemctl enable dhcpd.service</span>** komutlarını kullanabilirsiniz.

 > ISC DHCP, DHCP protokolünü kullanarak çalışan bir sunucu yazılımıdır. ISC DHCP, özellikle büyük ağlar için oldukça özelleştirilebilir ve güçlü bir DHCP sunucusu çözümüdür ve genellikle işletme ve büyük ölçekli ağ ortamlarında kullanılır.

> Linux sistemlerde, DHCP yapılandırması genellikle **<span style="color:#339511">/etc/dhcp/dhcpd.conf</span>** dosyasında yapılır. Bu dosya, ağın gereksinimlerine göre özelleştirilebilir.

> **<span style="color:#339511">sudo journalctl -u dhcpd.service</span>** komutu *DHCP* hizmetiyle ilgili günlükleri gösterecektir.


**<span style="color:blue">Linux'ta DHCP Sunucu Sorun Giderme:</span>**
DHCP sunucu sorunlarıyla karşılaştığınızda, genellikle ilk adım sunucunun durumunu kontrol etmektir. Bunun için **<span style="color:#339511">systemctl status isc-dhcp-server</span>** komutunu kullanabilirsiniz. Eğer sunucu beklenmedik şekilde durduysa veya hata veriyorsa, sorunu teşhis etmek için log dosyalarını incelemek gerekir, bu genellikle **<span style="color:#339511">/var/log/syslog</span>** içinde olur.

**<span style="color:blue">dhcpd.conf dosyasını yapılandırma:</span>**
örnek olarak IP adreslerinin sadece **"124.24.xx.xx"** ile başlayan bir aralıktan atanmasını sağlamak için, **dhcpd.conf** dosyasında bir alt ağ ve aralık belirtmelisiniz. Örneğin:

```bash
subnet 124.24.0.0 netmask 255.255.0.0 {</br>
    range 124.24.0.10 124.24.255.254;</br>
}
```
> Subnet ve netmask değerleri, ağınıza göre uyarlanmalıdır.

başka bir örnek olarak Her 5 dakikada bir IP adreslerinin yeniden atanmasını istiyorsanız, lease süresini bu süreye ayarlamalısınız.

```bash
default-lease-time 300; # Süre saniye cinsindendir, 300 saniye = 5 dakika</br>
max-lease-time 300;
```

Yapılandırmayı değiştirdikten sonra, DHCP sunucusunun yeni yapılandırmayı alması için yeniden başlatılması gerekecektir. Bu, kullanılan sistem ve DHCP sunucusunun sürümüne bağlı olarak değişir, ancak genellikle şu komutla yapılır:

```bash
sudo systemctl restart isc-dhcp-server **veya** sudo service isc-dhcp-server restart
```
**<span style="color:blue">Bir Linux Sunucusunu Dhcp sunucusu haline Getirme:</span>**</br>
DHCP Sunucusu Kurulumu:</br>
```bash
sudo apt-get install isc-dhcp-server
```
Ağ Arayüzünü Belirleme</br>
DHCP sunucusunun hangi ağ arayüzü üzerinden hizmet vereceğini belirtmeniz gerekecek. Bu ayar **<span style="color:#339511">/etc/default/isc-dhcp-server</span>** dosyasında yapılır.</br>
"INTERFACESv4" ya da "INTERFACES" satırını bulun ve DHCP sunucusunun dinlemesini istediğiniz arayüzü belirtin. Örneğin:</br>
```bash
INTERFACESv4="eth0"
```
**<span style="color:blue">DHCP Sunucusunu Yapılandırma:</span></br>**
Şimdi, DHCP sunucusunun nasıl IP adresleri dağıtacağını belirlemek için **<span style="color:#339511">/etc/dhcp/dhcpd.conf</span>**
dosyasını düzenlemeniz gerekecek.
```bash
default-lease-time 600;
max-lease-time 7200;
authoritative;

subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.10 192.168.1.100;
    option routers 192.168.1.1;
    option subnet-mask 255.255.255.0;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
}
```
Bu yapılandırmada, DHCP sunucusu 192.168.1.10 ile 192.168.1.100 arasında IP adresleri dağıtacak, ağ geçidi olarak 192.168.1.1 IP adresini belirleyecek ve Google DNS sunucularını kullanacaktır.</br>

**<span style="color:blue">DHCP Sunucusunu Başlatma:</span>**</br>
Yapılandırmayı tamamladıktan sonra, DHCP sunucusunu başlatmanız veya yeniden başlatmanız gerekecek:</br>
```bash
sudo systemctl restart isc-dhcp-server
```
Sunucunun durumunu kontrol etmek için:</br>
```bash
sudo systemctl status isc-dhcp-server
```

**<span style="color:blue">Güvenlik Duvarı Ayarları:</span>**</br>
Eğer aktif bir güvenlik duvarınız varsa, DHCP sunucusunun düzgün çalışması için **UDP port 67**'nin açık olduğundan emin olmalısınız.

## DHCP sunucusunda DHCP proxy'i aktif etme
**<span style="color:blue">dnsmasq ile DHCP Proxy Yapılandırması:</span>**</br>
```bash
sudo apt-get install dnsmasq

```
dnsmasq yapılandırma ayarlarını düzenleme
```bash
sudo vim /etc/dnsmasq.conf
```
```bash
dhcp-range=192.168.1.100,192.168.1.150,12h
```
Bu ayar, dnsmasq'ın 192.168.1.100 ile 192.168.1.150 arasındaki IP adreslerini 12 saat boyunca dağıtmasını sağlar.</br>

Yapılandırmayı tamamladıktan sonra dnsmasq servisini yeniden başlatın:
```bash
sudo systemctl restart dnsmasq
```

Bu basit yapılandırma, dnsmasq'ı bir DHCP proxy olarak kullanmanızı sağlar. Ancak, daha karmaşık veya özel ihtiyaçlarınız varsa, dnsmasq belgelerini veya kullandığınız diğer DHCP yazılımının belgelerini incelemenizi öneririm.

## DHCP sunucusunda DHCP Relay agent kullanma
```bash
sudo apt-get install isc-dhcp-relay
```

**<span style="color:blue">Yapılandırma Dosyasının Düzenlenmesi:**</span> DHCP relay agent'ı yapılandırmak için, genellikle **/etc/default/isc-dhcp-relay** dosyasını düzenlemeniz gerekmektedir. Bu dosyayı bir metin düzenleyici ile açın:
```bash
sudo vim /etc/default/isc-dhcp-relay
```
**<span style="color:blue">SERVERS:**</span> Bu, DHCP isteklerinin yönlendirileceği ana DHCP sunucusunun IP adresini belirtir. Örneğin: SERVERS="192.168.1.2"</br>
**<span style="color:blue">INTERFACES:</span>** DHCP isteklerini dinlemek için kullanılacak ağ arayüzlerini belirtir. Örneğin: INTERFACES="eth0"
</br>
Yapılandırmayı tamamladıktan sonra, DHCP relay hizmetini başlatmalı ve otomatik olarak başlatılacak şekilde etkinleştirmelisiniz
```bash
sudo systemctl start isc-dhcp-relay
sudo systemctl enable isc-dhcp-relay
```
Yapılandırmayı tamamladıktan sonra, DHCP relay hizmetini başlatmalı ve otomatik olarak başlatılacak şekilde etkinleştirmelisiniz
