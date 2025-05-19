# PANDAS

## GİRİŞ

- Pandas, veri biliminde çok kullanılan, veri biliminin ‘tablo işlemcisi’ olarak bilinen bir Python kütüphanesidir.

- Anaconda ile yüklemek için `conda install pandas` kodunu, pip ile yüklemek için `pip install pandas` çalıştırın.

- Bu defterde Pandas ile ilgili doyurucu bilgiler bulunsa da, defter Pandas ile yapılabileceklerin tamâmını kapsamamaktadır.

- Yazar : Mehmet Akif SOLAK

## Temel Yapıtaşı Seriler

- ‘numPy’ dizisine benzeyen; lâkin daha esnek olan bir veri yapısıdır.

- Farklı tip verileri barındırabilir.

- Barındırdığı verilere sıra numarası (indeks) atayan (bununla sınırlı değil) bir veri tipidir.

- Atanan sıra numarası bir etiket de olabilir; yanî sözlük gibi de çalışabiliyor.

- Serîler ‘etiketli liste’ gibi çalışan yapılardır.

#### 1) Seri oluşturma

- Sözlükle seri oluşturulabilir; bu durumda etiketler sıra numarasının yerine geçer. Serî oluştururken `dtype` parametresi yerine `numpy`'daki gibi veri tipi verilebilir:
  
  ```python
  sozluk = {"gider" :  123, "gelir" : 442, "satışGeliri" : 0,
          "elektronikGideri" : 23}
  seri = pandas.Series(sozluk, dtype='int16')
  print(seri)
  # Çıktı:
  # gider               123
  # gelir               442
  # satışGeliri           0
  # elektronikGideri     23
  # dtype: int16
  ```

- Listelerle seri oluşturulabilir; `Series()` fonksiyonuna sadece tek bir liste verilirse sıra numaraları sıfırdan başlanarak atanır. Eğer veriyle etiketler ayrı listeler hâlinde verilebilir. Karışıklık olmaması açısından parametre isminin yazılması daha iyi olur, fakat parametre ismi yazılmayacaksa ilk parametre veri, ikinci parametre indis olarak değerlendirilir:
  
  ```python
  veri = [123, 442, 0, 23]
  indeks = ["gider", "gelir", "satışGeliri", "elektronikGideri"]
  seri = pandas.Series(data = veri, index=indeks)
  seri = pandas.Series(data, indeks)# Yukarıdaki ile aynı işlem
  print(seri)# YUkarıdaki örnekle aynı sonucu verir
  ```

#### 2) Verilere Erişim

- Serîlere hem sıra numarasıyla, hem de anahtar kelîmeyle (eğer atandıysa) ile erişilebilir:
  
  ```python
  seri["gider"]# 123        -> indis ile erişme
  seri.iat[0]# 123          -> Sıra numarasıyla erişme
  seri.loc["gider"]#123     -> İndis ile erişme
  seri.iloc[0]# 123         -> Sıra numarasıyla erişme
  ```

- `at` ve `iat` özellikleriyle sadece münferid bir elemana erişilebilir; fakat `loc` ve `iloc` özelliklerini kullanarak veyâ doğrudan indisle erişimi kullanarak birden fazla eleman seçilebilir:
  
  ```python
  secilecekler = ["gider", "elektronikGideri"]
  seri.loc[secilecekler]
  secilen = seri.iloc[[0, 3]]
  print(secilen)
  # Çıktı
  # gider               123
  # elektronikGideri     23
  # dtype: int64
  ```

- **Yukarıdaki kodda seçilecek elemanların liste olarak verildiğine dikkat edin!**

#### 3) Serî Elemanları Üzerinde Değişiklik

- Serîye eleman ekleme ve serîdeki elemanın değerini değiştirme aynı kod yazım şekliyle yazılır; eğer serîde ‘anahtar’ anahtarıyla bir veri yoksa yeni veri eklenir; varsa var olan veri değiştirilir:
  
  ```python
  veri = [123, 442, 0, 23]
  indeks = ["gider", "gelir", "satışGeliri", "elektronikGideri"]
  seri = pandas.Series(data = veri, index=indeks)
  
  seri["mutfakGideri"] =  23
  seri["gider"] = seri["gider"] + seri["mutfakGideri"]
  print(seri)
  # Çıktı
  # gider                  146
  # gelir                  442
  # satışGeliri              0
  # elektronikGideri        23
  # mutfakGideri            23
  # dtype: int64
  ```

#### 4) Serîlerde İşleç Kullanımı, İki Serîyi 4 İşleme Sokma

