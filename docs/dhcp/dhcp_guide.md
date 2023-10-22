# DHCP (Dynamic Host Configuration Protocol)

DHCP (Dynamic Host Configuration Protocol), IP ağlarındaki cihazlara otomatik olarak IP adresi ve diğer ağ yapılandırma bilgileri sağlayan bir ağ protokolüdür. DHCP, bir ağ yöneticisinin her bir cihaza manuel olarak bir IP adresi ataması gerekliliğini ortadan kaldırarak işleri büyük ölçüde basitleştirir.

Ev ortamında, DHCP (Dynamic Host Configuration Protocol) işlevi genellikle internete erişim sağlayan cihaz tarafından gerçekleştirilir; bu cihaza genellikle modem, router veya modem/router kombinasyonu adı verilir. İnternet Servis Sağlayıcınız (ISP) tarafından sağlanan bu cihaz, ağınızdaki diğer cihazların internete bağlanmasını yönetir ve her birine benzersiz bir IP adresi atar, böylece birbirleriyle ve internetle iletişim kurabilirler. DHCP'nin temel çalışma prensiplerine ve kullanımına dair bir genel bakış sağlayayım:

**<span style="color:blue">Discover:</span>** İstemci ağa bağlandığında, ağ konfigürasyonu için bir IP adresine ihtiyaç duyar.
İstemci, ağdaki DHCP sunucularını belirlemek için bir DHCP DISCOVER mesajı yayınlar (broadcast). Bu, hedef adresi "255.255.255.255" olan bir broadcast mesajdır, yani ağdaki tüm cihazlar bu paketi alır, ancak sadece DHCP sunucuları buna yanıt verir.
Bu mesaj, istemcinin kendisi için bir IP adresi talep ettiğini belirtir ancak henüz bir IP adresi ataması almamış olduğundan, kaynak IP adresi "0.0.0.0" olarak ayarlanır.

**<span style="color:blue">Offer:</span>** Ağdaki DHCP sunucular, DHCP DISCOVER mesajını alır ve uygun bir IP adresi ve lease süresi içeren bir DHCP OFFER mesajı ile yanıt verir.
Bu teklif, istemcinin kullanabileceği bir IP adresi, alt ağ maskesi, varsayılan ağ geçidi ve DNS sunucuları gibi ağ ayarlarını içerir.

**<span style="color:blue">Request:</span>** İstemci, teklif edilen IP adresini kabul ettiğini belirtmek için ağa bir DHCP REQUEST mesajı gönderir. Genellikle, birden fazla DHCP sunucusu olabileceği ve her birinin bir teklif yapabileceği durumlar için, istemci en iyi teklifi seçer ve bu teklifi yapan sunucunun adını REQUEST mesajında belirtir.
Bu aşamada, istemci hala geçici bir IP adresi kullanır çünkü teklif edilen IP adresi henüz resmi olarak atanmamıştır.

**<span style="color:blue">Acknowledgment (ACK):</span>** İstemcinin REQUEST mesajını alan DHCP sunucusu, istemciye bir DHCP ACK mesajı göndererek IP adresi atamasını onaylar.
Bu ACK mesajı, ayrıntılı ağ konfigürasyon ayarlarını içerir ve istemci bu ayarları kullanarak ağa tam olarak bağlanır.

> **Bu süreç, bir istemcinin otomatik olarak IP adresi ve ağ yapılandırma bilgileri almasını sağlar.**
 
**<span style="color:blue">DHCP Lease Time:<span>** DHCP tarafından atanmış bir IP adresi kalıcı değildir; bir "lease time" vardır. Bu süre dolduğunda, client adresi yeniden talep etmeli veya mevcut adresin lease'ini renew etmelidir. Bu, IP adreslerinin verimli kullanımını sağlar, çünkü sadece aktif devices adres tutar.

**<span style="color:blue">DHCP Renewal:</span>** Lease time yaklaşık yarısına geldiğinde, client DHCP server'a bir renewal request gönderir. Server, mevcut IP adresinin lease'ini renew eder (genellikle) ve client'a yeni bir lease time verir.

**<span style="color:blue">DHCP Reservation:</span>** Network administrators, belirli devices'ların her zaman aynı IP adresini almalarını sağlamak için DHCP reservations kullanabilir. Bu, MAC address'e dayalı olarak yapılır, böylece belirli bir MAC address her zaman belirli bir IP address ile ilişkilendirilir.

**<span style="color:blue">DHCP Options:</span>** DHCP, sadece IP addresses dağıtmakla kalmaz, aynı zamanda DNS servers, SIP servers, WINS servers, NTP servers gibi network services hakkında bilgi de dağıtabilir.

## DHCP PROXY

**<span style="color:red">DHCP Proxy Nedir?</span>** </br>
DHCP proxy, DHCP istemcisi ile DHCP sunucusu arasında yer alan bir ara katmandır. DHCP proxy'nin temel işlevi, DHCP istemci isteklerini almak, bu istekleri işlemek ve ardından bu istekleri bir DHCP sunucusuna yönlendirmektir. Bu, DHCP istemcisinin ağda doğrudan DHCP sunucusuna erişimini engeller ve bu sayede ağ yöneticileri daha fazla kontrol ve esneklik kazanır.


