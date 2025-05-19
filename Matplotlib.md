# MATPLOTLIB

## GENEL BİLGİLER

- Matplotlib, Python ile veri biliminde yoğun şekilde kullanılan veri görselleştirme kütüphânesidir.

- Açık kaynak kodlu ve ücretsiz bir kütüphânedir.

- Matplotlib'in alt kitâplıkları vardır. Bilhassa veri biliminde, en çok kullanılan kitâplık `matplotlib.pyplot` kitâplığıdır. Bu defterde `pyplot` anlatılmaktadır.

- `pip install matplotlib` veyâ `conda install matplotlib` kodunu komut ekranında çalıştırarak Matplotlib kitâplığını kurabilirsiniz.

- Hâzırladığınız grafiği görüntülemek için `pyplot`'ın `show()` fonksiyonunu kullanabilirsiniz; eğer Jupyter notebook içerisinde çalışıyorsanız Jupyter notebook'ta `%matplotlib inline` komutunu çalıştırırsanız, grafiği görüntülemek için `show()` fonksiyonunu kullanmanız gerekmez; benzer kolaylıklar diğer platformlarda da var

- Bu kitâplığın hızlı kullanım gibi sebeplerle çok farklı kullanımları, kısayolları vardır.

- Bu defterde daha çok veri biliminde analiz için kullanılan temel seviye işlemler anlatılmaktadır; eğer matplotlib'i profesyonel seviyede kullanmak istiyor ve çok farklı grafikler çizdirmek istiyorsanız şu adresi ziyâret edebilirsiniz:
  [https://curbal.com/1-dataset-100-matplotlib-visualizations](https://curbal.com/1-dataset-100-matplotlib-visualizations)

- Yazar : Mehmet Akif SOLAK

## PYPLOT TEMEL KULLANIM

- Verilerin görselleştirilmesi için genellikle (x, y) koordinat düzlemi kullanılır.

- `pyplot` kitâplığı verilerin görselleştirilmesi için `figure` sınıfını kullanır. Bu sınıf görüntüyü ifâde eden temel sınıftır.

- `figure` sınıfı satır ve sütunlardan oluşur. Her hücrede bir koordinat düzlemi çizdirebilirsiniz.

- Her koordinat düzlemi ekseni ifâde eden `axis` sınıfından bir nesne barındırır.

- En basitiyle, bir koordinat düzlemi çizdirmek için `plot()` fonksiyonu kullanılır:
  
  ```py
  import matplotlib.pyplot as plotter
  xVals = [1990, 2001, 2014, 2022]
  yVals = [344, 566, 13553, 16544]
  plotter.plot(xVals, yVals, "green")
  # plot(xDegerleri, yDegerleri, renkIsmiVeyaRenkKodu)
  # Renk ismi yerine renk kodu da yazılabilir:
  plotter.plot(xVals, yVals, "#34A4A4")
  ```

- Sık kullanılan renkler için renk ismini uzun uzun yazmak yerine kısa kodunu yazabilirsiniz.
  `"g"` -> yeşil, `"y"` -> sarı, `"red"` -> kırmızı, `"k"` -> siyah, `"m"` -> kırmızımsı mor, `"w"` -> beyaz

- Sık kullanılan renk isimleri şunlar:
  
  blue -> mavi, orange -> turuncu, green -> yeşil, purple -> mor, pink -> pembe, gray -> gri, olive -> sarı, cyan -> turkuaz, brown -> kahverengi

- Daha fazla renk için ilgili rengin CSS'deki ismini veyâ renk kodunu yazabilirsiniz.

#### Kısa Kodlama İle Grafiği Özelleştirme

- Üçünü parametrede renk ismini yazmak yerine kısa kodlamayı yazabiliriz. Kısa kodlama, renk ismi + deseni içeren kodlama biçimidir. Sık kullanılan renk isimlerinin baş harfi ve sonrasında desen belirtilebilir:
  
  ```py
  plotter(xVals, yVals, "g-*")
  # Üçüncü parametrede ilk önce renk isminin kısa ismini,
  # sonra grafik desenini belirttik. Buna göre;
  # veri noktalarında yıldız olur, grafik aralıksız çizgi biçiminde olur
  ```

- Bâzı veri çizim desenleri şu şekildedir:
  
  `"g--"` : Grafik aralıklı çizgi biçiminde çizilir, veri noktaları işâretlenmez
  `"b-."` : Grafik düz çizgi biçiminde çizilir, veri noktaları nokta ile işâretlenir
  `"ro"` : Grafikte çizgi yoktur, veri noktaları kırmızı renkli büyük daire ile işâretlenir
  `"c-o"` : Grafik turkuaz rengindedir; veri noktaları büyük dâire ile işâretlenir
  `"b--o"` : Grafik aralık çizgi biçiminde çizilir, veri noktaları büyük dâireyle işâretlenir
  `"c^"` : Grafikte çizgi yoktur, veri noktaları şapka işâretiyle (`^`) işâretlenir
  `r-|` : Grafik çizgi biçiminde, veri noktaları dik çizgiyle işâretlenmiş..

#### Birden Fazla Denklem Grafiğini ekleme

- Aynı grafik üzerinde birden fazla (x, y) ikilisinin değerini göstermek istiyorsak, basitçe her bir (x, y) ikilisini peş peşe verebiliriz:
  
  ```py
  import numpy as nm
  otherXVals = nm.linspace(0, 30, 17)
  otherYVals = otherXVals ** 2
  plotter.plot(xVals, yVals, "g--", otherXVals, otherYVals, "b-o")
  # Daha fazlasını da aynı şekilde peş peşe ekleyebiliriz
  ```

#### Eksenleri ve Grafiği İsimlendirme

- Bunun için `xlabel()` ve `ylabel()` fonksiyonları, başlık için ise `title()` kullanılır:
  
  ```py
  plotter.xlabel("X ekseni veri ismi")
  plotter.ylabel("Y ekseni veri ismi")
  plotter.title("Grafik başlığı")
  ```

#### Sözlük İçerisindeki Veriyi Yazdırma

- `plot()` yönteminin `data` parametresine sözlük (`dict` nesnesi) verdiğinizde sözlük anahtar kelîmelerini yazarak grafiği çizdirebilirsiniz.

#### Birden Fazla Grafiği Tek Resim Üzerinde Gösterme

- Bunun için `subplot()` yöntemi kullanılır. Burada görselin kaç satır, kaç sütun olduğu ve üçüncü parametre olarak şu an hangisinin belirtildiği yazılır; ardından çağrılan `plot()` yöntemi o hücre için grafiği belirtir:
  
  ```py
  plotter.subplot(1, 2, 1)# 1 satır, 2 sütun, birincisini belirtiyorum
  plotter.plot(xVals, yVals, "g--")
  plotter.xlabel("1. veri x ekseni")
  plotter.ylabel("1. veri y ekseni")
  plotter.subplot(1, 2, 2)# 1 satır, 2 sütun, ikincisini belirtiyorum
  plotter.plot(otherXVals, otherYVals, "r-o")
  plotter.xlabel("2. veri x ekseni")
  plotter.ylabel("2. veri y ekseni")
  plotter.tight_layout()# Grafiklerin birbirine geçmesini önlemek için
  ```

## PLOT() FONKSİYONUNUN PARAMETRELERİ

- Temel yazımı:
  
  ```py
  Axes.plot(*args, scalex=True, scaley=True, data=None, **kwargs)
  ```

- Buradaki `args` parametreleri x ekseni verisi, y ekseni verisi ve kısayol ifâdelerinden oluşan eksen verileridir.

- `scalex` ve `scaley` parametreleri ölçeklemeyle alâkalıdır.

- `data` parametresi ise, verinin sütunlarına doğrudan isim yazılarak erişilmesini sağlayan parametredir.

- isimli parametreler `kwargs` sözlüğüyle verilebilir. En çok kullanılanlardan bâzıları:
  
  `linewidth` veyâ `lw` : çizgi kalınlığıdır, tamsayı verilir
  
  `linestyle` veyâ `ls` : Çizgi şeklidir, öntanımlı çizgi biçim değerleri metîn olarak verilebilir. Bunlar "dashed" (aralıklı çizgi), "solid" (düz normal çizgi), "dotted" (nokta nokta biçiminde ilerleyen çizgi), "-", "--", "-.", ":" gibi değerlerdir.
  
  `label` : Etiket değeri, metîn olarak
  
  `color` veyâ `c` : Renk, metîn olarak (ön tanımlı kısa renk ismi, ön tanımlı renk ismi, CSS renk ismi veyâ 16'lık renk kodu olabilir)
  
  `marker` : Veri noktaları üzerinde oluşturulması istenen işâret, ön tanımlı değerlerden biri, metîn olarak; bunlara yukarıda değinilmişti ('o', '.', ':' gibi). Path veyâ MarkerStyle nesnesi de verilebilir
  
  `markersize` veyâ `ms` : İşâretleyici
  
  `markeredgecolor` veyâ `mec` : İşâretleyici kenar rengi
  
  `markeredgewidth` veyâ `mew` : İşâretleyici kenar kalınlığı, kesirli sayı verilir
  
  `markerfacecolor` veyâ `mfc` : İşâretleyici orta noktası rengi (daire, yıldız, üçgen biçimindeki işâretleyicilerde görünür)
  
  `markeredgecolor` veyâ `mec` : İşâretleyici kenar rengi
  
  `markevery` : Her veri noktasının gösterilip, gösterilmeyeceğini belirtmek için kullanılır. Buraya her veri noktası için `True` veyâ `False` değeri içeren bir liste verilebilir. Hangi noktadan başlayıp, kaç atlama yapılacağını belirten iki tamsayı içeren bir demet olabilir. Misal, `(0, 2)` değeri verilirse, ilk veri noktasından başlayarak, birer atlamalı şekilde veri noktaları çizdirilir. Veri nokta indislerini barındıran bir liste verilebilir.
  
  `alpha` : Grafik çizgisinin görünürlüğünü belirtir, kesirli sayı olarak (1 -> tam görünür, 0 -> görünmez)
  
  `xdata` : X ekseni verisi bu şekilde de verilebilir
  
  `ydata` : Y ekseni verisi bu şekilde de verilebilir.

- ..

## GRAFİKLERİ BARINDIRAN "FIGURE" NESNESİNİ OLUŞTURMA

- Grafikleri daha fazla özelleştirebilmek için pyplot altındaki `Figure` sınıfından yeni bir nesne oluşturmalıyız. Bunun için `plotter.figure()` yazıp, dönen sonucu bir değişkene atayınız.

- `figure` oluştuğunda içerisinde hiçbir eksen yoktur. Eksen şöyle eklenebilir:
  
  ```py
  fg = plotter.figure()
  axes = fg.add_axes([0.2, 0.2, 0.9, 0.9])
  # add_axes kullanımı:
  # [xEkseniBaslangic, yEkseniBaslangic, xEksenUzunlugu, yEksenUzunlugu]
  ```

- Eksenleri ekledikten sonra bu eksenler içerisinde hangi verilerin gösterileceğini `plot()` yöntemiyle belirtip, grafiği çizdirebiliriz.

- Eksenleri bir değişkene atadıktan sonra şu yöntemleri kullanabiliriz:
  
  ```py
  axes.set_xlabel("X ekseni ismi", fontsize=15, color="orange",
          loc = "center")# X eksenini isimlendirir
  # fontsize, color, loc tercihîdir; loc: left, center, right olabilir
  axes.set_ylabel("Y ekseni ismi")# Y eksenini isimlendirir
  axes.set_title("Başlık")# Eksen için başlık belirtilir
  axes.legend(["satışlar"])# Grafik üzerindeki çizgilerin neyi
  # ifâde ettiği bu şekilde belirtilebilir
  # legend() fonksiyonu parametresiz çalıştırıldığında eksenin 'label'
  # özelliğine atanan değerleri gösterir.
  axes.set_xmargin(0.8)# x ekseninde verinin bulunduğu aralık ile
  # eksen başının ve sonunun aralığı arasında uzaklık bırakır.
  # Misal, yukarıdaki örnekte son verimiz 2020 idi; eğer bu kodu
  # çalıştırırsak x ekseni 1970-2040 aralığını gösterir;
  axes.set_ymargin(0.2)# Y ekseninde verinin bulunduğu aralık ile eksen
  # başının ve sonunun arasında uzaklık oluşturmak için kullanılır
  # xmargin ve ymargin değerleri -0.5'den büyük olmalıdır.
  axes.grid(True)# Kareli defter (ızgara) görünümü 
  axes.set_xlim([10, 100])# x verisi [10,100] aralığında olan gösterilir
  axes.set_ylim([50, 500])# y verisi bu aralıkta olan veriler gösterilir
  ```

- `axes` ve `figure` nesnelerini daha kolay elde edebilmek için:
  
  ```py
  (fig, axes) = plotter.subplots(1, 2)# 1 satır, 2 sütun
  # Geriye figure ve eksenlerden oluşan bir demet (tuple) döndürüyor
  # Yukarıdaki şekilde bunları değişkene atayabilirsiniz
  # Parametreler isimle belirtilerek de yazılabilir:
  (fig, axes) = plotter.subplots(nrows=1, ncols=2)
  # Eksenler numpy dizisi olarak döndürülüyor
  ```

- Gelen eksenleri için yapılacak işlemler benzerse, bunları bir döngü içerisinde ayarlayabilirsiniz.

#### 'Figure' Boyut ve Kalitesi

- `figure()` fonksiyonuna `figsize` ile grafik büyüklüğü verilebilir. Demet olarak x ve y uzunluğu verilir.

- `dpi` parametresine grafiğin kalitesini ve büyüklüğünü belirten değer verilebilir.

#### Görüntüyü ('Figure') Kaydetme

- Bunun için `savefig()` yöntemi kullanılabilir. İlk parametre olarak dosya ismi verilir. `dpi` parametresine kalitesini belirten dpi değeri verilebilir.

#### Etiketlerin Grafikteki Yerini Belirtme

- Etiketleri grafik üzerinde göstermek için `legend()` fonksiyonu kullanılır.

- Bu fonksiyona etiket isimleri liste olarak verilebilir.

- Eksenin `label` değeri zâten atandıysa, sadece bu fonksiyonun çağrılması etiketlerin gösterilmesi için kâfîdir.

- Etiketlerin grafik üzerindeki mevkîsini ayarlamak için fonksiyonun `loc` parametresi kullanılabilir. Bu parametreye ön tanımlı tamsayı değerleri verilir:
  
  `1` : Varsayılan değerdir, etiketler sağ üstte görünür
  
  `2` : Sol üstte görünür
  
  `3` : Sol alt
  
  `4` : Sağ alt
  
  `5` : Sağ orta
  
  `6` : Sol orta
  
  `7` : Sağ orta
  
  `8` : Alt orta
  
  `9` : Üst orta
  
  `10` : Tam orta

## DAHA FAZLA ÖZELLİK

- `pyplot.grid(True)` ile verilerin kareli defter arkaplanı gibi görünmesi sağlanabilir.

- `pyplot.text(xMargin, yVal, metin)` ile grafik üzerine yazı yazılabilir;
  `xMargin` metnin x ekseninin başlangıcından itibâren olan uzaklığı belirtir, tam sayı verilebilir.
  `yVal` ise metnin y eksenindeki hangi değer hizasında yazılacağını belirtmek için kullanılır; yanî y eksenindeki veriye göre belirtilir.

- `pyplot.axis("off")` eksen çizgileri gizlenebilir.

#### Grafik Üzerinde Bir Yerin Vurgulanması

- Bunun için `annotate()` yöntemi kullanılır.Parametreleri:
  
  İlk parametresi vurgu metnidir
  `xy` : Vurgulanacak x ve y değeri demet tipinde verilir
  `xytext` : Vurgu metninin yazılacağı x ve y değeri demet tipinde verilir
  `arrowprops` : Ok ile vurgulanacak yerin işâret edilmesini istiyorsak bu ok özellikleri bir sözlük biçiminde bu parametreye verilebilir. Bu sözlüğün 'facecolor', 'shrink' gibi parametreleri olabilir. `facecolor` okun rengidir; 'shrink' parametresi okun ne kadar küçültüleceğini belirtir, 0 ile 1 arasında bir değer verilebilir.

#### Resim Çizdirme

- `pyplot.imshow(resim)` ile resim çizdirilebilir.

- `cmap` parametresi renk haritasını, `vmin` en düşük değerli renk kodunu, `vmax` en yüksek değerli renk kodunu ifâde eder.

- `cmap` parametresine `"gray"` verilirse ve resim siyah - beyaz çizilir.

- `pyplot.colorbar()` komutuyla resme bir renk çubuğu eklenebilir.

#### Matris çizdirme

- `matshow(A)` fonksiyonuyla matris çizdirilebilir; matriste hangi hücrelerde değerin düşük olduğunu, hangi hücrelerde yüksek olduğunu anlamak için uygun bir usûldür.

### Diğer Grafik Çeşitleri Hakkında Kısaca

- `pyplot.scatter(x, y)` : Veri dağılım grafiğini çizer.

- `pyplot.hist(x, y)` : Verinin histogramını çizer.

- `pyplot.step(x, y)` : Verinin adım grafiğini çizer.

- `pyplot.boxplot([x, y])` : Verinin kutu grafiğini çizer.

- `pyplot.bar(categories, data)` : Verilen kategorik verinin oranlarını çizer.

- `pyplot.pie(x)` : Verinin pasta grafiğini çizer. Bâzı parametreleri şunlardır:
  
  - `x = None` : Verinin kendisidir. Veriyi yüzdelik olarak vermenize gerek yok, kendisi hesâplıyor.
  
  - `labels = None` : Her pasta diliminin etiketini barındıran, veri ile aynı sıralamaya sâhip dizidir.
  
  - `shadow = False` : Pastanın arkasında gölge bırakır.
  
  - `radius = 1` : Pastanın çapı ile oynayarak pasta büyüklüğünü ayarlamayı sağlar.
  
  - `frame = False` : `True` değeri verilirse pastayı koordinat sistemi çerçevesine koyar.
  
  - `rotatelabels = False` : Pasta dilimlerinin etiket isimlerini çevirir.
  
  - `normalize = True` : `False` verilirse verileri normalize etmez ve sizden yüzdelik dilimleri ondalık sayı cinsinden belirtmenizi bekler. Bu, büyük verilerde yüzdelik dilimin hesâplandığı durumda ve pastanın bir kısmını boş olacağı durumlarda kullanışlıdır.
  
  - `labeldistance = 1.1` Etiketlerin pasta diliminden ne kadar uzakta olmasını istediğimizi belirtmek için kullanılır. `1`   değeri pastanın kenarını ifâde etmektedir ve değer büyüdükçe etiket yazısı pastadan uzaklaşır; çok büyük değerlerden vermekten kaçınınız.
  
  - `startangle = 0` : Pastanın çizime başlandığı açıyı belirtmek için kullanılır.
  
  - `colors = None` : Pasta dilimlerinin renklerini belirtmek için kullanılır; her dilimin rengi verideki sıraya göre eşleştirilir.
  
  - `explode = None` : Her dilim için sırasıyla, dilimin pasta merkezinden ne kadar ayrılacağını belirtmek için kullanılır; varsayılan olarak pasta bitişiktir. Genellikle 1'den düşük değerler verilmesi uygundur.
  
  - `wedgeprops` : Bu parametre pastanın biçimiyle ilgili bâzı özellikler için öntanımlı ayarların verilebildiği bir sözlük bekler. Biçimle oynamak için kullanılır. Misal `wedgeprops` parametresine `{'linewidth':4}` değeri verilirse pasta kenarları epey kalın olur. Burada verilen özellikler diğer özellikleri baskılar. Bu parametreye şu değerler verilebilir:
    
    - `facecolor` : Pasta dilimlerinin rengidir. Bu parametreye değer verirseniz pastayı çizdirirken verdiğiniz `colors` parametresinin hükmü olmaz.
    
    - `linetyle = solid` : Pasta çizgi biçimini belirtir. 'solid', 'dashed', 'dotted' değerleri verilebilir.
    
    - `alpha = 1` : Pastanın saydamlığını belirtmek için kullanılır. [0,1] arasında değer verilebilir; `1` matlık; `0` ise saydamlık kutpudur.
    
    - `edgecolor` : Kenar rengidir.
    
    - `linewidth` : Kenar kalınlığıdır.
  
  - `autopct = None` : Her pasta diliminin içerisine yüzdelik oranı belirtilen formatta yazılır. Misal, bu parametreye '%d' değeri verilirse yüzdelik dilim tamsayı olarak yazılır; '.4f' değeri verilirse yüzdelik dilim virgülden sonra dört basamak olacak şekilde kesirli sayı olarak yazılır.

- ..