- Eğer seriler `+` işleciyle toplanırlarsa, bu durumda her iki seride de anahtar kelimesi ortak olan elemanlar toplanır; diğerlerinin değerine ‘not a number’ (`NaN`) değeri atanır. Eğer anahtar kelimeleri yoksa sıra numaralarına göre toplanır. Eğer yalnızca bir serinin sıra numarası varsa bu durumda bütün elemanların değeri `NaN` yapılır. Eğer sıra numaraları eşit değilse, küçük olan sıra numarasına kadar toplama işlemi yapılır; diğerleri `NaN` yapılır.

- Benzer şekilde çıkarma (`-`), çarpma (`*`), bölme (`/`) ve mod (`%`) alma işlemleri de yapılabilir. Veri tipleri tamsayı olan iki seri toplanırsa veya çıkarılırsa veya bölünürse veya modu alınırsa veri tipi noktalı sayı olur. Çarpılırsa veri tipi değişmez. Eğer ikisinden birinin veri tipi noktalı sayıysa çarpım durumunda da veri tipi de noktalı sayı olur. Eğer liste elemanları tabi tutmak istediğimiz işlemi desteklemiyorsa hata verir; Python’da karakter katarı (yazı, yani `str`) tipiyle tamsayının çarpılabildiğini unutmayalım. Elemanları eşleşen iki seride bir yazı değişkeni bir tamsayıyla çarpılırsa o elemanın tipi yine `object`olur; ama tamsayı çarpımıyla çarpılan elemanlardan üretilen elemanın tipi tamsayı (`int`) olur.

- Emsal kullanım:
  
  ```python
  sinav1 = pandas.Series({"Ahmed" : 98, "Mehmed" : 98, "İrfân" : 95})
  sinav2 = pandas.Series({"Ahmed" : 94, "Mehmed" : 88, "İrfân" : 84})
  ortalamalar = (sinav1 + sinav2) / 2
  print(ortalamalar)
  # Çıktı
  # Ahmed     96.0
  # Mehmed    93.0
  # İrfân     89.5
  # dtype: float64
  ```

#### 5) Serî Uygulamaları

- `seri = seri.replace(eskiDeger, yeniDeger)` ile serîdeki eski değerler, yenisiyle değiştirilebilir.

- `seri.tolist()` ile serî Python listesi tipine çevrilebilir.

- `seri.index` ile serînin sıra numaralarına erişilebilir.

- `seri.index.to_numpy()` ile serînin sıra numaraları numPy dizisi olarak alınabilir.

- `seri.unique()` ile serîdeki değerler münferid (tekil) olarak alınabilir.

- `seri.nunique()` ile serîdeki münferid değerlerin sayısı öğrenilebilir.

- `seri.sort_values(series, ascending = True, inplace = False)` ile serî içerisindeki veriler küçükten büyüğe doğru sıralanır. Eğer büyükten küçüğe doğru sıralama yapmak istiyorsak, `ascending` parametresine `False` vermeliyiz. Eğer değişikliklerin asıl serî nesnesine yansıtılmasını istiyorsak, `inplace` parametresine `True` değerini vermeliyiz.

- `seri.apply(fonksiyon)` : Verilen fonksiyon verilere uygulanır.

- `seri.idxmin()` ve `seri.idxmax()` ile serînin en düşük değerli elemanının indeksi ve en yüksek değerli elemanının indeksi alınabilir.

- `seri.nsmallest(n = 5)` : Serî içerisindeki en küçük `n` adet değeri serî olarak döndürür; `n` parametresinin varsayılan değeri 5'tir.

- `seri.nlargest(n = 5)` : Serî içerisindeki en büyük `n` adet değeri serî olarak döndürür; `n` parametresinin varsayılan değeri 5'tir.

- `seri.sample(n = 1)` : Serî içerisinden `n` adet rastgele değer döndürür.

- `seri.isin(values)` : Serî içerisinde `values` listesindeki elemanların olup, olmadığını sorgular; bu durumu belli eden `bool` değişkenlerden oluşan bir serî döndürür:
  
  ```py
  seri = pandas.Series([123, 23, 53], dtype='int8')
  print(seri.isin([123]))
  # 0     True
  # 1    False
  # 2    False
  # dtype: bool
  
  # Birden fazla değer için sorgulama yapılabilir,
  # Bu durumda verilen değerlerden birisini barındıran eleman için
  # True değeri yazılan bir serî döndürülür:
  print(seri.isin([123, 23]))
  # 0     True
  # 1     True
  # 2    False
  # dtype: bool
  
  # Bu, sorgulama yapmak için kullanılabilir:
  print(l[l.isin([123, 53])])
  # 0     123
  # 1      53
  # dtype: int8
  ```

- `isnull()` ile serî içerisindeki `None` olmayan elemanlar öğrenilebilir. Bu metod da `isin()` metodu gibi çalışır. Bunun tersi `notnull()` metodu da vardır.

- `seri.between(left, right, inclusive = 'both')` : Serî içerisinde, 'left' ve 'right' arasında yer alan değerlerin tespit edilmesi için kullanılır. Bu değerleri getirmek yerine bu aralıktaki değerlerin bulunduğu indise `True` yazılmış bir serî getilir. `inclusive` parametresi `left` ve `right` değerlerinin bu değer aralığına dâhil olup, olmadığını ifâde etmek için kullanılır; varsayılan olarak bu değerler de ilgili aralığa dâhildir. `inclusive` parametresi 'both', 'neither', 'left' ve 'right' değerlerini alabilir. Bunlar sırasıyla, 'ikisi de dâhil', 'ikisi de dâhil değil', 'sol dâhil' ve 'sağ dâhil' anlamlarına gelir. Misal:
  
  ```py
  seri = pandas.Series([123, 23, 53], dtype='int8')
  print(seri.between(23, 53))
  # 0    False
  # 1     True
  # 2     True
  # dtype: bool
  ```

- `seri.duplicated(keep='first')` metoduyla serî içinde hangi değerlerin tekrâr ettiği öğrenilebilir. Bu metot,  tekrar eden ikinci ve sonraki değerlerin bulundukları indislerde `True` yazan bir serî döndürür. `keep` parametresiyle hangi elemanın ikinci sayılacağı değiştirilebilir. Eğer `keep='last'` değeri verilirse, tekrar eden değere sâhip son eleman için `False` yazar; ondan öncekiler için `True` yazar. Bu metod tekrar eden değerleri filtrelemek için kullanılır:
  
  ```py
  seri = pandas.Series([123, 53, 53], dtype='int8')
  print(seri.duplicated())
  # 0    False
  # 1    False
  # 2     True
  # dtype: bool
  
  print(seri.duplicated(keep='last'))
  # 0    False
  # 1     True
  # 2    False
  # dtype: bool
  
  print(seri[seri.duplicated(keep='last')])
  # 1    53
  # dtype: int8
  #Son eleman kalsın dediğimiz için ilk elemanı tekrar eden eleman saydı
  
  # Tersini almak için list comprehensive yapısı kullanılabilir:
  print(seri[[not i for i in l.duplicated(keep='last').tolist()]])
  # 0    123
  # 2     53
  # dtype: int8
  ```

- `seri.drop_duplicates(keep='first')` : Yukarıdaki kodun yaptığını yapar; serînin tekrar eden verilerinin silinmiş hâlini döndürür. Tekrar eden verilerden hangisinin tutulacağı `keep` parametresiyle belirlenir; `first` değeri için ilk elemanı tutar, sonrakileri siler, `last` değeri için son elemanı tutar, diğerlerini siler.

- ..

## Serîlerin Birleşmiş Hâli : DataFrame (Veri Çerçevesi, Tablo)

- Serilerin yan yana gelmiş hali gibidir. Yani matris formundadır. Satırlar, satır numaraları, sütunlar ve sütun numaraları vardır; buradaki numara kavramı yine `Series`'te olduğu gibi anahtar kelime olarak da çalışabilir.

#### 1) Veri Çerçevesi Oluşturma

- Veri çerçevesi oluşturmak için serîler, numPy dizileri, diziler, matrisler veyâ başka veri çerçeveleri kullanılabilir:
  
  ```python
  # NumPy dizisi ile:
  veri = pandas.DataFrame(veri, satırIsimleri, sutunIsimleri)
  # Yukarıdaki kodun parametre ismi yazılmış hâli:
  veri = pandas.DataFrame(data = veri,
                      index = satırİsimleri, columns = sutunİsimleri)
  ```

- İndekse isim atamak için `veri.rename_axis('indeksIsmi', axis = 1)` yazılır.

- Emsal kullanım:
  
  ```python
  sutunlar = ["Matematik", "Yazılım"]
  veri = [{"Matematik" : 81, "Yazılım" : 98},
         {"Matematik" : 78, "Yazılım" : 86},
         {"Matematik" : 98, "Yazılım" : 95}]
  isimler = ["Ahmed", "Fâruk", "Necîp"]
  veri = pandas.DataFrame(data = veri, index = isimler,
          columns = sutunlar)
  print(veri)
  # Çıktı:
  #        Matematik  Yazılım
  # Ahmed         81       98
  # Fâruk         78       86
  # Necîp         98       95
  ```

#### 2) Verilere Erişim

- Verilere erişim serîlerde olduğu gibidir; birkaç farklılıkları vardır.

- Bir sütundaki verilerin tamamına şu şekilde erişilebilir: `veri['sutunIsmi']`
  Eğer sütunlara isim verilmemişse bu şekilde erişemeyiz.

- Birden fazla sütundaki verilerin tamamına şu şekilde erişilebilir:
  `veri[["sutunIsmi1", "sutunIsmi2"]]`

- Eğer bir sütun veri olarak çekilirse geriye 'Series' tipinde bir değer döner; eğer birden fazla sütun çekilirse 'DataFrame’ tipinde bir değer döndürülür.

- Satır verisine erişmek için `loc` özelliği kullanılabilir : `veri.loc["satırIsmi"]`
  Eğer satırlara isim verilmemişse bu şekilde erişemeyiz.

- Bir satırdaki veriye şu şekilde de erişilebilir :` veri.iloc[sıraNumarasi]`
  Burada 'sıraNumarasi' liste numaralandırması gibi kullanabilir, bu sayede ilk 5 satır, son üç satır gibi belirli satırdaki veriler çekilebilir

- Belli bir satırın belli sütununa erişirken dizi gibi erişilebilir:
  `veri[sıraNumarası]["sutunIsmi"]`

