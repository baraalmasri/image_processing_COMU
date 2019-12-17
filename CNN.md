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

![png](imgs/cnn1.png?raw=true)

Örneğin basit olması için sadece 1 kanal işlenecektir.
Resimin 5×5 boyutunda ve 1 ve 0 ‘lardan oluşan bir resim olduğunu varsayalım. Filtremizi 3×3 boyutunda oluşturalım.

![png](imgs/cnn2.png?raw=true)

Şimdi, filtrenin nasıl uygulandığına bir bakalım,

![png](imgs/cnn3.png?raw=true)

Öncelikle, filtre görüntünün sol üst köşesine konumlandırılır. Burada, iki matris arasında (resim ve filtre) indisler birbirisi ile çarpılır ve tüm sonuçlar toplanır, daha sonra sonucu çıktı matrisine depolanır. Ardından, bu filtreyi sağa 1 piksel (“basamak” olarak da bilinir) kadar hareket ettirip işlemi tekrarlanır. 1. Satır bittikten sonra 2 satıra geçilir ve işlemler tekrarlanır. Tüm işlemler bittikten sonra çıktı matrisi oluşturulur. Burada çıktı matrisinin 3×3 olmasının nedeni 5×5 matrisinde 3×3 filtresi yatayda ve dikeyde 3 kez hareket etmesinden kaynaklanır.
Eğer resim 6×4 ve filtre 3×3 boyutunda olsaydı çıkış matrisi 4×2 boyutunda olurdu.
Peki çıktı matrisi bize ne anlatıyor? Bu matrise genellikle Feature Map denir. Filtre tarafından temsil edilen özellikte görüntünün bulunduğu yeri gösterir. Kısacası, filtreyi görüntü üzerinden hareket ettirerek ve basit matris çarpımını kullanarak, özelliklerimizi tespit ediyoruz.
Genellikle, birden çok özelliği tespit etmek için birden fazla filtre kullanlır, yani bir Cnn ağında birden fazla konvolüsyonel (Convolutional) katman bulunur. Aşağıdaki animasyona bir göz atın, burada bu işlem biraz daha görsel olarak anlatılıyor:

![png](imgs/cnn4.GIF?raw=true)

## Bir adım daha
İlk filtreyi uyguladığımızda, bir Feature Map oluşturuyor ve bir özellik türünü tespit ediyoruz. Ardından, ikinci bir filtre kullanıp başka bir özellik türünü algılayan ikinci bir Feature Map oluştururuz.
Yukarıdaki örnekte görebildiğimiz gibi bu filtreler basit olabilir, ancak görüntüde bazı karmaşık özellikler çıkarmak istiyorsanız bu filtreler karmaşık hale gelebilirler. Daha karmaşık olan filtreleri görmek için aşağıdaki resme gözatabilirsiniz

Daha önce bahsettiğimiz, ancak ayrıntılı olarak açıklamadığımız bir başka şey, stride (büyük adım).
Bu terim genellikle padding terimi ile birlikte kullanılır. Stride, filtrenin giriş görüntüsünün etrafında nasıl evrildiğinini denetler. Yukarıdaki örnekte Stride 1 piksel idi, ancak daha büyük olabilir. Bu, Feature Map’in çıktısının boyutunu etkiler.
Cnn’nin ilk aşamalarında, ilk filtreleri uygularken, diğer Convolutional Katmanlar için mümkün olduğunca çok bilgiyi korumamız gerekir. İşte padding bu nedenden dolayı kullanılır. Feature Map’in orijinal giriş görüntüsünden daha küçük olduğunu fark etmişsinizdir. Bu nedenle Padding, (aşağıdaki resimde olduğu gibi)resmin boyutunu korumak için bu haritaya sıfır değerler katacaktır:
![png](imgs/cnn5.png?raw=true)

