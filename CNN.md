## Convolutional Neural Network (ConvNet yada CNN) nedir, nasıl çalışır?

### Evrişimsel Sinir Ağlarının Yapısı
Konuştuğumuz işlevselliği elde etmek için, Cnn görüntüyü çeşitli katmanlarla işler.
Bu katmanları yazının bir sonraki bölümünde ayrıntılı olarak inceleyeceğiz ancak şu an sadece bu katmanlara ve 
amaçlarına genel bir bakış yapalım:
  - ** Convolutional Layer ** Özellikleri saptamak için kullanılır
  - ** Non-Linearity Layer ** Sisteme doğrusal olmayanlığın (non-linearity) tanıtılması
  - ** Pooling (Downsampling) Layer ** Ağırlık sayısını azaltır ve uygunluğu kontrol eder
  - ** Flattening Layer ** Klasik Sinir Ağı için verileri hazırlar
  - ** Fully-Connected Layer **  Sınıflamada kullanılan Standart Sinir Ağı
  
  
  Temel olarak, Cnn, sınıflandırma sorununun çözümü için standart Sinir Ağı kullanır,
  ancak bilgileri belirlemek ve bazı özellikleri tespit etmek için diğer katmanları kullanır.
Haydi her katmanın ve işlevlerinin detaylarına dalalım.

**Convolutional Layer**

Bu katman CNN’nin ana yapı taşıdır. Resmin özelliklerini algılamaktan sorumludur. Bu katman, görüntüdeki düşük ve yüksek seviyeli özellikleri çıkarmak için resme bazı fitreler uygular. Örneğin, bu filtre kenarları algılayacak bir filtre olabilir. Bu filtreler genellikle çok boyutludur ve piksel değerleri içerirler.(5x5x3) 5 matrisin yükseklik ve genişliğini, 3 matrisin derinliğini temsil eder.
Şimdi mu filtrenin nasıl uygulandığına bakalım;