- Herhangi bir satıra koşulla erişilebilir : `veri[veri.isim == 'deger’]`
  ('veri’ çerçevesinin 'isim’ adlı sütununun değeri 'deger’ olan satırlar istendi).

- Eğer sütunlara isim verdiysek ve sütunlara sıra numarasıyla erişmek istiyorsak şu kodu doldurabiliriz : `veri.iloc[:,sutunSıraNumarasi]`
  Burada farklı sıra numaraları vererek istediğimiz sütunları çekebiliriz; satır numaralarında da aynı işlemleri yapabiliriz.

- Eğer birden fazla satırı ismiyle çekmek istiyorsak şu kodu doldurmalıyız:
  `veri.loc[["isim1", "isim2"]]`

- Eğer bir değere sadece sıra numarasıyla ulaşmak istiyorsan şu kod doldurumalı:
  `veri.iat[satirNo, sutunNo]`

#### 3) Sütun Ekleme

- Bu işlem serîlerdeki gibidir : `veri[yeniSutun] = yeniVeri`
  Aynı serilerde olduğu gibi eğer 'yeniSutunIsmi' isminde bir sütun yoksa yeni bir sütun eklenir. 'yeniSutunVerisi' değişkeninin tipi liste ('list') de olabilir.
  Eğer en sona yeni bir sütun eklemek istiyorsak şu şekilde eklenebilir::
  `veri[len(veri)]  = yeniSutunVerisi`

#### 4) Sütun Silme

- Sütun ismiyle sütun silme : `veri.drop('sutunIsmi', axis = 1, inplace = True)`

- Sütun numarasıyla : `veri.drop([sıraNumarası], axis = 1, inplace = True)`

- **!** Buradaki 'axis' girdisi ekseni belirtiyor; eğer sütun silmek istiyorsak 1 numaralı ekseni seçmeliyiz. 'inplace' girdisi ise yapılan değişikliğin 'veri' değişkenine kaydedilip – kaydedilmeyeceğini belirtiyor. Varsayılan değeri 'False'dur.

- Eğer sütun ismi verildiyse ve sütun numarasıyla sütun silinmek isteniyorsa şu şekilde silinebilir:
  `veri.drop(veri.iloc[0].columns[sutunNumarasi], axis=1, inplace = True)`

- Sütun sıra numaralarıyla oynanarak belirli sütunlar silinebilir.

#### 5) Satır Silme

- Sütun silme işleminden tek farkı `drop()` fonksiyonu girdisinde `axis = 0` olarak belirtilmesidir; `axis` girdisinin varsayılan değeri 0 olduğundan yazılmayabilir.

#### 6) Satır Ekleme

- Liste veya sözlük biçimindeki bir veriyle yeni satır eklenebilir. Eğer sözlük biçiminde olursa anahtar kelimelerin sütun isimleriyle aynı olması gerekir ve bu şekilde daha münasiptir; liste şeklinde olursa doğru sırada yazılmalıdır.

- Son satıra yeni veri ekleme : `veri.loc[len(veri)] = yeniSatirVerisi`

> ***NOT :*** `loc` özelliğiyle vâr olan bir indekse eriştiğimizde o satırdaki verinin değiştirileceğine, yanî yeni verinin eskisinin yerini alacağına dikkat ediniz!

- Pandas'ın yeni sürümünde `append()` fonksiyonuyla da yeni satır eklenebilir:..

#### 7) Sıra numaralarıyla, indekslerle oynama

- Yeni bir anahtar sıra numarası atamak istiyorsak öncelikle bunu veri çerçevimize sütun şeklinde eklemeliyiz; ardından şu kodu doldurmalıyız:
  `veri.set_index('yeniSutununIsmi', inplace = True)`

##### 7.1) Çoklu İndeks ('MultiIndex')

- Bir başlığın altında birden fazla açılmış başlık gibi anahtarlarımızı bir anahtar çatısında birleştirebiliriz.

###### 7.1.1) Çoklu indeks oluşturma:

- Bir demet ('tuple') içerisinde çoklu anahtarlar sıralanıp, ve oradan `MultiIndex`'e çevrilebilir:
  
  ```python
  siniflar = ["B sınıfı", "B sınıfı", "B sınıfı",
              "C sınıfı", "C sınıfı", "D sınıfı"]
  motorlar = [1.0, 1.1, 1.2, 1.3, 1.4, 2.0]
  # Bunları bir demet haline getirelim:
  anahtarSira = list(zip(siniflar, motorlar))
  # 'MultiIndex'in 'from_tuples(..)' fonksiyonuyla
  # çoklu anahtar sıra numarasını üretelim:
  cokluIndeks = pa.MultiIndex.from_tuples(anahtarSira)
  veriler = [["Panda Benzin", "Fiat"],
            ["", ""], ["Berlingo Dizel", "Cıtroen"],
            ["Linea Dizel", "Fiat"], ["Linea Benzin", "Fiat"],
            ["Passat Dizel", "Volkswagen",]]
  # Bu örnek Volkswagen ve Cıtroen'i reklam amacı taşımamaktadır.
  # Bilhassa Uygur bölgesinde de fabrikası olan VW masum değildir
  
  veri = pandas.DataFrame(data = veriler, index = cokluIndeks,
         columns = ["Model", "Marka"])
  print(veri)
  # Çıktı:
  #                        Model       Marka
  # B sınıfı 1.0    Panda Benzin        Fiat
  #          1.1                            
  # C sınıfı 1.6  Berlingo Dizel     Cıtroen
  #          1.3     Linea Dizel        Fiat
  #          1.4    Linea Benzin        Fiat
  # D sınıfı 2.0    Passat Dizel  Volkswagen
  ```

###### 7.1.2) Çoklu indekse erişme

- Eğer ilk anahtarla erişirsek o anahtarın altındaki tüm satırlar gelir:
  
  ```python
  print(veri.loc["B sınıfı"])
  # Çıktı:
  #             Model Marka
  # 1.0  Panda Benzin  Fiat
  # 1.1                    
  ```

- Eğer özel anahtarıyla bir satırı getirtmek istiyorsan genel anahtardan sonra virgül koyup özel anahtarı yazmalısın : `veri.loc["B sınıfı", 1.0]`

- Şu şekilde de erişilebilir : `veri.loc["B sınıfı"].loc[1.0]`

###### 7.1.3) Çoklu indeksi silme

- Eğer üst anahtarla silme işlemi yaparsak o anahtarın altındaki tüm satırlar silinir:
  
  ```python
  print(veri.drop(("B sınıfı")))
  # Çıktı:
  #                        Model       Marka
  # C sınıfı 1.6  Berlingo Dizel     Cıtroen
  #          1.3     Linea Dizel        Fiat
  #          1.4    Linea Benzin        Fiat
  # D sınıfı 2.0    Passat Dizel  Volkswagen
  ```

- Eğer özel bir anahtarla bir satırı silmek istiyorsak o zaman anahtar kısmına anahtarları '(genelAnahtar', ozelAnahtar)' şeklinde vermeliyiz:
  
  ```python
  veri.drop(("B sınıfı", 1.1), inplace = True)
  print(veri)
  # Çıktı:
  #                        Model       Marka
  # B sınıfı 1.0    Panda Benzin        Fiat
  # C sınıfı 1.6  Berlingo Dizel     Cıtroen
  #          1.3     Linea Dizel        Fiat
  #          1.4    Linea Benzin        Fiat
  # D sınıfı 2.0    Passat Dizel  Volkswagen
  ```

