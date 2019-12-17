## Convolutional Neural Network (ConvNet yada CNN) nedir, nasıl çalışır?

### Evrişimsel Sinir Ağlarının Yapısı
Konuştuğumuz işlevselliği elde etmek için, Cnn görüntüyü çeşitli katmanlarla işler.
Bu katmanları yazının bir sonraki bölümünde ayrıntılı olarak inceleyeceğiz ancak şu an sadece bu katmanlara ve 
amaçlarına genel bir bakış yapalım:
  - **Convolutional Layer**  Özellikleri saptamak için kullanılır
  - **Non-Linearity Layer** Sisteme doğrusal olmayanlığın (non-linearity) tanıtılması
  - **Pooling (Downsampling) Layer** Ağırlık sayısını azaltır ve uygunluğu kontrol eder
  - **Flattening Layer** Klasik Sinir Ağı için verileri hazırlar
  - **Fully-Connected Layer**  Sınıflamada kullanılan Standart Sinir Ağı
  
  
  Temel olarak, Cnn, sınıflandırma sorununun çözümü için standart Sinir Ağı kullanır,
  ancak bilgileri belirlemek ve bazı özellikleri tespit etmek için diğer katmanları kullanır.
Haydi her katmanın ve işlevlerinin detaylarına dalalım.

**Convolutional Layer**

Bu katman CNN’nin ana yapı taşıdır. Resmin özelliklerini algılamaktan sorumludur. Bu katman, görüntüdeki düşük ve yüksek seviyeli özellikleri çıkarmak için resme bazı fitreler uygular. Örneğin, bu filtre kenarları algılayacak bir filtre olabilir. Bu filtreler genellikle çok boyutludur ve piksel değerleri içerirler.(5x5x3) 5 matrisin yükseklik ve genişliğini, 3 matrisin derinliğini temsil eder.
Şimdi mu filtrenin nasıl uygulandığına bakalım;


Örneğin basit olması için sadece 1 kanal işlenecektir.
Resimin 5×5 boyutunda ve 1 ve 0 ‘lardan oluşan bir resim olduğunu varsayalım. Filtremizi 3×3 boyutunda oluşturalım.

Şimdi, filtrenin nasıl uygulandığına bir bakalım,



Öncelikle, filtre görüntünün sol üst köşesine konumlandırılır. Burada, iki matris arasında (resim ve filtre) indisler birbirisi ile çarpılır ve tüm sonuçlar toplanır, daha sonra sonucu çıktı matrisine depolanır. Ardından, bu filtreyi sağa 1 piksel (“basamak” olarak da bilinir) kadar hareket ettirip işlemi tekrarlanır. 1. Satır bittikten sonra 2 satıra geçilir ve işlemler tekrarlanır. Tüm işlemler bittikten sonra çıktı matrisi oluşturulur. Burada çıktı matrisinin 3×3 olmasının nedeni 5×5 matrisinde 3×3 filtresi yatayda ve dikeyde 3 kez hareket etmesinden kaynaklanır.
Eğer resim 6×4 ve filtre 3×3 boyutunda olsaydı çıkış matrisi 4×2 boyutunda olurdu.
Peki çıktı matrisi bize ne anlatıyor? Bu matrise genellikle Feature Map denir. Filtre tarafından temsil edilen özellikte görüntünün bulunduğu yeri gösterir. Kısacası, filtreyi görüntü üzerinden hareket ettirerek ve basit matris çarpımını kullanarak, özelliklerimizi tespit ediyoruz.
Genellikle, birden çok özelliği tespit etmek için birden fazla filtre kullanlır, yani bir Cnn ağında birden fazla konvolüsyonel (Convolutional) katman bulunur. Aşağıdaki animasyona bir göz atın, burada bu işlem biraz daha görsel olarak anlatılıyor:
