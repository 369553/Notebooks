# PHP

## ÖN BİLGİLER

- PHP, web siteleri ve web uygulamaları için kullanılan yorumlamalı bir dildir.

- Sunucu tabanlı çalışan bir dildir; yanî web uygulamalarının 'back-end' (arka-uç) alanını hâzırlamak için kullanılır.

- PHP sunucu tarafında çalışıp, kullanıcıya göstermek üzere HTML sayfası üretir / döndürür. Üretilen HTML sayfası istemciye iletilir; web tarayıcı da bu HTML sayfasını görüntüler.

- Açık kaynaktır, uzun seneler boyu yaygın şekilde kullanılmıştır; günümüzde de yaygın şekilde kullanılmaktadır.

- Rasmus Lerdorf ilk geliştiricisidir. Sürekli geliştirilmektedir.

- Dinamik programlamayı sağlar. Misal, sayfa yenilenmeden sayfa üzerinde değişiklik yansıtılması işlemi dinamik bir işlemdir.

- PHP, HTML dosyalarına gömülebilir.

- PHP dosyası, içerisinde HTML kodları barındırabilir (çalıştırılabilir); bu durumda HTML kodları web tarayıcısında çalışırken PHP kodu da sunucu tarafında çalışır.

- PHP, yoğun olarak kullanılan tüm veritabanlarını destekliyor.

- Geniş kullanıcı kitlesi olduğundan, problem çözme noktasında geniş bir ağı var.

- Ocak 2013 itibâriyle 244 milyondan fazla web sitesi PHP ile çalışırken, 2.1 milyon web sunucusunda PHP kurulumu varmış; günümüzde de hâlen revaçtadır.

- Güvenlidir, güvenlik katmanları vardır.

- Ana protokolleri destekliyor (HTTP, FTP, ...)

- CSS ve JavaScript'i destekliyor.

- PHP'yi kullanabilmek için yerel makinenizi sunucu gibi yapılandıran bir yapının olması lazım. Bunun için de sunucu hizmeti sunan Apache Server'ı (veyâ başka bir tânesini), PHP'i kurmanız ve veritabanı için de MYSQL'i (veyâ farklı bir veritabanını) kurmanız ve yapılandırmanız gerekiyor; veyâ bütün bunları tek bir elden yapabilmenizi sağlayan ve sizin için kolaylaştıran XAMPP (Linux için LAMP kurabilirsiniz) yazılımını kurabilirsiniz. 

## GENEL BİLGİLER

- PHP kodları `<?php .... ?>` içerisinde yazılır.

- Her kod satırı noktalı virgül (`;`) ile biter

- PHP'de yapılandırma ayarları ‘php.ini’ dosyasında tutulur.

- Hatâların istemci tarafına gönderilmesi için ‘php.ini’ dosyasındaki ‘display_errors’ yapılandırma parametresi ‘On’ yapılmalıdır.

- PHP'de yazı birleştirme işleci nokta (`.`)dır.

- PHP'de metîn verisi içerisine değişken değeri yerleştirilmek isteniyorsa, bu, süslü parantez içerisinde değişken ismi yazılarak yapılabilir:
  
  ```php
    metin="aşağıdaki {$brand} marka araba.."
  ```

- PHP sayfası içerisinde HTML kodları çalıştırılabilir. Bunun için açılan php etiketi kapanmalı ve HTML kodları o şekilde yazılmalı. Misal:
  
  ```php
  <?php ... ?>
          #... (BURAYA HTML kodları yazılabilir)
  <?php ... ?>
  ```

- PHP 8'de hem kare (`#`) işâretiyle hem de çift ayraç (`//`) ile satır, yorum satırı olarak işâretlenebilir. Çok satırlı yorum için Java'daki gibi yorumun başına `/*` koymalı, yorumun sonuna `*/` koymalıyız.

## VERİ TİPLERİ

PHP'de değişkenler için temel ve veri tipleri ve en çok kullanılan veri tipleri şunlardır:

- **string** : Metînsel verilerdir

- **int** : Tamsayılar için kullanılan veri tipidir

- **noktalı sayısal veri** : Kesirli sayılar için kullanılan veri tipidir

- **boolean** : Tek bitten oluşur ve yalnızca iki değeri (true - false) barındırabilir

- **object** : Nesne yönelimli programlama desteği bulunduğundan nesne üst sınıfıdır

- **array** : Verilerin dizi veyâ harita biçiminde saklanabildiği işlevsel bir veri tipidir

- **null** : Bir değer barındırmayan, dolu bir bellek adresini işâret etmeyen(?) veri tipidir

***NOT***  : `gettype()` yöntemiyle değişkenin tipi öğrenilebilir

## DEĞİŞKENLER

```php
# Değişken tanımlama söz dizimi:
$degisken_ismi = değer
```

- PHP'de değişken tanımlarken değişkenin tipinin belirtilmesi zorunlu değildir

- Değişken isminde boşluk karakteri olamaz,

- Değişken ismi rakamla başlayamaz,

- Değişken isimleri büyük - küçük harf duyarlıdır.

- Değişkenler dolar işâreti (`$`) ile başlar.

- Türkçe karakter kullanılabilir; fakat kullanılmaması tavsiye edilir.

- Type juggling : farklı tipteki değişkenlerin yorumlanabilmesi, karşılaştırılması demektir. PHP yorumlanabilir bir dil olduğundan tamsayı tipinde olmayan, ama tamsayıya çevrilebilen string değişkenleri de tam sayı kabûl eden fonksiyonlara verebiliyorsunuz, karşılaştırma işlemlerinde kullanabiliyorsunuz.

- PHP'de veri tipleri arasında dönüşüm (cast) yapmak kolaydır; Java'daki gibidir; değişkenin önüne parantez içerisinde dönüşüm yapılmak istenen tip yazılır:
  
  ```php
  $noktaliSayi = 2.18;
  $tamSayi = (int) $noktaliSayi // tamSayi = 2
  ```

- Ancak PHP'de dönüşüm biraz daha esnektir. Misal, metînsel bir veri bu şekilde tamsayısal veriye çevrilebilir. Hattâ metînsel verinin tamâmı tamsayıya çevrilemiyorsa, çevrilebildiği kadarı çevrilir; hattâ hiç çevrilemiyorsa varsayılan değer olan sıfır (`0`) değeri atanır.

- PHP'de değişkenin önüne parantez içinde `bool` veyâ `boolean` yazılarak bitsel veriye çevrilebilen veri tipi tam sayıdır. Misal, `false` ifâdesini `bool` tipine çevirmek istersek `true` sonucunu elde ediyoruz!

#### Değişkenlerde Kapsam

- PHP'de değişkenlerin kapsamı biraz farklıdır.

- Diğer dillerde olduğu gibi PHP'de fonksiyon içinde tanımlanan değişkene fonksiyon dışından erişilemez.

- Fakat, PHP'de fonksiyon içerisinden bir üst tabakadaki değişkene de doğrudan erişilemez. Bunun için fonksiyon içerisinde ilgili değişkenin fonksiyon içinde şu şekilde tanımlanması gerekir; bu tanımdan sonraki fonksiyon içerisinde nerede `$degisken` çağırılırsa, orada üst tabakadaki küresel değişken çağrılmış olur.
  
  ```php
  $katsayi = 2.14;
  
  function fonksiyon1(){
      global $katsayi;
      $katsayi = 2.19;
  }
  fonksiyon1();
  echo("Katsayı : {$katsayi}");// Katsayı  : 2.19 yazar
  ```

- Küresel değişkene erişmenin bir başka yolu ise ön tanımlı küresel değişken olan `$GLOBALS` haritasını kullanmaktır. Ön tanımlı küresel değişkenler PHP tarafından tanımlanan ve kodun herhangi bir kısmında erişim isteğinde bulunulabilen değişkenlerdir.
  
  ```php
  $katsayi = 2.14;
  
  function fonksiyon1(){
      echo $GLOBALS["katsayi"];//2.14
  }
  ```

- Fonksiyon içerisinde küresel değişkenlere -normal yollarla- değer atayamıyordunuz; fakat PHP'nin yeni sürümünde bunu yapabiliyorsunuz. PHP'nin eski sürümlerinde bunu yapmak için `$GLOBALS` değişkeninin ilgili değişken ismindeki elemanına şu şekilde erişmelisiniz: `$GLOBALS["degisken_ismi"]`

- 'static' değişken sadece fonk içinden erişilebilen ve fonk bittiğinde bellekten temizlenmeyip, fonksiyon daha sonra yeniden çağrıldığında kullanılabilen değişkendir. Statik değişken tanımlamak için ilgili fonksiyon içerisinde değişken isminden evvel 'static' anahtar kelîmesini yazmalıyız.
  
  #### Ön Tanımlı Küresel Değişkenler (Super Global Variables)
  
  PHP'deki bâzı ön tanımlı küresel değişkenler şunlardır:
  
  - `$_SERVER` : Sunucuyla alâkalı bilgilere ulaşmak için kullanılır. Misal, sayfaya gelen isteğin tipini öğrenebilmek için \$\_SERVER["REQUEST_METHOD"] harita değeri kullanılır.
  
  - `$_ENV` : Betiğin ('script') çevre bilgilerini barındırır
  
  - `$GLOBALS` : Küresel değişkenleri barındıran bir ön tanımlı küresel değişkendir.
  
  - `$_GET` : GET isteğiyle gönderilen parametreleri barındırır
  
  - `$_POST` : POST isteğiyle gönderilen parametreleri barındırır
  
  - `$_COOKIE` : HTTP çerezlerini barındırır
  
  - `$_FILES` : POST yöntemiyle gönderilen dosya verilerini barındırır
  
  - `$_REQUEST` : HTTP isteğiyle ilgili verileri barındırır
  
  - `$_SESSION` : Giriş yapılmış oturum bilgilerini barındırır

#### Sâbitler (Consts)

- Bir kez atandıktan sonra değeri değiştirilemeyen değişkenlere 'sâbit' denir.

- PHP'de sâbit ifâde tanımlamanın iki yolu vardır:
  
  1. `define()` yöntemiyle : Yöntem anahtar - değer kuralına göre çalışıyor. anahtar metînsel bir veri olmalı. Misal:
     
     ```php
     define("baslangicDegeri", 23);
     ```
  
  2. `const` ifâdesiyle : Değişken isminden evvel kullanılır.
     
     ```php
     const dbUrl = "localhost://8080";
     ```

***NOT:*** Sâbit tanımlarken dolar işâreti (`$`) kullanılmadığına dikkat ediniz.

## DİZİLER - LİSTELER

- İki türlüdür:
  
  1) İndis mantığıyla çalışan sıralı diziler
  
  2) Anahtar - değer ilişkisi yapısındaki diziler.

- Dizi içerisinde farklı veri tipinde değişkenler olabildiği gibi, dizi de olabilir.

- ```php
  // İndis mantığıyla çalışan sıralı dizi tanımlama:
  $dizi1 = array("değer1", 2, "değer3");
  
  // Harita mantığıyla çalışan liste tanımı:
  $dizi2 = array(
  "anahtar" => "değer",
  "anahtar2" => "değer2"
  );
  ```

- Verilere erişirken matris verisine erişiyor gibi erişebiliriz: dizi["değer1"]["değer1_1"]

- Dizi üzerinde işlemler:

- ```php
  count($dizi);// Dizideki eleman sayısını döndürür
  sizeof($dizi);// Dizideki eleman sayısını döndürür
  array_push($dizi, $eleman);// Dizinin başına eleman ekler
  array_unshift($dizi, $eleman);// Dizinin sonuna eleman ekler
  array_shift($dizi);// Dizinin başından bir eleman siler;
                     //geriye sildiği elemanı döndürür
  array_pop($dizi); // Sondan eleman siler; geriye sildiğini döndürür
  array_unshift($dizi); //Dizinin başından 1+ sayıda eleman siler
  array_pad($dizi, $uzunluk, $deger); //Eğer dizi verilen boyutta değilse,
          //dizi boyutunu verilen boyuta çıkarır ve yeni elemanlara
          //verilen değeri atar.
          // Parametreleri : array $dizi, int $uzunluk, mixed $deger
  in_array(); // Verilen dizide verilen değeri arar,
              // Üçüncü parametre olan 'strict' parametresine
              // 'true' verilirse aranan değerin tipine de bakar.
  array_reverse(); // Diziyi tersten sıralayıp, döndürür.
  ```

> 

#### Dizilerde Sıralama Yöntemleri

- `sort($dizi[, $bayraklar])` : İkinci parametre tercihîdir. Sadece dizi verilirse verilen dizi artan sırada sıralanır. Bu fonksiyon doğrudan dizi üzerinde değişiklik yaptığından geriye dizi döndürmez; dâimâ `true` döndürür. Bayraklar, sıralamanın neye göre yapılacağını belirtmek için kullanılan yapıdır. Şu bayraklar vardır:
  
  1. `SORT_REGULAR` : Sıralama karşılaştırma işleçleri kullanılarak yapılır, buna normal sıralama denir.
  
  2. `SORT_NUMERIC` : Sıralamanın sayısal olarak yapılması için kullanılır.
  
  3. `SORT_STRING` : Sıralamanın metînsel olarak yapılması için kullanılır.
  
  4. `SORT_LOCALE_STRING` : Sıralamanın bulunulan bölgenin karakter setine göre yapılması için kullanılır.
  
  5. `SORT_NATURAL` : İçerisinde sayı bulunan metînsel verilerde alfabetik isme göre sıralama yapıldığında, sayısal olarak yanlış sıralama yapılmış olabiliyor. Misal, 'araba10' elamanı, 'araba2' elemanından önceye yerleştiriliyor; çünkü 'araba' kelîmesi bittiğinde alınan '1' karakteri '2'den önce geliyor. Bunun böyle olmaması ve metînler sıralanırken sayı kısımlarının sayı gibi sıralanması için bu bayrak işâretlenmelidir.
  
  6. `SORT_FLAG_CASE` : Metînsel sıralama yaparken, küçük - büyük harf duyarsız sıralama yapılması için kullanılır. Bu bayrak `SORT_NATURAL` ve `SORT_STRING` gibi metînsel sıralamayı ifâde eden bayraklarla berâber kullanılır.
  
  Birden fazla bayrağı berâber kullanırken  bayraklar boru ('pipe', `|`) denilen işâretle birbirinden ayrılmalıdır : `sort($dizi, SORT_NATURAL | SORT STRING);`
  **Çok dikkat edilmesi gereken bir detay, bu fonksiyon nesne elemanlarına yeni indis (anahtar) değeri atar**. Dolayısıyla, elemanların indisleri sayısal olarak sıralama değilse, o anahtarları kaybetmiş olursunuz.

- `asort($dizi, )` : Dizinin değerlerini anahtarlarıyla ilişkisini bozmadan sıralar. Sıralama değere göre yapılır. Yine benzer bayraklar kullanılabilir.

- `ksort()` : Başında 'k' harfi 'key' (anahtar) kelîmesini ifâde eder. Sıralama anahtarlara göre yapılır; bayraklar kullanılabilir.

- `krsort()` : `ksort()` ile aynı işlevi yapar; tek farkı sıralamayı artan sırada, yanî tersten yapar. 'sort' ifâdesinin başındaki 'r' harfi bunu ifâde etmektedir.

- `arsort()` : `asort()` ile aynı işlevi yapar; tek farkı sıralamayı artan sırada, yanî tersten yapar. 'sort' ifâdesinin başındaki 'r' harfi bunu ifâde etmektedir.

#### Diğer Bâzı Dizi Yöntemleri

- `array_flip($dizi)` : Aldığı dizinin indisiyle değerlerini yer değiştirir.

- `array_rand($dizi, $istek_sayisi)` : Diziden belli sayıda rastgele anahtar döndürür. `$istek_sayisi` parametresi ise, kaç anahtar değeri istendiğini belirten bir parametredir; sıfırdan büyük, dizi uzunluğundan küçük veyâ dizi uzunluğuna eşit olmalıdır. Bu seçim işleminin kriptografik olarak güvenilir olmadığı belirtilmektedir.

## FONKSİYONLAR

- Fonksiyon `function` ifâdesiyle tanımlanıyor:
  
  ```php
  function ilkFonksiyon(){
      //.;.
  }
  ```

- Fonksiyon tanımlanırken fonksiyonun geri dönüş tipini ve geri döndürdüğü değeri yazmak zorunda değiliz.

- Geri döndürme işlemi `return` deyimiyle yapılıyor.

- Fonksiyon girdisinde veri tipi belirtilebilir, fakat zorunlu değildir. Misaldeki ilk girdinin tipi belirtilmemiş, ikincinin ise belirtilmiştir:
  
  ```php
  function fonksiyon($girdi_1, int $girdi_2){
      //.;.
  }
  ```

- Girdi parametrelerine varsayılan değer atanabilir. Misal:
  
  ```php
  function fonksiyon($girdi_1 = 21){}
  ```

- Fonksiyona sayısı belirsiz girdi parametresi verilebilir. Şöyle ki:
  
  ```php
  function fonksiyon(...$girdiler){}
  ```

- Programlama dillerinde fonksiyon girdileri genellikle yeni bir değişken olarak saklanır. Bu, PHP'de de böyledir. Dolayısıyla bir fonksiyona bir değişkeni parametre olarak gönderirseniz, fonksiyon aldığı parametre üzerinde değişiklik yapsa, bu durumda bu değişiklikler gönderdiğiniz değişken üzerinde yapılmış OLMAZ!

- Gerçekten bir değişken üzerinde değişiklik yapan bir fonksiyon tasarlamak istiyorsak, bu durumda girdi parametresinin önüne '&' işâreti ekleyerek gönderilen değişkenin adresinin parametre olarak verilmesini sağlamalıyız:
  
  ```php
  function BasHarfiBuyukHarfeCevir(&$metin){}
  ```

- Fonksiyonun parametre sayısını `func_num_args()` yöntemini fonksiyon içerinden çağırarak öğrenebiliriz

- Yine fonksiyon içerisinden çağrılabilen `func_get_arg($girdi_indeksi)` yöntemiyle ise verilen sıra numarasındaki fonksiyon girdi parametresine erişilebilir.

- PHP'de parametre istemeyen fonksiyona parametre gönderilebilir; uygulama hatâ vermez.

- PHP'de fonksiyon girdi parametresinin veri tipi belirtildiğinde dahî, o fonksiyona istenen veri tipine dönüştürülebilen parametre girdi olarak verilebilir. Misal:
  
  ```php
  function fonksiyon(int $girdi_1){
      echo $girdi_1;
  }
  fonksiyon(2);// Doğru girdi tipi
  fonksiyon(2.0);// Ayar değiştirilmedikçe hatâ vermez
  fonksiyon("2.0");// Ayar değiştirilmedikçe hatâ vermez
  fonksiyon("2");// Ayar değiştirilmedikçe hatâ vermez
  ```