> ***NOT :*** Çoklu indeksli tabloda indeks vererek silme işlemi yaparken indeksin bir demet (`tuple`) şeklinde verildiğine dikkat ediniz!

> ***NOT :*** Yaptığımız işlemlerin tabloda kalıcı olmasını istiyorsak `inplace` parametresine `True` vermeyi unutmamalıyız!

#### 8) Kullanışlı Bâzı İşlemler

##### 8.1) Filtreleme

- Serîlerde olduğu gibi şart kontrol işlemleri yapılabilir:
  
  ```python
  sart = veri > 4
  sartlıveri = veri[sart]
  ```

- Yukarıdaki kod tablodaki verilerin 4'ten büyük olanların alındığı, 4'ten küçük olanların ise `NaN` olarak alındığı bir işlemi gösteriyor.

> ***NOT :*** Eğer bütün veriler tamsayı değilse hata verir!

##### 8.2) Boş verilerle ilgilenme

- Boş verileri doldurmak için `fillna()` yöntemi kullanılabilir:
  
  ```python
  veri.fillna(2, inplace = True)# Boş verilerle 2 sayısıyla doldurulur
  ```

- Boş verileri silmek için `dropna()` yöntemi kullanılır. Bu yöntem varsayılan olarak içerisinde bir tâne bile boş veri bulunduran tüm satırları siler. Bunu değiştirmek için `thresh` parametresi kullanılır. `axis` parametresine `1` değeri verilerek işlemin sütun bazında yapılması sağlanabilir. Yapılan işlemin mevcut `DataFrame`'e uygulanması için `inplace = True` parametresi verilmelidir:
  
  ```python
  sutunlar = ["Matematik", "Türkçe", "Yazılım"]
  veri = [{"Matematik" : 81, "Yazılım" : 98},
         {"Matematik" : 78, "Yazılım" : 86},
         {"Matematik" : 98},
         {}]
  isimler = ["Ahmed", "Fâruk", "Necîp", "Zafer"]
  veri = pandas.DataFrame(data = veri, index = isimler,
          columns = sutunlar)
  print(veri)
  # Çıktı:
  #        Matematik  Türkçe  Yazılım
  # Ahmed       81.0     NaN     98.0
  # Fâruk       78.0     NaN     86.0
  # Necîp       98.0     NaN      NaN
  # Zafer        NaN     NaN      NaN
  # Aşağıdaki kodlardan sadece biri çalıştırıldığında oluşan
  # etki yanında yazmaktadır (peş peşe çalıştırıldığında değil!):
  veri.dropna()# Her satırda boş veri olduğunda tüm veriyi siler
  veri.dropna(thresh = 2)# 2+ sayıda dolu hücresi olan satırları silmez
  # Sütun bazında silme:
  veri.dropna(axis = 1)# Boş satırı olan tüm sütunları siler
  veri.dropna(axis = 1, thresh = 2)# 2+ hücresi dolu olanları silmez
  veri.dropna(axis=1, thresh=1)# En az 1 hücresi dolu olan sütunu silmez
  ```

- Boş verileri doldurmakla ilgili örnek:
  
  ```python
  hava = {"Ağrı" : {"Prş" : 12, "Cuma" : 14, "Cmt" : nm.nan},
         "Of" : {"Prş" : 21, "Cuma" : 22, "Cmt" : 24},
         "Konya" : {"Prş" : 23, "Cuma" : nm.nan, "Cmt" : nm.nan},
         "Bursa" : {"Prş" : 26, "Cuma" : 29, "Cmt" : nm.nan}}
  veri = pandas.DataFrame(hava)
  print(veri)
  # Çıktı:
  #          Ağrı     Of     Konya     Bursa
  # Prş      12.0     21     23.0       26.0
  # Cuma     14.0     22      NaN       29.0
  # Cmt       NaN     24      NaN        NaN
  veri.fillna(veri.mean().mean(), inplace = True)
  # Yukarıdaki kod boş hücreleri tüm tablonun ortalamasıyla doldurur
  veri.fillna(veri.mean().mean(), limit=1)
  # Yukarıdaki kod sadece her sütunun ilk boş hücresini ort ile doldurur
  # Aşağıdaki kod ise her sütunu (ili) kendi ortalamasıyla doldurur:
  for il in veri:
      veri[il].fillna(veri[il].mean(), inplace = True)
  print(veri)
  # Çıktı:
  #       Ağrı  Of  Konya  Bursa
  # Prş   12.0  21   23.0   26.0
  # Cuma  14.0  22   23.0   29.0
  # Cmt   13.0  24   23.0   27.5
  ```

