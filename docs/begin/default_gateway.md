# Default Gateway

Default gateway, bir ağdaki diğer alt ağlara yönlendirilen veri paketlerinin geçtiği ağ cihazının IP adresidir. Default gateway, genellikle ağda bulunan bir yönlendirici (router) veya firewall cihazının IP adresini temsil eder. Bu cihaz, ağdaki diğer alt ağlara erişimi sağlar ve internet gibi harici ağlara bağlantıyı kolaylaştırır. Ev ortamında default gateway modeminiz olabilir modem IP adresi default gateway IP adresi ile aynı olabilir.

Örnek bir ağ yapılandırması düşünün: Ağdaki bilgisayarlar, tabletler ve diğer cihazlar farklı IP adresleri alır ve bu cihazlar arasında iletişim kurarlar. Ancak bu cihazlar farklı alt ağlarda yer alıyorsa, iletişim kurmak için bir yol gereklidir. İşte burada default gateway devreye girer.

**<span style="color:blue">Örneğin, bir ağda aşağıdaki cihazlar bulunsun:</span>**

Bilgisayar A: IP adresi 192.168.1.10, Alt Ağ A'da</br>
Bilgisayar B: IP adresi 192.168.2.10, Alt Ağ B'de

Bu iki bilgisayar birbirleriyle iletişim kurmak istediklerinde, default gateway devreye girer. Her iki bilgisayar da kendi alt ağları içinde yer aldıkları için, doğrudan iletişim kuramazlar. Ancak her iki bilgisayar da default gateway olarak belirtilen yönlendiriciyi kullanarak veri paketlerini birbirlerine gönderirler.

Yönlendirici (default gateway), bu veri paketlerini alır, hangi alt ağa gönderilmesi gerektiğini bilir ve veriyi doğru yolu izleyerek hedef bilgisayara ileteceği alt ağa yönlendirir. Bu sayede, farklı alt ağlardaki cihazlar arasında iletişim kurulabilir.

Default gateway, aynı zamanda bu ağdaki cihazların harici ağlara (örneğin internet) erişmesini de sağlar. Harici bir sunucuya erişim sağlanırken, cihazlar verileri default gateway üzerinden yönlendirir ve bu cihaz, verileri harici ağa iletir.

Sonuç olarak, default gateway, ağdaki farklı alt ağlar arasında iletişimi sağlayan ve harici ağlara erişimi mümkün kılan önemli bir ağ bileşenidir.

**<span style="color:blue">Bir Senaryo ile düşünecek olursak</span>**

Birinci Karakterler:

Emma: Ofis çalışanı, bilgisayar kullanıcısı
Jake: IT departmanından sorumlu çalışan
Hikaye:

Emma, ofiste bir rapor hazırlamak için bilgisayarını kullanıyordu. Raporu bitirdikten sonra, bu dosyayı e-posta yoluyla patronuna göndermeye karar verdi. Ancak e-postayı göndermeye çalıştığında, bir hata mesajı aldı. Emma, e-posta gönderme işleminin başarısız olduğunu gördü ve internete de erişemediğini fark etti.

Kısa bir süre sonra Emma, IT departmanından sorumlu Jake'i çağırdı. Jake, sorunun ne olduğunu incelemek için Emma'nın bilgisayarına geldi. Bilgisayarın ağ ayarlarını kontrol etmeye başladı. Default gateway ayarlarının yanlış olduğunu fark etti ve bu nedenle bilgisayarın internete erişemediğini belirledi.

Jake, işleri düzeltmek için hemen harekete geçti. Ofisin ana yönlendiricisinin (router) IP adresini doğru bir şekilde buldu ve Emma'nın bilgisayarının default gateway ayarını bu IP adresi olarak düzenledi. Bu basit ayar değişikliği, bilgisayarın tekrar internete erişebilmesini sağladı.