- Tabi bu ayar varsayılan olarak böyledir. PHP sayfasında fonksiyondan script'in başında ayrı bir kod bloğu olarak şu kodu yazarsanız yukarıdaki fonksiyon sadece tamsayı (`int`) türündeki girdileri kabûl eder:
  
  ```php
  <?php declare(strict_types=1); ?>
  // Yukarıdaki kod bloğu ana <?php ...?> kod bloğundan evvel yazılmalı(?)
  // Bu ayar sadece bu kodun yazıldığı dosya için geçerlidir.
  ```

- Eğer fonksiyonun geri dönüş tipini fonksiyon tanımında belirtmek istersek şu şekilde yapabiliriz:
  
  ```php
  function fonksiyon() : int{
      return 0;
  }
  ```

- 'strict_types' isimli ayar değişkeni üzerinden tiplerin birbirine dönüşmesinin zorlanması seçeneğini devredışı bırakabiliyoruz; bunun istisnası `float` değişkenidir. Veri tipi zorlamasını devre dışı bırakmış olsanız bile, `float` veri tipini kabûl eden bir fonksiyona tam sayıyı gönderebilirsiniz.

- Fonksiyonların girdi parametrelerini isimlendirilerek, fonksiyon parametrelerinin sırası bilinmeden fonksiyonlar çeşitli farklı biçimlerde kullanılabilir. Bunlara 'named arguments' (isimlendirilmiş parametre) deniyor. Bu özellik PHP 8.0'dan itibâren var. Emsal kullanım:
  
  ```php
  function izinKontrol($ipAdresi, $oturumIsmi){}
  izinKontrol($oturumIsmi : "gX35g", $ipAdresi : "127.168.1.1");
  ```

- Bİr fonksiyonun birden fazla tipte geri dönüş yapabilmesi mümkündür. Misal, 'strpbrk' yöntemi verilen karakterleri verilen metîn içerisinde arar; eğer bulursa, o karakterden itibâren alt metni döndürür; yanî geriye 'string' tipinde bir değer döndürür; fakat bulamazsa geriye 'false' döndürür; yanî 'boolean' tipinde bir değer döndürür.

- `null` değer `string`'e dönüştürüldüğünde boş metîn elde edilir.

- dizi (`array`) tipindeki değişken `string`'e dönüştürülmek istendiğinde 'Array' yazısı elde edilir, ayrıca sunucu uyarı da verir.
  
  ##### Sayısız (Belirsiz sayıda) Parametreli Fonksiyon (variadic-function):

- Bir fonksiyona çok farklı sayılarda parametre gönderilmesi isteniyorsa, bunun bir yolu fonksiyon imzasında herhangi bir parametre belirtmeyip, fonksiyon içerisinde `func_get_args()` yöntemini kullanarak gelen parametreleri almaktır.
  
  ```php
  function topla(){
      $parametreler = func_get_args();
      $toplam = 0;
      for($sayac = 0; $sayac < count($parametreler); $sayac++){
          $toplam += $parametreler[$sayac];
      }
      return $toplam;
  }
  ```
  
  Bunun başka bir yolu ise üç nokta işlecini ('...') kullanmaktır. Bu işleç, PHP 5.6 ile gelmiş.
  
  ```php
  function topla(...$sayilar){
      $toplam = 0;
      for($sayac = 0; $sayac < count($sayilar); $sayac++){
          $toplam += $sayilar[$sayac];
      }
      return $toplam;
  }
  ```
  
  PHP 7 ile sayısız parametre işlecinin belirttiği değişkenin tipini belirleme özelliği de gelmiş. Buna göre fonksiyon imzasında girdi kısmına `int ... $sayilar` yazarak gelen tüm parametrelerin tam sayı tipinde olması gerektiği belirtilebilir.

##### Bâzı Ön Tanımlı, Kullanışlı Fonksiyonlar

```php
$dizi = array("a", "b", "c");

count($dizi)# İçerisine aldığı dizinin eleman sayısını döndürür : 3
```

  ...

## METÎNLER (STRINGS)

- `echo()` fonksiyonunda değişkenlerin metîn ile berâber değişken kullanımı:
  
  1. Metin ile değişkeni birleştirerek:
     
     ```php
     echo "Geçtiğimiz gün ".$[degisken]."'i gördüm.";
     ```
  
  2. Metin içerisinde süslü parantez içinde değişkeni çağırarak:
     
     ```php
     echo "Geçtiğimiz gün {$[degisken]}'i gördüm.";
     ```
  
  3. Metin içerisinde doğrudan değişkeni çağırarak:
     
     ```php
     echo "Geçtiğimiz gün $[degisken]'i gördüm.";
     ```

#### Önemli Metînsel Yöntemler / Fonksiyonlar

- Metnin bir parçasını alma: `substr()`
  Parametreler:
  
  1. Metîn
  
  2. Başlangıç indeksi
  
  3. Alınacak karakter sayısı
  
  Eğer parçalanmak istenen metîn Türkçe karakter içeriyorsa 'mb_substr' kullanılmalıdır. (mb_substr : 'multibyte' ifâdesinin baş harfleri fonksiyon başına getirilmiştir. ASCII karakteri dışındaki karakterler 1 byte ile ifâde edilmediğinden Unicode karakterlerle çalışırken bâzen fonksiyonların başına 'mb' getirilmiş versiyonları tercih edilmelidir).
  
  ```php
  echo substr("Turkiye",2,4);// 'rkiy'
  echo mb_substr("Türkiye", 2, 4);// 'rkiy'
  ```
  
  Eğer başlangıç indisi eksi işâretli bir sayı olarak verilirse dizinin son elemanı -1, sondan bir önceki eleman -2 olacak şekilde dizinin sonundan alt metîn alınabilir. Ayrıca üçüncü parametre ters indis olarak da kullanılabilir.
  
  ```php
  echo mb_substr("Türkiye", -4, 3);// 'kiy'
  echo mb_substr("Türkiye",2,-3)."<br>";// 'rk'
  // T    ü    r    k    i    y    e
  // 0    1    2    3    4    5    6    -> İndisler
  //-7   -6   -5   -4   -3   -2   -1    -> Ters indisler
  ```

- Metîndeki bâzı harf veyâ harflerin başka harf veyâ harflerle değiştirilmesi: `str_replace()`
  
  Parameteler:
  
  1. Değiştirilmesi istenen metînsel değer
  
  2. Yeni metînsel değer
  
  3. Metîn
  
  Değiştirilmesi istenen parametreler dizi hâlinde verilebilir. Misal, değiştirilmek istenen dizinin ["mi", "?"] olduğunu, yeni değerlerin ["", "!"] olduğunu varsayalım. Bu durumda yazıdaki "mi" değerleri boş metînle, soru işâretleri de ünlem işâretiyle değiştirilir.
  
  ***NOT:*** Değiştirilen metîn geriye döndürülür; asıl değişken değiştirilmez.
  
  Bunun küçük büyük harf duyarlı olmayan hâli: `str_ireplace()` fonksiyonudur.
  
  ```php
  $metin = "http://localhost/sources";
  echo str_replace("http", "https", $metin);// https://localhost/sources
  echo str_replace(["http", "localhost"], ["https", "uygurrapor.rf.gd"],
                  $metin);// https://localhost/sources
  echo str_ireplace("rw-", "r--", "dRW-RW-R--");// dr--r--R--
  ```
  
  ##### Diğer önemli fonksiyonlardan bâzıları:
  
  ```php
  echo strtolower("ADAM");// Küçük harfe çevirir : adam
  echo strtoupper("tur");// Büyük harfe çevirir : TUR
  echo str_word_count("15 kişiydik.");// kelîme sayısını döndürür : 2
  echo strlen("ADAM");// Metîn uzunluğunu döndürür : 4
  echo ucfirst("tokat meydanı");// İlk harfi büyük yapar: Tokat meydanı
  echo ucwords("tokat meydanı");// Kelîmelerin ilk harfini büyük yapar
  echo trim(" Ak ");// Metnin başındaki ve sonundaki boşlukları siler
  echo ltrim(" Ak ");// Sol (baştaki) boşluğu sil
  echo rtrim(" Ak ");// Sağ (sondaki) boşluğu sil
  echo substr_count("rw-r--r--", 'r');// Aranan ifâde kaç defâ geçiyor:3
  echo str_contains("rw-r--r--", "rwx");// İlk metîn içinde ikinci
                      // parametredeki metîn geçiyorsa true döndürür
  ```

- Metin içerisindeki bir kelîmeden itibâren alt metin alma : `strstr()`
  
  Parametreler:
  
  1. Metîn
  
  2. Aranan baslangıç kelimesi
  
  Bunun küçük büyük harf duyarsız olanı : stristr()
  
  ```php
  $metin = "Sırasıyla : 15, 17, 71";
  echo strstr($metin, ":");// : 15, 17, 71
  echo stristr("Akşam ankara'da...", "Ankara");// ankara'da...
  ```

- Metni diziye çevirme: `str_split()`
  Parametreler:
  
  1. İlk parametre metîndir
  
  2. İkinci parametre metînden alınmak istenen uzunluk miktarıdır
  
  ```php
  $metin = "drwxrw-rw-";
  $dizi = str_split($metin);
  echo $metin[1];// r
  echo $dizi[1];// r
  echo gettype($metin);// string
  echo gettype($dizi);// array
  ```

- Metnin ne ile başladığını kontrol etme: `str_starts_with()`
  Geriye 'boolean' tipinde bir değer döndürür.
  Parametreler:
  
  1. Metîn
  
  2. İlgili karakter veyâ karakter dizisi
  
  ```php
  echo str_starts_with($metin, "d");// 1
  ```