##### 8.3) İndeksleri sıfırlama

- `veri.reset_index()` fonksiyonuyla sıra numaraları sıfırlanır ve gerçekten sıra numarası atanır; eğer daha önce satır isimleri vardıysa bunlar yeni üretilen 'index' ismindeki sütuna taşınır; o isimde bir sütun varsa bu yeni sütunun ismi 'level_0' yapılır; o isimde de bir sütun varsa hata verir.

##### 8.4) Veri çerçevelerini birleştirme

- Bunun için Pandas'ın `concat()` yöntemi kullanılır:
  
  ```python
  gruplandirilmisVeri = pa.concat([veri, veri2])
  ```

- `concat()` fonksiyonu içerisine verdiğimiz listenin elemanları seri ('Series') ya da veri çerçevesi ('DataFrame') olabilir. Üretilen 'gruplandirilmisVeri' 'DataFrameGroupBy' sınıfından bir değişkendir. Bu değişkenin özelliklerinden faydalanarak çeşitli işlemler yapılabilir.

##### 8.5) Veri çerçevelerini kaynaştırma

- Bir veri çerçevesinde verilerin bazı özellikleri, başka bir veri çerçevesinde aynı verilerin farklı özellikleri olabilir. Bunları birleştirmek için `pandas.merge()` yöntemi kullanılır. Bu işlemi yaparken hangi sütuna göre verilerin kaynaştırılmasını istediğimizi `on` parametresiyle belirtmeliyiz:
  
  ```python
  yeniVeri = pa.merge(veri, veri2, on = 'ortakSutun')
  ```

- 'veri' ve 'veri2' çerçevelerindeki ortak veriler yeni tabloda yer alır; birisinde olup, diğerinde olmayan veriler yer almaz. Bu, varsayılan olarak böyledir; istersek değiştirebiliriz. Bunun için fonksiyon girdisinden olan 'how' girdisinin değerini 'outer' yapmalıyız. Buraya 'left', 'right' değerleri de verebilir ve veritabanında kullanılan join tipleri uygulanabilir. İlgili ayar birisinden olup, diğerinde olmayan sütunları alacak şekilde ayarlanırsa bir çerçevede olup, diğerinde olmayan verilerin olduğu yere `NaN` yazılır.

##### 8.6) İndeksi İsimlendirme

- İndeksi isimlendirmek için, `DataFrame` nesnesinin `index` özelliği kullanılır:
  
  ```py
  veri.index.name = "isim"
  ```

##### 8.7) Sıralama

- Sıralama, serîlerdekine benzerdir; fakat farklı olarak birden fazla sütuna göre sıralama yapılabilir:
  
  ```py
  sutunlar = ["Matematik", "Yazılım"]
  veri = [{"Matematik" : 81, "Yazılım" : 98},
         {"Matematik" : 91, "Yazılım" : 98},
         {"Matematik" : 98}]
  isimler = ["Fâruk", "Ahmed", "Necîp"]
  veri = pandas.DataFrame(data = veri, index = isimler,
          columns = sutunlar)
  veri.index.name = 'öğrenci'# İndeksi isimlendiriyoruz
  
  # Sıralama örnekleri:
  veri.sort_values('Yazılım')# Tek sütuna göre sıralama
  #          Matematik  Yazılım
  # Fâruk           81     98.0
  # Ahmed           91     98.0
  # Necîp           98      NaN
  veri.sort_values(['Yazılım', 'öğrenci'])# Birden fazla sütuna göre..
  #          Matematik  Yazılım
  # Ahmed           91     98.0
  # Fâruk           81     98.0
  # Necîp           98      NaN
  ```

- Yukarıdaki örnekte görüleceği üzere, ilk verilen sütuna göre veriler sıralanır; sonra sıralamanın yapıldığı sütundaki verisi aynı olan veriler, ikinci verilen sütuna göre sıralanır ve 'Ahmed' ismi 'Fâruk' isminden alfabetik olarak önce geldiğinden ilk sıraya alınır.

- Sıralamanın kalıcı olması için `inplace` parametresine `True` değeri verilmeli.

- Verileri bir sütuna göre artan sırada sıraladıktan sonra, diğer sütuna göre azalan sırada sıralamak istersek, `ascending` parametresine uygun değerleri vermeliyiz:
  
  ```py
  veri.sort_values(['Yazılım', 'öğrenci'],
                  ascending = [False, True])
  # Matematikten en düşük not alan öğrencileri alfabetik sırada sıralar
  ```

