
## K-Means Algoritması
``` K-Means ``` algoritması bir unsupervised learning ve kümeleme algoritmasıdır. 
K-Means’ teki K değeri küme sayısını belirler ve bu değeri parametre olarak alması gerekir. Bu durum aslında bir dezavantajdır.
K değerini kendi hepsalayan X-Means adında başka bir algoritmada vardır. Algoritmanın basit bir çalışma şekli vardır.
K değeri belirlendikten sonra algoritmada rastgele K tane merkez noktası seçer.
Her veri ile rastgele belirlenen merkez noktaları arasındaki uzaklığı hesaplayarak veriyi en yakın merkez noktasına göre bir kümeye atar.
 
Daha sonra her küme için yeniden bir merkez noktası seçilir ve yeni merkez noktalarına göre kümeleme işlemi yapılır.
Bu durum sistem kararlı hale gelene kadar devam eder.
K-Means algoritmasındaki başlangıç merkez noktalarının rastgele atanması sorunlara yol açabilmektedir.
Başlangıç noktalarını daha iyi seçebilmek için 2007 yılında David Arthur ve Sergei Vassilvitskii K-Means algoritmasının
bir varyasyonu olan K-Means++ algoritmasını geliştirilmiştir. K-Means++’a göre rastgele başlangıç noktası seçildikten sonra 
diğer tüm veriler ile arasındaki mesafe hesaplanır. 
Bu mesafenin karesi alınıp belli hesaplamalar yaparak yeni başlangıç noktaları seçilir. Bu işlemin kamaşıklık analizi O(log k)’dır.
```python
# csv dosyalarını okumak için
import pandas as pd

# csv dosyamızı okuduk.
data = pd.read_csv('Iris.csv')

# Veriler
v = data.iloc[:,1:-1].values

# KMeans sınıfını import ettik
from sklearn.cluster import KMeans

# KMeans sınıfından bir nesne ürettik
# n_clusters = Ayıracağımız küme sayısı
# init = Başlangıç noktalarının belirlenmesi
km = KMeans(n_clusters=3, init='k-means++',random_state=0)

# Kümeleme işlemi yap
km.fit(v)

# Tahmin işlemi yapıyoruz.
predict = km.predict(v)

# Küme merkez noktaları
# [[5.9016129  2.7483871  4.39354839 1.43387097]
#  [5.006      3.418      1.464      0.244     ]
#  [6.85       3.07368421 5.74210526 2.07105263]]
print(km.cluster_centers_)

# Grafik şeklinde ekrana basmak için
import matplotlib.pyplot as plt
plt.scatter(v[predict==0,0],v[predict==0,1],s=50,color='red')
plt.scatter(v[predict==1,0],v[predict==1,1],s=50,color='blue')
plt.scatter(v[predict==2,0],v[predict==2,1],s=50,color='green')
plt.title('K-Means Iris Dataset')
plt.show()
```
![gif](imgs/kmeans.gif?raw=true)