- Metîn içerisinde karakter arama: `strpbrk()`
  Bu fonksiyon metîn içerisinde ikinci parametreyle verilen harflerden birini arıyor; ilk bulduğundan itibâren alt metni oluşturmaya başlıyor ve cevâp olarak bu alt metni döndürüyor. Eğer aranan karakterlerden birisi dahî fonksiyonda yoksa 'false' döndürüyor. Karakterler büyük - küçük harf duyarlı olarak aranıyor.
  Parametreler:
  
  1. Metin
  
  2. Harflerden oluşan metin (dizi olarak verilmemelidir)

- ```php
  echo strpbrk("iiisbbsi", "bs");// 'sbbsi'
  ```

- Alt metnin başlangıç mevkîsini öğrenme: `strpos()`
  Eğer aranan alt metîn (veyâ harf) bulunursa bu alt metnin (veyâ harfin) metîn içerisindeki başlangıç indisi döndürülür; bulunamazsa, geriye 'false' döndürülür.
  Parametreler:
  
  1. Metîn
  
  2. Aranan alt metîn (veyâ harf)
  
  3. Arama başlangıç indisi (varsayılan olarak sıfırdır, yanî varsayılan olarak metnin başından itibaren arar)
  
  ```php
  echo strpos("drw-rw-r--", "w");// 2
  echo strpos("drw-rw-r--", "w", 3);// 5
  ```
  
  Bu fonksiyonun unicode karakterler için olan versiyonu : `mb_strpos` fonksiyonudur. Bu fonksiyon dördüncü parametre olarak string biçiminde metîn kodlama ismini alır (eğer üçüncü parametre verilmeyecekse üçüncü parametre olarak yazılır, zîrâ üçüncü parametrenin varsayılan değeri vardır):
  
  ```php
  echo mb_strpos("Gerçekten...", "ç", "UTF-8");// 5
  ```

- Bir metni düzenli şekilde katlamak, belli uzunlukta yazdırmak için `wordwrap()` fonksiyonu kullanılır. Parametreleri:
  
  1. Metîn (string)
  
  2. Metnin katlanacağı ve istenen harfin getirileceği uzunluk (integer)
  
  3. Belirlenen uzunluğa yerleştirilecek metînsel veri (string)
  
  4. Eğer belirlenen uzunlukta bir kelîme içerisindeysek, kelîmenin bölünüp, bölünemeyeceği parametresi (boolean)
  
  ```php
  $metin = "Gerçekten doğruları görmek isteyene zor değildir.";
  echo word_wrap($metin, 30, "<br/>");
  # Gerçekten doğruları görmek<br/>
  # isteyene zor değildir.
  ```

- ...

***NOT:*** `explode()` yöntemiyle metni belli bir ayraca göre ayırıp, diziye çevirebiliriz. Bu fonksiyonun ilk parametresi ayraç, ikinci parametresi ise parçalanacak metîndir.

## KULLANIŞLI FONKSİYONLAR

##### Genel:

`phpinfo()` : PHP sunucusuyla ilgili temel bilgileri yazdırır. Bunlar içerisinde şunlar vardır: PHP versiyon bilgisi, işletim sistemi ve sürümü, bilgisayar ismi, sunucu tipi, yapılandırma dosyası (php.ini)nın dosya yolu, IPv6 desteği, 'Thread Safety', 'Thread API'

`die()` : Betik dosyasını ('script') çalıştırmayı durdurur.

`var_dump()` : Aldığı değişkenin veri tipini ve değerini ekranda görüntüler.

..

##### Matematik Fonksiyonları:

`is_int()` : Tam sayı mı?

`is_float()` : Ondalıklı sayı mı?

`is_double()` : Ondalıklı sayı mı?

`is_numeric()` : Bir sayı mı? (Bu fonksiyon metin hâlindeki sayıları da sayı olarak algılıyor)

`ceil()` : Yukarı yuvarla

`floor()` : Aşağı yuvarla

`abs()` : Mutlak değerini al

`sqrt()` : Karekökünü al

`pow($sayi, $us)` : \$sayi değişkeninin \$us derecesinden üssünü al

`max($sayilar)` : \$sayilar içerisindeki en büyük sayıyı döndür

`min($sayilar)` : $sayilar içerisindeki en küçük sayıyı döndür

`sin()` : sinüsünü al

`cos()` : Kosinüsünü al

`acos()` : Ark kosinüsünü al

`asin()` : Ark kosinüsünü al

`rad2deg()` : Verilen radya değerini dereceye çevir

`bindec()` : Verilen ikili sayı sistemi sayısını onluk sisteme çevir

`decbin()` : Verilen onluk sayı sistemi sayısını ikilik sisteme çevir

`decoct()` : Verilen onluk sayı sistemi sayısını sekizlik sisteme çevir

`octdect()` :Verilen sekizlik sayı sistemi sayısını onluk sisteme çevir

`exp()` : 'e' sayısının üssünü al

`hexdec()` : Verilen onaltılık sayı sistemi sayısını onluk sisteme çevir

`dechex()` : Verilen onluk sayı sistemi sayısını onaltılık sisteme çevir

`is_finite()` : Sayı sonlu mu?

`is_infinite()` : Sayı sınırsız mı?

`is_nan()` : Sayı mı?

`getrandmax()` : Olası en büyük değer

`mt_getrandmax()` : En yüksek olası değer

`getrandmax()` : Karekökünü al

`rand($taban, $tavan)` : Rastgele değer üretir. Parametreler verilmezse sıfır ile tam sayı üst sınırı arasında rastgele sayı üretir.

`mt_rand()` : Rastgele değer üret (geliştirilmiş, daha hızlı versiyonu). Parametreler verilmeyebilir.

`pi()` : Pi sayısı

`tan()` : Tanjantını al

`cot()` : Kotanjantını al

***NOT:*** Daha fazlası için ziyâret et : https://www.php.net/manual/en/ref.math.php

##### Sunucu Tarafı Fonksiyonları:

`move_uploaded_file($kaynak, $hedef)` : \$kaynak adresindeki dosyayı \$hedef adresine taşır. İşlem başarılı olursa 'true', başarısız olursa 'false' döndürür.

## İŞLEÇLER

- İşleçler genellikle Java'daki gibidir; ama eksiği ve fazlası vardır.

- **Atama ve aritmetik işleçler:**
  
  | İşleç | İşlevi                      | İşleç | İşlevi                |
  |:-----:|:---------------------------:|:-----:|:---------------------:|
  | =     | Değerleri atar              | -     | Çıkarma işleci        |
  | .=    | Metînleri birleştirip, atar | %     | Mod alma işleci       |
  | *     | Çarpma işleci               | **    | Üs alma işleci        |
  | /     | Bölme işleci                | ...++ | Sonra arttırma işleci |
  | +     | Toplama işleci              | ++... | Önce arttırma işleci  |
  | --... | Önce eksiltme işleci        | ...-- | Sonra eksiltme işleci |
  | +=    | Topla ata                   | -=    | Çıkar ata             |
  | *=    | Çarp ata                    | /=    | Böl, ata              |
  | %=    | Mod al, ata                 |       |                       |

- **Karşılaştırma işleçleri:**

- | İşleç | İşlevi         | İşleç | İşlevi                           |
  |:-----:|:--------------:|:-----:|:--------------------------------:|
  | !=    | Eşit değil mi? | <=>   | Eşit değil mi?                   |
  | ==    | Eşit mi?       | <>    | Eşit değil mi?                   |
  | <     | Küçük mü?      | ===   | Eşit mi ? (Veri tipine de bakar) |
  | >     | Büyük mü?      |       |                                  |

- **Bitsel işleçler:**

- | İşleç | İşlevi          | İşleç  | İşlevi      |
  |:-----:|:---------------:|:------:|:-----------:|
  |       |                 | Değili | <<          |
  | &     | ve              | >>     | sağa kaydır |
  | ^     | özel veyâ (xor) |        |             |

- **Metîn işleçleri:**
  
  | İşleç | İşlevi            | İşleç | İşlevi                  |
  |:-----:|:-----------------:|:-----:|:-----------------------:|
  | .     | Metin birleştirme | .=    | Metni birleştirerek ata |

- **Mantıksal işleçler:**
  
  | İşleç | İşlevi    | İşleç | İşlevi |
  |:-----:|:---------:|:-----:|:------:|
  | &&    | ve        | !     | değili |
  | and   | ve        |       |        |
  |       | \|        | veyâ  |        |
  | or    | veyâ      |       |        |
  | xor   | özel veyâ |       |        |

- **Diğer işleçler:**
  
  | İşleç      | İşlevi                                                                                                    | İşleç      | İşlevi                                                                                                                                                                                                      |
  |:----------:|:---------------------------------------------------------------------------------------------------------:|:----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
  | yield      | Fonksiyondan veriyi alır, döndürür ve fonksiyonun çalışmasını durdurur                                    | clone      | Bir nesnenin kopyasını oluşturmak için kullanılır. Bu, 'shallow copy' biçimindeki bir kopyadır; yanî yeni nesne oluşturulur. Nesne içindeki özellikler, temel tiplerdeyse kopyalanır; nesne ise kopyalanmaz |
  | yield from | Değer üretilmesini başka bir üreticiye devretmek için üretici ('generator') içerisinde kullanılır         | instanceof | Nesnenin belirtilen sınıfın veyâ arayüzün bir örneği olup, olmadığını kontrol etmeyi sağlar                                                                                                                 |
  | ?:         | Kısa şart ('ternary') yazım biçimidir, ilgili bölüme bakınız                                              | @          | Hatâ kontrol işlecidir                                                                                                                                                                                      |
  | ??         | null birleşim işlecidir. Bu işlecin solundaki ifâde null değilse onu, null ise sağındaki ifâdeyi döndürür | ``         | Kabuk (shell) komutu çalıştırmak için kullanılır                                                                                                                                                            |

