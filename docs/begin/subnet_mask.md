# Subnet Mask (Alt Ağ Maskesi)

Subnet mask, bir IP adresinin hangi kısmının ağ adresi için, hangi kısmının ise cihaz adresi için kullanıldığını belirtir. IP adresleri, ağ içindeki her cihaz için benzersiz tanımlayıcılar olduğundan, bir ağdaki cihazların doğru bir şekilde iletişim kurabilmesi için bu ayrımın yapılması gereklidir.

**<span style="color:blue">IP Adresi ve Subnet Mask Birlikte Nasıl Çalışır:</span>**
 "1" olan bitler ağ adresini, "0" olan bitler ise cihazın adresini temsil eder. Örneğin, 192.168.1.100 IP adresi ve 255.255.255.0 alt ağ maskesi kullanılıyorsa, bu, IP adresinin ilk üç bölümünün ağ adresini ve sonuncu bölümünün cihazın adresini tanımladığını gösterir. Yani, bu ağın alt ağındaki cihazlar 192.168.1.x şeklinde olur. Burada alt ağ maskesinin ilk 3 bloğu 255 ve son bloğu 0 olduğu için 255 olan bloklar aynı ağda tamamen aynı ip adresine sahip sadece son blok değişebilir. Örnek olarak:
 192.168.1.4,
 192.168.1.254

alt ağ maskeleri farklı uzunluklarda (farklı "1" ve "0" bit dizileri) olabilir. Örnek :</br>
255.255.255.0: Alt ağdaki cihazların son bölümü cihaz adresini tanımlar.</br>
255.255.0.0: Alt ağdaki cihazların son iki bölümü cihaz adresini tanımlar.</br>
255.255.255.192: Alt ağdaki cihazların son iki biti cihaz adresini tanımlar.

**<span style="color:blue">Şimdi, alt ağ maskelerinin ağ adresleri ve cihaz adresleri arasında nasıl bir ayrım yaptığını daha iyi anlayabilmek için bunu biraz daha detaylandıralım:</span>**

255.255.255.0: Bu alt ağ maskesi en yaygın kullanılanlardandır. Burada ilk üç grup (255.255.255) ağ adresini temsil ederken, son grup (0) cihaz adresini temsil eder. Bu durumda, aynı ağ içerisinde 254 adet cihaz barındırabiliriz, çünkü cihaz adresi için kullanılabilecek sayılar 1'den 254'e kadardır (0 ağın kendisi ve 255 yayın adresi için ayrılmıştır).

255.255.0.0: Bu maskede ilk iki grup (255.255) ağ adresini, son iki grup (0.0) ise cihaz adresini temsil eder. Bu, çok daha büyük bir ağ olup, binlerce cihaza (teorik olarak 65,534) ev sahipliği yapabilir.

255.0.0.0: Bu durumda, sadece ilk grup ağ adresini temsil eder ve geri kalanı cihaz adresleri için kullanılır. Bu, milyonlarca cihazı (16,777,214) destekleyebilen devasa bir ağı ifade eder.

Alt ağ maskesi yapılandırması çok daha detaylı bir konudur buna ileride değineceğiz.