**<span style="color:green">Senaryo: Üniversite Kampus Ağı</span>**</br>
Bir üniversite kampüsünde, farklı binalar ve laboratuvarlar bulunmaktadır. Her bina ve laboratuvarın kendi özel IP adresi havuzu vardır. Öğrenciler, kampüsün herhangi bir yerinden internete bağlanabilirler.

**<span style="color:blue">Başlangıç:</span>** Bir öğrenci, kütüphanede çalışmak için laptopunu açar ve Wi-Fi'ye bağlanır.</br>
**<span style="color:blue">IP Talebi:</span>** Öğrencinin laptopu, IP adresi talebinde bulunur. Bu talep, kütüphanenin DHCP proxy'sine ulaşır.</br>
**<span style="color:blue">DHCP Proxy İşlemi:</span>** DHCP proxy, bu talebi alır ve kütüphaneye özgü IP adresi havuzundan bir IP adresi seçer. Ardından bu talebi ana DHCP sunucusuna yönlendirir.</br>
**<span style="color:blue">DHCP Sunucusu Yanıtı:</span>** Ana DHCP sunucusu, proxy'den gelen talebi onaylar ve gerekli ağ ayarlarını (IP adresi, alt ağ maskesi, DNS sunucuları vb.) geri gönderir.</br>
**<span style="color:blue">IP Ataması:</span>** DHCP proxy, ana DHCP sunucusundan aldığı bilgileri öğrencinin laptopuna iletir. Laptop, bu bilgileri kullanarak internete bağlanır.
Yer Değişikliği: Eğer öğrenci, kütüphaneden bir laboratuvara taşınırsa ve tekrar internete bağlanmak isterse, bu sefer laboratuvarın DHCP proxy'si devreye girer ve aynı süreç tekrar başlar.
</br></br>
Büyük ağlarda, çok sayıda DHCP istemcisinin bulunduğu yerlerde, her istemcinin DHCP sunucusuna doğrudan yayın (broadcast) mesajları göndermesi, ağ trafiğini ciddi şekilde artırabilir. DHCP proxy, bu yayın trafiğini azaltarak ağ performansını optimize eder.
Merkezi bir DHCP sunucunun varlığı, her bir ağ segmenti veya alt ağ için ayrı ayrı DHCP sunucularının kurulmasına gerek kalmadan IP adresi dağıtımını yönetebilir. Bu, kaynak kullanımını azaltır ve yönetimi kolaylaştırır.

> Bu senaryo, DHCP proxy'nin, ağdaki farklı segmentlere veya bölümlere özgü IP adresi havuzlarını yönetme yeteneğini gösteriyor. Ayrıca, öğrencinin kampüs içerisindeki hareketliliği göz önüne alındığında, DHCP proxy'nin ağ yönetimini nasıl basitleştirdiğini ve esneklik sağladığını da görebiliriz.

## DHCP Relay Agent Nedir?

DHCP agent, genellikle DHCP relay agent olarak da adlandırılır. DHCP agent'ın temel işlevi, DHCP isteklerini aynı yerel ağda olmayan bir DHCP sunucusuna yönlendirmektir. Özellikle büyük ağ yapılandırmalarında, tüm alt ağlarda ayrı ayrı DHCP sunucuları bulundurmak yerine, merkezi bir DHCP sunucusu kullanmak daha verimli olabilir. Ancak, DHCP protokolü, istemcilerin ve sunucunun aynı yayın (broadcast) domainde olmasını gerektirir. Bu nedenle, farklı bir yayın domainindeki DHCP sunucusuna istek göndermek için DHCP agent'a ihtiyaç duyulur.

DHCP agent, bir istemcinin DHCP isteğini alır, bu isteği unicast trafiği olarak değiştirir ve konfigüre edilen DHCP sunucusuna yönlendirir. DHCP sunucusu, yanıtını DHCP agent'a gönderir, ve agent bu yanıtı istemciye geri yönlendirir.

**<span style="color:green">Bir ağda neden DHCP relay agent kullanıldığına dair basit bir örnek verelim:</span>**

Bir şirketin farklı katlarda veya binalarda farklı VLAN'larda çalışan bilgisayarları (istemcileri) olduğunu düşünelim. Şirket, merkezi bir DHCP sunucusu kullanarak tüm bu VLAN'lardaki cihazlara IP adresi dağıtmak istiyor. Ancak, DHCP protokolü yayın (broadcast) mesajları kullanarak çalışır ve bu yayın mesajları genellikle yönlendiriciler veya VLAN sınırları tarafından engellenir. Yani, bir VLAN'daki istemci doğrudan farklı bir VLAN'daki DHCP sunucusuyla iletişim kuramaz.

Bu problemi çözmek için, her VLAN'da bir DHCP relay agent çalıştırılır. Bu agent, kendi VLAN'ındaki DHCP isteklerini (broadcast) alır ve bu istekleri unicast trafiği olarak merkezi DHCP sunucusuna yönlendirir. DHCP sunucusu, yanıtını bu agent'a geri gönderir, ve agent bu yanıtı ilgili istemciye yönlendirir.

Bu şekilde, merkezi bir DHCP sunucusu, farklı VLAN'larda veya ağ segmentlerindeki tüm istemcilere IP adresi dağıtabilir. Bu, IP adres yönetimini merkezileştirir ve ağ yönetimini kolaylaştırır.
![image](../img/dhcp.png)