##### 8.8) Gruplandırma

- Verileri gruplandırarak, üzerlerinde pek çok işlem yapmayı kolay hâle getiren `groupby()` metodu SQL dilindeki `GROUP BY` yapısına benzemektedir.
- Bu, gruplandırılmış verileri bir `DataFrame` olarak döndürmez; bunun sebebi, gruplandırılmış veriler üzerinde kolayca işlem yapabilmek içindir:
  
  ```py
  # Öğrencilerin hangi dersi aldıklarını gösteren bir tablomuz olursa;
  sutunlar = ["Matematik", "Yazılım", "Siyâset"]
  veri = [{"Matematik" : True, "Yazılım" : True},
         {"Matematik" : False, "Yazılım" : True, "Siyâset" : False},
         {"Matematik" : False, "Yazılım" : True, "Siyâset" : True}]
  isimler = ["Fâruk", "Ahmed", "Necîp"]
  veri = pandas.DataFrame(data = veri, index = isimler,
          columns = sutunlar, dtype='bool')
  veri.index.name = 'öğrenci'# İndeksi isimlendiriyoruz
  
  # Derse göre gruplama yapılabilir:
  mat = veri.groupby('Matematik')
  print(mat.size())
  # Matematik
  # False    2
  # True     1
  # dtype: int64
  # İki kişi Matematik dersini almamış
  # 'mat' nesnesi üzerinden 'agg()' metoduyla toplam
  # ('aggregate') fonksiyonları uygulanabilir
  # İstatistiksel değerler median(), mean()
  # gibi metotlarla öğrenilebilir
  ```
- ..

#### 9) Verileri İçe ve Dışa Aktarma

- 'xls', 'xlsx' gibi tablo işlemci (Excel, Calc) çıktısı türünden verilerinizi, 'csv' formatındaki verilerinizi Pandas ile içe `DataFrame` nesnesi olarak aktarabilirsiniz:
  
  ```py
  df = pandas.read_csv('csvDosyaIsmi.csv')
  df = pandas.read_excel('xlsDosyaIsmi.csv')
  ```

- Verileri dışa aktarırken `to_csv()`, `to_excel()`, `to_json()`, `to_html()`, `to_markdown()`, `to_xml()` metotları kullanılabilir.

- ..

#### 10) DataFrame Hakkında Diğer Bilgiler

- `value_counts(sutunIsmi)` ile verilen sütunda hangi değerden kaç adet olduğunu sorgulayabilirsiniz.

- `idxmax(axis=0)` : Her sütun için en yüksek veriye sâhip satırın indeksini serî biçiminde getirir; eğer `axis = 1` yapılırsa, her satır için en yüksek veriye sâhip sütunun indeksini (ismini) serî şeklinde getirir:
  
  ```py
  # Yukarıdaki öğrenci - not verisi üzerinden gidersek;
  print(veri.idxmax())
  # Matematik    Necîp
  # Yazılım      Fâruk
  # dtype: object
  
  # Yukarıdaki sonuç Matematikten en yüksek notu Necip'in aldığını,
  # yazılımdan en yüksek notu Fâruk'un aldığını gösteriyor.
  # Aslında Ahmed'in 'Yazılım' notu ile Fâruk'un 'Yazılım' notu aynı;
  # fakat veri sıralamasında Fâruk önce yer aldığından Fâruk getirildi.
  
  print(veri.idxmax(axis = 1))
  # öğrenci
  # Fâruk      Yazılım
  # Ahmed      Yazılım
  # Necîp    Matematik
  # dtype: object
  
  # Yukarıdaki sonuca göre;
  # Fâruk en yüksek notunu 'Yazılım'dan
  # Ahmed en yüksek notunu 'Yazılım'dan
  # Necip ise 'Matematik'ten almış
  ```

- `idxmin(axis = 0)` : `idxmax()` ile benzer biçimde kullanılır; farkı en düşük veri indeksini getirir.

- `query(str)` metoduyla veri içerisinden sorgu yapar gibi başka verileri getirtebiliriz:
  
  ```py
  # Yukarıdaki öğrenci verisi üzerinden gidecek olursak;
  veri.query('Yazılım>90')# 'Yazılım'dan 90+ puan alanlar getirilir
  
  # Birden fazla sorgu & (ve), | (veyâ) işleçleriyle birleştirilebilir:
  veri.query('Yazılım>90 & Matematik > 90')
  
  # '&' işleci yerine 'and', '|' işleci yerine 'or' yazılabilir:
  veri.query('Yazılım>90 and Matematik > 90')
  ```

- ..