- Java'dakinden farklı olarak ‘üs alma’ işleci var (Python'da olduğu gibi..): `**`

- Üs alma işleci olduğu gibi ‘üs alıp, atama’ işleci de var: `**=`

- PHP'de kontrol işlecinde Java'dakinden biraz farklılık var, PHP bu tür basit esneklikleriyle Python'a da benziyor. Şöyle ki, PHP'de ‘eşit mi?’ işleci (`==`) değer tabanlı kontrol yapıyor; yanî veri tipleri farklı olsa dahî barındırdıkları değer aynı cinsten ve eşit ise bu işleç ‘true’ sonucu üretiyor. Misal, şu kontroller PHP'de ‘true’ sonucu üretiyor:
  `2 == "2"`
  `2 == 2.0`

- Bu durumda iki değerin yalnızca veri tiplerinin aynı olduğu ve barındırdığı değerlerin de aynı olduğu durumda ‘true’ değeri üreten yeni bir işlece ihtiyaç var. O da üç kez art arda eşittir işâreti yazılmasıyla ifâde edilen işleç: `===`

- Tabi bu işlecin olumsuz anlamda olan versiyonu (Java'daki ‘eşit değil’ (`!=`) işleci) ise şudur: `!==`

- Nokta işleci (`.`) ise metînlerde 'metîn birleştirme' işlemi yapar. Sayılarda da yine aynı işlemi yapar; yanî sayıları metne çevirir ve metînleri birleştirir.

- Nokta işlecinin işlem yaptıktan sonra atayan versiyonu da yeni bir işleç olarak var : `.=`

- Başka yeni 2 kontrol işleci ise şunlar:
  `<>`, `<=>`
  Bu işleçler de 'eşit değil mi?' kontrolü yapıyorlar

##### MANTIKSAL İŞLEÇLER

- Mantıksal işleçlerin pek çoğunun farklı versiyonu var; bunun sebebi, ‘SQL Injection’a karşı tedbir alınmasıdır.
  
  ```php
  if(a and b) // = if(a && b)
  if(a or b) // = if(a || b)
  if(a | b) // = if(a || b)
  
  if(a xor b) // Özel veyâ
  not
  ```

- İşleçlerdeki öncelik diğer dillerdekine benzerdir. Eğer işleçler eşit önceliğe sâhipse işlecin yönüne göre sırasıyla işlem yapılır. Misal `+` işlecinin yönü 'soldan' olduğu için `2+3+1` ifâdesi `(2+3)+1` şeklinde gruplanır. Lâkin `=` işlecinin yönü 'sağdan' olduğu için `$a = $b = $m`' ifâdesi '`$a = ($b = $m)`' şeklinde gruplandırılır.

## ŞART KONTROL

- if şart bloğu Java'dakine ve C'dekine benziyor; fakat ‘else if’ ifâdesi bitişik yazılıyor : `elseif`

- ‘switch - case’ yapısı da C'deki gibidir. `break` ifâdesi konulmazsa tüm tüm koşullar çalışır

- if kontrol yapısı Java'dan farklı olarak, içerisine aldığı değer 'null' olduğunda false; 'null' olmadığında true değerini üretiyor; bunlar PHP'nin yorumlamalı bir dil olmasının getirdiği özelliklerdir.

- ##### Tek satır kontrol söz dizimi (ternary):
  
  Yapısı: **sart ? ifade1 : ifade2**
  Eğer ‘sart’ sağlanıyorsa ‘ifade1’ çalıştırılır, sağlanmıyorsa ‘ifade2’ çalıştırılır.
  Eğer ‘ifade1’ içerisinde başka bir tek satır kontrolü yapmak istiyorsak, parantez içerisine almalıyız:
  `sart ? (sart2 ? ifade1_1 : ifade1_2): ifade2`
  
  ```php
  $metin = "rw-";
  $canRun = (gettype(strpos($metin, "x")) == "integer") ? true : false;
  if($canRun)
      echo "Dosya çalıştırma izni var."."<br>";
  else
      echo "Dosya çalıştırma izni yok."."<br>";
  ```
  
  ...

## DÖNGÜLER

`for` ve `while` döngüleri C ve Java dilindeki gibidir.

##### 'foreach' döngüsü:

Dizi içerisindeki tüm elemanlar üzerinde gezinmenin kolay bir yoludur.
Yapısı:
`foreach ($eleman as $dizi){...}`
Harita biçimindeki listelerde şu şekilde kullanılabilir:
`foreach ($degisken as $key => $value){...}`

```php
$isimler = "Ahmet Mehmet Hasân";
$dizi = explode(' ', $isimler);// isimler diziye çevriliyor
foreach($dizi as $isim){
    echo "isim : ".$isim."<br>";
}
/*  isim : Ahmet
    isim : Hasân
    isim : Mehmet */
```

***NOT:*** PHP sayfası içerisinde HTML kodları yazılabildiğinden ötürü, php etiketiyle bir döngü açıldıysa ve araya HTML kodları yazıldıysa, bu HTML kodlarının sonunda tekrar php etiketi açılıp, döngü sonunda olduğu belirtilmelidir:

```php
<?php foreach($elemanlar as $eleman) ?>
// ... (BURAYA HTML kodları yazılır)
<?php endforeach; ?>
// Döngü ‘for’ döngüsü olsaydı kapanış için ‘endfor;’ yazılmalıydı.
```

• ..

## PHP'de PARÇALI TASARIM

- PHP sayfası içerisine başka bir PHP sayfasını dâhil edebiliriz. Bu yapıldığında hâricî PHP sayfasında tanımlanan değişkenler, fonksiyonlar bu sayfada kullanılabilir. İlgili PHP sayfasındaki HTML kodları da dâhil edildiğinden başka sayfada tasarlanan görünüm bu sayfada kullanılabilir

- Bunun için iki yöntem vardır. Birincisi sayfayı bu sayfaya dâhil etmek, ama çağrılan sayfanın var olmasını şart koşmamaktır:
  
  ```php
  include 'digerPHPSayfasi.php';
  ```
  
  Eğer ‘digerPHPSayfasi’ yoksa sayfanın ilgili kısmı ya boş görünür, yâ dâ hatâ olarak görünür (bu ayarı php.ini sayfasından değiştirebilir miyiz?); sayfanın diğer kısımları yüklenir.

- İkincisi ise, sayfanın çalışması için hâricî sayfanın olmasını şart koşmaktır:
  
  ```php
  require 'digerPHPSayfasi';
  ```

- Çağrılan sayfa tek tırnak içerisinde yazılmak zorunda değildir; sonuna noktalı virgül konulması şart değildir; konulursa da hatâ vermez.

## FORMLAR

- Formları kullanıcıdan kolayca girdi almak için kullanırız. Şu HTML koduyla basit bir form tasarlanabilir:

```html
<form action="search.php" method="GET">
    <input type="text" name="key">
    <button type="submit">ARA</button>
</form>
```

- Yukarıdaki form ‘search.php’ sayfasını ‘GET’ yöntemiyle çağırır; çağırırken ‘key’ anahtar kelîmesiyle bir değer gönderir.

- HTTP protokolünde birkaç sayfa çağırma yöntemi mevcuttur:
  
  1. **GET** : Bu yöntem sunucudan veri istendiği kullanılır. Gönderilen sorgu paramereleri sayfa adresine yazılır. Sunucu tarafından sayfa adresinden alınır. Sayfa adresinde istenilen parametre ve değer ikilisi yazılabildiğinden ötürü, GET parametreleri ‘script injection’ ve ‘sql injection’ türü saldırılara açık bir yöntemdir. Sunucu tarafında alınan birkaç basit tedbirle bu saldırılardan korunulabilir. Gönderim yöntemi ‘GET’ olduğunda gönderilen parametre ve değeri sayfa adresine eklenir, misal:
     www.search.com?key=girilen_deger
  
  2. **POST** : Bu yöntemde sunucuya gönderilen parametreler sunucuya gönderilen isteğin (‘request’) gövdesine (‘body’) yazılır; bu istek şifrelenip, paketlenerek gönderildiyse -ki HTTPS protokolünde böyle yapılır- gönderilen parametreleri paket trafiğini izleyen birisi göremez (şifreyi kırması gerekir). Bu yöntem genellikle kullanıcı adı ve şifresi gibi önemli bilgiler gönderilirken kullanılır. Yöntemin sonunda sunucudan bir cevâp istenmez mi?
  
  3. PUT : Bu yöntem sunucuya yüksek boyutlu veri yüklenirken kullanılır.

- ‘search.php’ sayfasında ön tanımlı bir değişken olan `$GET` değişkeni aracılığıyla gönderilen parametreye erişilebilir: `$GET["key"]`

- Eğer parametre gönderim yöntemi ‘POST’ olsaydı ilgili sayfada `$_POST` ön tanımlı değişken aracılığıyla bu değere erişilebilir.

- Tarayıcıdan elle adres girmek sûretiyle GET yöntemiyle değer gönderebiliriz (eğer ilgili sayfa bu yöntemi kabûl ediyorsa (?)); bunu yaparken her parametre arasına `&` işâreti koymalıyız.

- Eğer POST yöntemiyle dosya gönderilmek isteniyorsa HTML formunun `enctype` parametresine `"multipart/form-data"` değeri verilmesi gerekiyor

- POST yöntemiyle sunucuya yüklenen dosyalara `$_FILES` ön tanımlı değişkeniyle erişilir.

## ÇEREZLER (Cookies) ve OTURUMLAR (Sessions)

- Çerez istemci bilgisayarda saklanan, istemciyi belirli kılmaya yönelik verileri  saklandığı küçük dosyalardır.

- Bir çerez şu şekilde oluşturulur:
  
  ```php
  setcookie("isim", "değer", $sure);
  ```
  
  Çerez "sure" ânı gelene kadar kullanılabilir; buraya saniye cinsinden değer verilir. Misal, oluşturulduktan sonra bir saat saklı kalması istenen bir çerez için bu süre şu şekilde yazılabilir: `time() + (60*60)`

- Çerez oluşturulurken sunucu konumu (?) (‘domain’), güvenlik seçeneğinin etkin olup, olmadığı belirtilebilir.

- Bir çerezin son kullanma târihine geçmiş târih değeri atanırsa çerez sayfa çalıştırıldığında (?) silinmek için kodlanır (?)

- Bir oturum dosyası (‘session’) oluştururken ön tanımlı değişken olan ‘$_SESSION’ dizisine yeni bir değer eklenir; fakat oturum dosyası kullanmak istiyorsak bunu sayfanın başında veyâ kullanmadan önce herhangi bir kod satırında belirtmeliyiz; o da şu kod ile yapılıyor: `session_start();`

##### Bâzı önemli çerez ve oturum yöntemleri:

- `session_regenerate_id()` : Geçerli oturum kimliğini yenisiyle değiştirir; oturum içeriğini korur. İstenilirse ikinci parametre olarak veyâ elle 'delete_old_session' parametresine 'false' verilerek eski oturum bilgisi silinebilir. Bu yöntem geriye işlemin başarılı olup, olmadığı bilgisini döndürür. 

## DOSYA AÇMA - KAPAMA

- `fopen()` yöntemi kullanılır. İlk parametre dosya adresidir; ikinci parametre ise dosya açma modudur.

- Eğer dosya adresi kısmında yalnızca dosyanın adı yazılırsa (uzantısıyla berâber yazılmalıdır) PHP dosyayı PHP sayfasını bulunduğu dizinde arar.

- Dosya açma modları şunlardır:
  
  1. `r` : ‘read’ (okuma) kelîmesini ifâde eder; dosyayı okumak için açarken kullanılır.
  
  2. `w` : ‘write’ (yazms) kelîmesini ifâde eder; dosyayı yazmak için açarken kullanırız; eğer belirtilen adreste bir dosya varsa, dosyaya veri yazdığımızda içindeki tüm bilgiler gider.
  
  3. `a` : ‘append’ (ekleme) kelîmesini ifâde eder; dosya yazma modunda açılır, fakat imleç dosya sonunda olduğu için dosyada dahs önce bulunan değerler silinmez.
  
  4. `x` : Verilen adreste bir dosya varsa ‘false’ değeri döndürür; diğer durumda dosya yazma modunda oluşturulur
  
  5. `r+` : Dosya hem okuma, hem de yazma modunda oluşturulur, imleç dosya başındadır
  
  6. `w+` : Dosya hem okuma, hem de yazma modunda açılır; imleç dosya başındadır, belirtilen adreste dosya varsa, içindeki veriler silinir
  
  7. `a+` : Dosya hem okuma, hem de yazma modunda açılır; imleç dosya sonundadır, yazılan değerler dosya sonuna eklenir; dosya yoksa oluşturulur

##### Bâzı temel fonksiyonların temel yapısı:

- `fread($dosyaAkisi, $uzunluk)` : Dosyayı ikili veri (binary) olarak okur. 

- `filesize($dosyaIsmi)` : Dosya adresi alır, dosya büyüklüğünü byte cinsinden geri döndürür.

- `fgets($dosyaAkisi)` : Dosyadan bir satır okunur.

- `feof($dosyaAkisi)` : İşâretçinin (imlecin) dosya sonunda olup, olmadığını kontrol eder.

- `fwrite($dosyaAkisi, $veri[, $uzunluk])` : Dosyaya veri yazmak için kullanılır. Veri, metîn olmalıdır; `$uzunluk` parametresi belirtilmeyebilir. Belirtilirse, belirtilen uzunluk kadar veri yazıldıktan sonra işlem durdurulur; verinin boyutu uzunluktan kısaysa, veri yazılınca durulur.

- `fclose($dosyaAkisi)` : Akışı verilen dosyayı kapatır.

- `fseek($dosyaAkisi, $hedef, $mevki)` : Dosya üzerindeki imleci başka yere taşır. `$hedef` kadar bayt sonrasına dosya imleci götürülür; fakat `$mevki` kısmında şu bu `$hedef` miktarının nereden itibâren sayılmaya başlanacağı belirtilebilir; belirtilmezse dosya başından itibâren `$hedef` kadar sonrasına gidilir. `$mevki` için şu değerler verilebilir:
  
  1. `SEEK_SET` : Bulunulan konum dosya başı olarak değerlendirilir.
  
  2. `SEEK_CUR` : Bulunulan konum, imlecin mevcut konumu olarak değerlendirilir.
  
  3. `SEEK_END` : Bulunulan konum dosya sonu olarak değerlendirilir.

- ..

## XML ve JSON ile ÇALIŞMAK

- JSON dosyaları `json_decode()` yöntemiyle parçalanıp, okunabilir

- Bir dosyaya JSON verisi yazmak için ise `json_encode()` yöntemine verileri bir dizi şeklinde verebiliriz; yöntemin ikinci parametresi olan `$flags` parametresi dâhilinde `JSON_PRETTY_PRINT` yazılırsa  veriler hizalı şekilde dosyaya yazdırılır.

## VERİTABANI ve MYSQL

- PHP ile en çok kullanılan veritabanlardan birisi MySQL'dir.

- MySQL veritabanıyla iki farklı şekilde bağlantı kurulabilir.
  Birincisi: `mysqli_connect()` yöntemiyle bağlantı kurulur. Parametreleri sırasıyla şöyledir:
  
  1. `$username` : MySQL hesâbı kullanıcı ismi
  
  2. `$password` : MySQL hesâbı kullanıcı şifresi
  
  3. `$database` : Bağlanılmak istenen veritabanı
  
  4. `$port` : Bağlantının kurulacağı (yanî MySQL servisinin istemci isteklerine açık olduğu) port numarası
  
  5. `$socket` : ...

- Bağlantı kurulduktan sonra `mysqli_connect_errno()` yöntemiyle bağlantının başarılı olup, olmadığı kontrol edilebilir. Bu yöntem bağlantı hatâ sayısını döndüren bir fonksiyondur.

- `mysqli_close()` yöntemiyle bağlantı kapatılır. Bu fonksiyon içerisine bağlantı linkini alır.

- `mysqli_query()` yöntemiyle MySQL sorgusu gönderilebilir; sorgu metîn şeklinde olmalıdır. İlk parametre bağlantı değişkeni, ikincisi ise sorgu metnidir.

- Eğer gönderilmek sorgu metni birden fazla MySQL komutu içeriyorsa bu durumda `mysqli_multi_query()` yöntemi kullanılmalıdır. İlk iki parametre sırası aynıdır.

- MySQL sorgu cümlesi (Statement) hâzırlamak için `mysqli_prepare()` yöntemi kullanılır. Bu yöntem ilk parametre olarak bağlantı değişkenini, ikinci parametre olarak ise sorgu cümlesini alır; fakat sorgu cümlesindeki değerlerin yerine soru işâreti (‘?’) yazılmış olmalıdır:
  
  ```sql
  INSERT INTO tablo(alan_1, alan_2, alan_3) VALUES (?, ?, ?);
  ```

- Hâzırlanan sorgu cümlesine değerleri koymak için `mysqli_stmt_bind_param()` yöntemi kullanılır. Bu yöntemin ilk parametresi ‘statement’ tipinde sorgu cümlesidir. İkinci parametresi ise sırasıyla her soru işâreti yerine gelecek değerlerin veri tiplerininin baş harfleridir(?)(metîn tipinde olmalıdır). Misaldeki alanların veri tiplerinin sırasıyla ‘string’, ‘string’ ve ‘int’ olduğunu düşünelim; bu durumda ikinci parametre şöyle olmalıdır:
  
      "ssi"
  
  Her bir harf bir değişkenin veri tipini ifâde ediyor. Veri tiplerinin sırası sorgu cümlesindeki değişkenlerin sırasıyla aynı olmalıdır. Kısaltmalar:
  
       s -> string
       i -> int
  
  Üçüncü parametresi ise sırasıyla değerler olmalıdır.

- Hâzırlanan ve değerleri de koyulan bu ‘statement’ tipindeki sorguyu çalıştırmak için `mysql_stmt_execute()` yöntemi kullanılır.

##### Bir Başka Bağlantı Kurma Yöntemi : PDO (PHP Data Objects):

- 12 farklı veritabanına bağlanabilmeyi sağlayan bir yapıdır.

- Bağlantı kurma:
  `connection = new PDO(...)`

- Bağlantı kapatma:
  `$connection = null;`

- ..

##### MySQL Veritabanından Veri Çekme:

- MySQL veritabanından iki şekilde veri çekilebilir:
  Veri çekmek için hâzırlanan sorgu cümlesi çalıştırıldıktan sonra dönen değer şu iki yönteme verilerek veriler alınır:
  
  1. `mysqli_fetch_row()` : Bu yöntem veriyi satır satır çeker. Her satırın sütununa dizi gibi indisle erişilebilir.
  
  2. `mysqli_fetch_assoc()` : Bu yöntem verilere sütun ismiyle erişmeyi sağlıyor.

- `mysqli_affected_rows()` yöntemiyle verilen bağlantı üzerinden çalıştırılan sorgularda kaç adet satırın etkilendiği öğrenilebilir.

- Bağlantıyı kapatma (bağlantı değişkeni \$connection olsun):
  `mysqli_close($connection);`

- MySQL veritabanından veritabanı seçmek için `mysql_select_db()` yöntemi kullanılır.

## NESNE YÖNELİMLİ PROGRAMLAMA

#### SINIF (CLASS), ÖZELLİK (PROPERTY) ve YÖNTEM (METHOD)

- Bilindiği üzere nesne yönelimli programlamanın temeli 'sınıf' yapısıdır. Sınıflar nesneler için nesne içerisinde hangi özelliklerin ('properties') ve hangi yöntemlerin ('methods') barındırılacağını belirten bir taslaktır.

- Nesneler ise sınıfların örnekleridir. Sınıf, özellik ve yöntem şu şekilde tanımlanır:
  
  ```php
  <?php
      class Student{
          // özellikler (properties):
          $number;
          $name;
  
          // yöntemler (methods):
          function requestForHomeWork(){
              //.;.
          }
      }
  ?>
  ```

#### SINIF ÖRNEĞİ (NESNE) OLUŞTURMA

- 'new' anahtar kelîmesinden sonra sınıf ismi bir fonksiyon gibi yazılır:
  
  ```php
  <?php
      $student = new Student();
      $student2 = new Student;
      // Eğer yapıcı yöntem bir parametre alıyorsa, ikinci tanımlama
      // yöntemi kullanılamaz!
  ?>
  ```

- Nesne tanımlandığında nesnenin yapıcı yöntemi çağrılır; dolayısıyla tanımlanan bir nesne aynı zamânda ilklendirilmiş ('initialized') olur; 'null' olmaz.

#### SINIF ÖZELLİKLERİNE ve FONKSİYONLARINA ERİŞİM

- Sınıf içerisinden sınıf yöntemlerine veyâ sınıf özelliklerine erişim için `$this` anahtar kelîmesi kullanılır.

- Sınıf dışından erişim için `->` işleci kullanılır:
  
  ```php
  $student->number;
  $student->requestForHomeWork();
  // Sınıf değişkeninin başında '$' işâreti olduğuna ve
      // sınıf özelliğinin ve yönteminin başında '$' işâreti
          // olmadığına dikkat ediniz 
  ```

> Geriye bir değer döndürmesi beklenmeyen birden fazla sınıf yöntemini ard arda kullanırken kolaylık olması açısından kullanılan bir yöntem vardır : **method chaining (yöntem zincirleme)**.
> 
> Öncelikle bu yöntemlerin sonuna `return $this` eklenerek geriye nesnenin kendisini döndürmesi sağlanır. Ardından yöntemler çalıştırılmak istenen sırayla peş peşe `->` işleciyle bağlanır, `$this` anahtar kelîmesi ve nesne ismi sadece en başta kullanılır:
> 
> ```php
> class windowOpener(){
>     /*.;.*/
>     public function showSidebar(){
>         //.;.
>         return $this;
>     }
>     public function showFooter(){
>         //.;.
>         return $this;
>     }
>     public function setDisplaySize(int $width, int $height=150){
>         //.;.
>         return $this;
>     }
>     // Bunları başka bir yöntem içerisinde kullanmak istiyoruz:
>     public function open(){
>         $this->setDisplaySize(350)->showFooter()
>         ->showSidebar();
>     }
> }
> ```

#### YAPICI YÖNTEM (CONSTRUCTOR)

- Sınıftan bir örnek üretildiğinde çağrılan yapıcı yöntemler PHP'de `function __construct(){/*..*/}` ile tanımlanır.

- Eğer herhangi bir yapıcı yöntem tanımlanmazsa hatâ oluşmaz; çünkü PHP'de varsayılan olarak çalıştırılan parametresiz bir yapıcı yöntem vardır.

- Yapıcı yöntemin imzası (parametrelerinin sayısı - sırası - veri tipi cihetinden tanımı) farklı olsa bile **sadece bir yapıcı yöntem tanımlanabilir**.

> Çoğu durumda yapıcı fonksiyona gönderilen parametreler sınıfın bir özelliğine atanır. Bu işlemi daha kolay yapabilmek adına PHP, 8.0 sürümüyle yeni bir özellik eklendi : **constructor promotion:**
> 
> ```php
> <?php
>     class Student{
>         function __construct(private $number, private $name){
>             // Herhangi atama ifâdesi yazmaya gerek yok.
>         }
>     }
> 
> ?>
> ```
> 
> Yukarıdaki koda göre; sınıfın 'private' erişim belirtecinde `$number` özelliği ve `$name` özelliği vardır; yapıcı fonksiyona gönderilen parametreler bu özelliklere atanır.
> 
> ****!**** Bu özellikleri yapıcı fonksiyon dışında tanımlamak isterseniz, hatâ oluşur.
> 
> Bu işlev, özellik bazlıdır ve başına 'private' yazmadığınız özellikler için bu işlev aktif olmaz.

#### YIKICI YÖNTEM (DESTRUCTOR)

- Yıkıcı yöntem sınıftan üretilmiş bir nesne silindiğinde çağrılır.
- `function __destruct(){/*..*/}` ile tanımlanır.
- Yıkıcı yöntemler herhangi bir parametre almazlar.
- Sadece bir yıkıcı yöntem tanımlanabilir.

#### ERİŞİM BELİRTEÇLERİ

- Erişim belirteci özelliğe veyâ yönteme nerelerden erişilebileceğini denetim altında tutmak için kullanılan, nesne yönelimli programlamanın temel yapıtaşlarından birisidir.

- PHP'de erişim belirteçleri özellik veyâ yöntem (fonksiyon) tanımının en başına yazılır: `public int $tamsayi`

- PHP'de üç erişim belirteci mevcuttur:
  
  1. `public` : Herhangi bir erişim kısıtlamasının olmadığı erişim belirtecidir. Varsayılan erişim belirteci budur.
  
  2. `private` : Bu erişim belirteciyle tanımlanan özellik ve fonksiyonlara sadece sınıf içinden erişim sağlanabilir.
  
  3. `protected` : Bu erişim belirteciyle tanımlanan özellik ve fonksiyonlara sınıf sınıf içinden ve bu sınıftan türemiş alt sınıfların içinden erişim sağlanabilir. Yabancı sınıflardan erişim sağlanamaz.

- Özellik / fonksiyon tanımında herhangi bir erişim belirteci belirtilmediğinde, varsayılan erişim belirteci olan 'public' erişim belirteci uygulanır.

#### ALT SINIF OLUŞTURMA ve MİRAS (INHERITANCE)

- Bir sınıf başka bir sınıfın alt sınıfı olarak tanımlanabilir, bu durumda üst sınıftaki özellikler ve yöntemler alt sınıfa da eklenmiş olur.

- PHP'de yalnızca **bir sınıftan miras alınabilir**.

- Bu işlev için `extends` anahtar kelîmesi kullanılır:
  
  ```php
  <?php
  require 'Person.php';
  class Student extends Person{
      //.;.
  }
  ?>
  ```

- Üst sınıftaki bir özellik alt sınıfa da geçtiğinden üst sınıfta tanımlanan bir özelliğe `$this` anahtar kelîmesiyle erişilebilir (statik sınıf özellikleri hâriç).

- Eğer alt sınıfta bir yapıcı yöntem tanımlanmazsa sınıf örneği oluşturulurken üst sınıfın yapıcı yöntemi kullanılır.

> **NOT :** Üst sınıfın parametre almayan yapıcı yöntemi olmadığını ve alt sınıfın parametre alan bir yapıcı yöntemi olduğunu düşünelim. Bu durumda alt sınıfın yapıcı yöntemi içerisinde üst sınıfın yapıcı yönteminin çalıştırılması zorunlu değildir (misal, Java'da zorunludur). Bu, gözden kaçırıldığında hatâya sebebiyyet verebilir:
> 
> ```php
> <?php
> class Person{
>     public string $name;
>     public function __construct(string $name){
>         $this->name = $name;
>     }
> }
> class Student extends Person{
>     public int $number;
>     public function __construct(int $number){
>         $this->number = $number;
>     }
> }
> 
> $student1 = new Student();
> // Buraya kadar uygulama hatâ vermez.
> echo "İsim : ".$student1->name;// !!! HATA
> // $name özelliği ilklendirilmediğinden uygulama hatâ verir.
> ?>
> ```

- Eğer alt sınıf içerisinden üst sınıfın yapıcı yöntemini çağırmak istiyorsak, sınıf özelliğine erişim belirteci olan `$this` belirtecini kullanamayız, çünkü bu işleç mevcut sınıfa işâret eder. Bunun için üst sınıf işleci şu şekilde kullanılmalıdır:

- ```php
  <?php
  //.;.
  class Student extends Person{
      public int $number;
      public function __construct(string $name, int $number){
          parent::__construct($name);
          $this->number = $number;
      }
  }
  ?>
  ```

- ..

#### SÂBİTLERİN (CONSTS) KULLANIMI ve SÂBİT FONKSİYON TANIMLAMA

- Fonksiyonel programlama kullandığımızda, PHP'de sâbit tanımlamanın birkaç yolu vardır; fakat bu sâbitler sınıfın bir üyesi değildir. Bu sâbitler sayfanın tümünde geçerlidir ve sınıfın bir özelliği olarak çağrılamazlar; hattâ sınıf içerisinde `const` anahtar kelîmesiyle sâbit tanımlayamazsınız; ancak bir fonksiyon içerisinde `define` yöntemini çağırarak sâbit tanımlayabilirsiniz, ama bu da sayfaya âit bir sâbit olur, ne bu sınıfın bir örneği üzerinden, ne de alt sınıf örneği üzerinden sâbite erişemezsiniz. 

- Sınıfâ âit sâbit yöntem tanımlanabilmesi için `final` anahtar kelîmesi kullanılmalıdır. Bu, kelîme eğer varsa erişim belirtecinden sonra, `function` ifâdesinden önce yazılır:
  
  ```php
  <?php
  class Person{
      function __construct($name){/*/.,.*/}
      public final function showID(){/*.;.*/}
  }
  ?>
  ```

- PHP'de sınıf özelliğini `final` anahtar kelîmesiyle tanımlayamıyorsunuz. Değiştirilemeyen bir özellik tanımlamak için PHP 8.1 ile gelen `readonly` işlevini değişken üzerinde uygulamalısınız.

### ÇOK ÇEŞİTLİLİK

##### Üzerine Yazma (Overriding)

- Üst sınıfta tanımlanan bir yöntemin (method) alt sınıfta yeniden tanımlanmasına 'overriding' denir ve nesne yönelimli programlamanın önemli bir parçasıdır. PHP'de bunu yapabilmek için fonksiyonu alt sınıfta yeniden tanımlamak kâfîdir.

> ***NOT :*** Üst sınıfta tanımlanan 'abc' yöntemi alt sınıfta yeniden tanımlandığında `this->abc` kodu yeniden tanımlanan yönteme işâret etmektedir. Üst sınıftaki yöntem çağrılmak istendiğinde şu kod yazılmalıdır:
> 
> ```php
> class A{
>     function abc(){/*.;.*/}
> }
> class B extends A{
>     function abc(){/*...*/}
>     function abcFromUpperClass(){
>         parent::abc();
>     }
> }
> ```

- Eğer üst sınıfta tanımlanan bir yöntemin alt sınıfta yeniden tanımlanmasını önlemek istiyorsak, o sınıfı `final` anahtar kelîmesiyle tanımlamalıyız. 

- ..

### VERİ TİPİ BELİRTİLEREK TANIMLANAN ÖZELLİK (TYPED PROPERTY)

- PHP'de özellik tanımlarken veri tipi tanımlanabilir:
  
  ```php
  class Student{
      public int $number = 0;
  }
  ```

- Bu şekilde tanımlanan özelliklere 'typed property' (tiplendirilimiş özellik) denir.

> **NOT :** Sınıf içerisinde veri tipi belirtilmeden tanımlanan özelliklere varsayılan olarak 'null' değeri atanır; dolayısıyla bu değişkenler 'ilklendirilmiş' olur. Fakat tip belirtilerek atanan özelliklerin varsayılan değeri 'null' değildir; dolayısıyla bu değişkenler ilklendirilmemiş olur. Dolayısıyla bu, ileride hatâya sebebiyyet verebilir. Bu sebeple veri tipi belirtilmiş özelliklere en başta 'null' değeri atanmalıdır:
> 
> ```php
> class Student{
>     public $projectType;
>     public int $selectedField;
>     //.;.
> }
> 
> $student1 = new Student();
> if($student1->projectType == null)
>     echo "Öğrencinin görev aldığı bir proje yok"."<br>";
> if($student1->selectedField== null){// !!! HATÂ 
>     //.;.
> }
> #Hatâ oluşmaması için özellik tanımı şöyle yapılmalı:
> # public int $selectedField= null;
> ```

#### SOYUT SINIF (ABSTRACT CLASS) ve SOYUT YÖNTEM (ABSTRACT METHOD)

- Soyut sınıflar, kendisinden miras alan sınıflara hangi işin yapılacağını ve sınıf örneğinin (nesne) hangi özellikleri taşıyacağını belirtmek için kullanılan bir yapıdır.

- PHP'deki Soyut sınıfların iki temel özelliği vardır:
  
  1. Soyut yöntem barındırabilmesi
  
  2. Kendisinden bir örnek (nesne) oluşturulamaması

- Soyut sınıf `class` ifâdesinden önce gelen `abstract` anahtar kelîmesiyle tanımlanır:
  
  ```php
  abstract class Car{/*.;.*/}
  ```

- Soyut sınıflar soyut yöntem barındırmak için kullanılsa da, soyut bir yöntem barındırmayabilirler (Java'da en az bir soyut yöntem barındırmalıdırlar).

##### Soyut Yöntem (Abstract Method)

- Soyut yöntemler bir yöntemin imzasını tanımlamak, fakat içeriğini doldurma işini alt sınıflara bırakmak için kullanılan bir yapıdır. Bu yapı, bir sınıfa bir işlemi yapmasını şart koşmak, fakat bu işlemin nasıl yapılacağının kodlanmasını o sınıfa bırakmak için kullanılır.

- Soyut yöntemlerin iki temel özelliği vardır:
  
  1. Yöntem (fonksiyon) gövdesi barındırmazlar
  
  2. Yalnızca soyut bir sınıfın içinde tanımlanabilirler

- Soyut yöntemler tanımlandığı sınıfta herhangi bir fonksiyon gövdesi barındırmazlar, sadece yöntem imzasını tanımlarlar.

- `function` ifâdesinden önce gelen `abstract` anahtar kelîmesiyle tanımlanır:
  
  ```php
  abstract class Car{
      abstract function showEngineInfo();
  }
  ```

- Bir sınıf soyut bir yöntem barındırırsa, bu sınıftan miras alan ve soyut olmayan tüm alt sınıflar bu yöntemin gövdesini yazmak zorundadır. Bu yapılırken `abstract` anahtar kelîmesi kullanılmamalıdır:
  
  ```php
  <?php
  require 'Car.php';
  class Fiat_Linea extends Car{
       function showEngineInfo(){
          echo "1.4 Fireturbo engine";
      }   
  }
  ?>
  ```

- Bir soyut sınıftan miras alan bir sınıf, ya üst sınıftaki tüm soyut yöntemlerin gövdesini yazmak zorundadır, yâ dâ kendisi bir soyut sınıf olmak zorundadır.

- Tahmîn edilebileceği üzere soyut bir sınıfın erişim belirteci `private` olamaz.

- 

#### ARAYÜZ (INTERFACE)

- Bir sınıfın belli bir şablonu uygulamasını sağlamak ve bu şablonu uyguladığını işâretlemek maksadıyla kullanılır.

- Arayüzler soyut yöntemlerdeki gibi içi doldurulmamış yöntemler barındırırlar.

- Arayüzü uygulayan sınıf bu yöntemlerin içini doldurmak zorundadır.

- Soyut sınıfların aksine, arayüzler içerisinde herhangi bir özellik (property) barındıramazlar, içi dolu bir fonksiyon barındıramazlar.

- Arayüz tanımlamak için `interface` anahtar kelîmesi kullanılır. Bir sınıfa arayüz eklemek için ise, sınıf tanımından sonra, süslü parantezi açmadan evvel `implements` anahtar sözcüğü ve arayüz ismi yazılır:
  
  ```php
  interface Connection{
      function connect();//Arayüz içerisinde fonksiyon tanımlanırken
                          //'abstract' anahtar kelîmesi kullanılmaz.
  sadece içi doldurulmaz ve sonuna noktalı virgül konur
  }
  class USB implements Connection{
      function connect(){
          echo "USB bağlantısı kuruldu<br>";
      }
  }
  ```

- Arayüz, içerisinde hiçbir fonksiyon (yöntem) barındırmayabilir.

- Bir sınıf birden fazla arayüzü uygulayabilir; bu durumda arayüz isimlerinin aralarına virgül konmalıdır:
  
  ```php
  interface IConnection{/*...*/}
  interface IDeviceCompatible{/*...*/}
  class USB implements IConnection, IDeviceCompatible{/*...*/}
  ```

- Arayüzün tüm fonksiyonlarının (yöntemlerinin) belirteci `public` olmak zorundadır.

- Arayüzü uygulayan sınıflara 'concrete class' denir.

- ..

#### SADECE OKUNABİLİR ('READONLY') ÖZELLİK

- PHP'de 'sadece okunabilir özellik' işlevi **8.1 versiyonuyla tanıtıldı**. Buna göre bir özelliğinin sadece bir kez değer alması sağlanabilir:

- Bu işlev sadece veri tipi belirtilmiş özellikler (**typed properties**) de kullanılabiliyor. Bu işlevi bir özelliğe uygulamak için özelliğin tanımında veri tipinden evvel `readonly` anahtar kelîmesi yazılır.
  
  ```php
  class Student{
      public readonly int $number;
  }
  ```

- Bu işlev 'constructor promotion' işlevi kazandırılmış bir parametreye de uygulanabilir:
  
  ```php
  class Student{
      function __construct(private readonly int $number){
          //.;.
      }
  }
  ```

> **NOT :** Bu işlev temel veri tipi dışında bir tipte tanımlanan bir özelliğin herhangi bir özelliğinin değişmeyeceğini söylemiyor. Misal:
> 
> ```php
> class Student{
>     public readonly ExamInfo examResult;
>     public function __construct(private readonly int $number,
>         readonly string $name, ExamInfo $examResult){
>         $this->examResult = $examResult;
>     }
> }
> 
> class ExamInfo{
>     public string lessonName = "";
>     private int $score = -1
>     public function __construct(string $lessonName){
>         $this->lessonName = $lessonName;
>     }
> }
> 
> $student1 = new Student(177, "Mehmet Akif", new ExamInfo("PC"));
> $student1->examResult->lessonName = "Matematik";// Hatâ vermez
> $student1->examResult = new ExamInfo();/// !!! HATA
> ```

..

#### NOTLAR

> **NOT - 1)**
> 
> Eğer sınıfın bir özelliği `unset` ile silinirse, daha sonra o özelliğe erişilemez, erişilmeye çalışılırsa hatâ alınır.

..