## Non-linearity
Tüm Convolutional katmanlarından sonra genellikle Non-Linearity(doğrusal olmayan) katmanı gellir. Peki görüntüdeki doğrusallık neden bir problemdir? Sorun şu ki, tüm katmanlar doğrusal bir fonksiyon olabildiğinden dolayı Sinir Ağı tek bir perception gibi davranır, yani sonuç, çıktıların linear kombinasyonu olarak hesaplanabilir.
Bu katman aktivasyon katmanı (Activation Layer) olarak adlandırılır çünkü aktivasyon fonksiyonlarından birini kullanılır. Geçmişte, sigmoid ve tahn gibi doğrusal olmayan fonksiyonlar kullanıldı, ancak Sinir Ağı eğitiminin hızı konusunda en iyi sonucu Rectifier(ReLu) fonksiyonu verdiği için artık bu fonksiyon kullanılmaya başlanmıştır.
ReLu Fonksiyonu f (x) = max (0, x)
ReLu fonksiyonunun Feature Map’a uygulandığında aşağıdaki gibi bir sonuç üretilir.
![png](imgs/cnn6.png?raw=true)

## Pooling Layer
Bu katman, CovNet’teki ardışık convolutional katmanları arasına sıklıkla eklenen bir katmandır. Bu katmanın görevi, gösterimin kayma boyutunu ve ağ içindeki parametreleri ve hesaplama sayısını azaltmak içindir. Bu sayede ağdaki uyumsuzluk kontrol edilmiş olur. Birçok Pooling işlemleri vardır, fakat en popüleri max pooling’dir. Yine aynı prensipte çalışan average pooling, ve L2-norm pooling algoritmalarıda vardır.
Bu işlemi şekiller üzerinden açıklayarak gidelim. Öncelikle 2×2 boyutunda bir filtre oluşturalım. Bu filtreyi aşağıdaki (4×4) resim üzerinde görebilirsiniz. Resimde gördüğünüz gibi, filtre, kapsadığı alandaki en büyük sayıyı alır. Bu sayede, sinir ağının doğru karar vermesi için için yeterli bilgiyi içeren daha küçük çıktıları kullanmış olur.
![png](imgs/cnn7.png?raw=true)
Bununla birlekte birçok kişi bu katmanı kullanmayı tercih etmez. Bunun yerine Convolutional katmanında daha büyük Stride (Filtreyi kaydırma işlemi) tercih edilir. Ayrıca variational autoencoders (VAEs) or generative adversarial networks (GANs) gibi daha üretken modellerde pooling katmanını tamen çıkartırlar.
## Flattening Layer
Bu katmanın görevi basitçe, son ve en önemli katman olan Fully Connected Layer’ın girişindeki verileri hazırlamaktır. Genel olarak, sinir ağları, giriş verilerini tek boyutlu bir diziden alır. Bu sinir ağındaki veriler ise Convolutional ve Pooling katmanından gelen matrixlerin tek boyutlu diziye çevrilmiş halidir.

![png](imgs/cnn8.png?raw=true)

## Fully-Connected Layer
Bu katman ConvNet’in son ve en önemli katmanıdır. Verileri Flattening işleminden alır ve Sinir ağı yoluyla öğrenme işlemini geçekleştirir.
Bu katman başlı başına bir derya olduğundan dolayı bu yazıdaincelenmeyecktir.

## Evrişimsel Sinir Ağlarının Mimarileri
Basit bir Cnn kurmanın yolu, birkaç Convolutional Katmanı arka arkaya koymak ve her birinden sonra ReLU katmanı eklemektir. Ve bundan sonra Pooling katmanı(ları) ve Flattening katmanı eklenmelidir.daha sonra ReLu katmanı kadar Fully-Connceted katmanı eklenir.Aklınızda bulunsun Cnn’nin en son katmanı Fully Connected katmanı olmalıdır.Örnek olarak;
```Giriş Resmi -> [[Conv -> ReLU]*N -> Pool?]*M -> Flattening -> [FC -> ReLU]*K -> FC```
şeklinde tanımlanabilir.
Bazı yaygın ConvNet isimleri;
LeNet — Bu ağ, Convolutional Networks’ün ilk başarılı uygulaması sayılır. 1990’lı yıllarda Yann LeCun tarafından geliştirildi ve posta kodlarını, basit basamakları vb. okumak için kullanıldı.
AlexNet — Bu ağ, 2012’de ImageNet ILSVRC challenge’ta sunuldu. Diğer ağlardan oldukça başarılı bir performans göstermiştir.
GoogLeNet — ILSVRC 2014’ün kazananı bu ağ olmuştur. Ağdaki parametrelerin sayısını önemli ölçüde azaltmak için avarage pooling katmanlarını kullandılar.
VGGNet — Bu ağ, ağ derinliğinin Sinir ağları için ne kadar önemli olduğunu kanıtlamıştır. 16 tane Convolutional katman bulunur.

