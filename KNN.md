```K-NN ( K-Nearest Neighbor)``` algoritması en basit ve en çok kullanılan sınıflandırma algoritmasından biridir. ```K-NN non-parametric ( parametrik olmayan )```, ```lazy ( tembel )``` bir öğrenme algoritmasıdır. lazy kavramını anlamaya çalışırsak eager learning aksine lazy learning’in bir eğitim aşaması yoktur. Eğitim verilerini öğrenmez, bunun yerine eğitim veri kümesini “ezberler”. Bir tahmin yapmak istediğimizde, tüm veri setinde en yakın komşuları arar.
Algoritmanın çalışmasında bir K değeri belirlenir. Bu K değerinin anlamı bakılacak eleman sayısıdır. Bir değer geldiğinde en yakın K kadar eleman alınarak gelen değer arasındaki uzaklık hesaplanır. Uzaklık hesaplama işleminde genelde Öklid fonksiyonu kullanılır. Öklid fonksiyonuna alternatif olarak Manhattan, Minkowski ve Hamming fonksiyonlarıda kullanılabilir. Uzaklık hesaplandıktan sonra sıralanır ve gelen değer uygun olan sınıfa atanır.
Not : Yapıcağımız örnekteki Iris veri seti kullanılmıştır. Buraya tıklayarak indirebilirsiniz.
Veri seti tanımı : Her bir çiçeğin bazı özelliklerinin ( boy, genişlik vs. ) yanı sıra her tür için 50 örnek içeren 3 iris türünü içerir.
Örnek yapağımız uygulamada veri dosyasından K-NN algoritması kullanılarak bir model oluşturup iris türü tahmini yapılacaktır.
Örneğin sonunda başarı oranını değerlendireceğiz. Confusion Matrix kavramını bilmiyorsanız buraya tıklayarak öğrenebilirsiniz.

```python
# csv dosyalarını okumak için
import pandas as pd

# csv dosyamızı okuduk.
data = pd.read_csv('Iris.csv')

# Bağımlı Değişkeni ( species) bir değişkene atadık
species = data.iloc[:,-1:].values

# Veri kümemizi test ve train şekinde bölüyoruz
from sklearn.cross_validation import train_test_split
x_train, x_test, y_train, y_test = train_test_split(data.iloc[:,1:-1],species,test_size=0.33,random_state=0)


# KNeighborsClassifier sınıfını import ettik
from sklearn.neighbors import KNeighborsClassifier

# KNeighborsClassifier sınıfından bir nesne ürettik
# n_neighbors : K değeridir. Bakılacak eleman sayısıdır. Default değeri 5'tir.
# metric : Değerler arasında uzaklık hesaplama formülüdür.
# p : Alternatif olarak p parametreside verilir. p değerini 2 vererek uzaklık hesaplama formülünü
# minkowski yerine öklid olarak değiştirebilirsiniz.
knn = KNeighborsClassifier(n_neighbors=5,metric='minkowski')

# Makineyi eğitiyoruz
knn.fit(x_train,y_train.ravel())

# Test veri kümemizi verdik ve iris türü tahmin etmesini sağladık
result = knn.predict(x_test)

# Karmaşıklık matrisi
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_test,result)
print(cm)

# Başarı Oranı
from sklearn.metrics import accuracy_score
accuracy = accuracy_score(y_test, result)
# Sonuç : 0.98
print(accuracy)
```
![png](Images/greadent descnt.png?raw=true)

16 + 18 + 15 + 1= 50 tane veri içinden 49 tanesini doğru tahmin edilirken 1 tanesi yanlış tahmin edilmiştir.
Başarı oranı 49 / 50= 0,98 ‘ dir.
##Sonuç
Hepsi bu kadar. Bu yazıda K-NN ```( K-Nearest Neighbor)``` algoritmasının ne olduğunu ve Python dili ile nasıl kodlanabileceğini öğrendiniz.
