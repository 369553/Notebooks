# FastAPI

## GENEL BİLGİLER

- FastAPI, API geliştirme sürecinin hızlı olmasını sağlayan, Python için bir API geliştirme kütüphânesidir.

- FastAPI, MIT lisansıyla sunulan açık kaynak kodlu, ücretsiz bir kütüphânedir.

- FastAPI, API geliştirilirken, metot parametrelerinin değişkenleştirilmesi, gelen bağlantı adreslerinin ilgili fonksiyonlarla eşleştirilmesi, dinamik API dökümantasyonunun sağlanması gibi pek çok özellik sunar.

- FastAPI kütüphânesini yüklemek için `pip install "fastapi[standard]"` kodunu veyâ `pip install fastapi` kodunu çalıştırın. Birinci kod, kütüphânenin bir takım varsayılan ayarlamalarla gelmesini sağlıyor.

- FastAPI, 'pydantic', 'starlette' ve 'uvicorn' gibi kitâplıklar kullanmaktadır. Sunucu servisi olarak `uvicorn` kullanmaktadır; modellerin genelleştirilmesi için `pydantic` kitâplığını kullanmaktadır.

- FastAPI, pek çok API kütüphânesinde olduğu gibi, bildirim (notasyon) bazlı bir yaklaşım sunmaktadır; Python'da bu yaklaşım bir fonksiyonu başka fonksiyonla sarmalama anlamına gelen 'decorator' yapısına denk düşmektedir. Fonksiyonların hangi bağlantılarla eşleşeceğini belirtmek için 'decorator' yapısı kullanılır.

- FastAPI ile kodunuzu yazıp, kaydettikten sonra sunucunun yeniden başlatılmasına veyâ başka bir ayara gerek kalmadan API'niz otomatik olarak yenilenir.

- **API sunucunuz varsayılan olarak 8000 portunda çalışmaktadır**.

- FastAPI dinamik ve otomatik dökümantasyon üretmektedir. Fast API projenizin dökümantasyonuna ulaşmak için ilgili port numarasından sonra `/docs` ekleyin. Geliştirme ortamında varsayılan olarak şudur : `http://127.0.0.1:8000/docs`

- OpenAPI şemasına ulaşmak için ise varsayılan olarak şu adres kullanılır:
  `http://127.0.0.1:8000/openapi.json`

- Yazar : Mehmet Âkif SOLAK

## API HAKKINDA TEMEL BİLGİLER

- API, bilhassa uygulamaların birbirleriyle haberleşmesi için ve sunucu-istemci haberleşmesi için kullanılan bir protokolvâri standarttır.

- Basit olarak, hangi adrese hangi iletişim metoduyla hangi veri verildiğinde sunucunun ne yapacağını, ne döndüreceğini belirten bir standarttır. Bu standart sâyesinde hem kullanıcı ve uygulamalar sunucuyla rahat iletişim kurar, hem de sunucu tarafında isteklerin ele alınması için hangi fonksiyonların çalışacağı ve içerisinde ne yapılacağı bilgisi kolayca ele alınır.

- API'ler genellikle HTTP(S) istekleriyle berâber çalışır.

- HTTP protokolü üzerindeki bâzı iletişim usûlleri şunlardır:
  
  - **GET** : Bu yöntem sunucudan veri istendiğinde kullanılır. Gönderilen sorgu paramereleri sayfa adresine yazılır. Sunucu tarafından sayfa adresinden alınır. Sayfa adresinde istenilen parametre ve değer ikilisi yazılabildiğinden ötürü, GET parametreleri ‘script injection’ ve ‘sql injection’ türü saldırılara açık bir yöntemdir. Sunucu tarafında alınan birkaç basit tedbirle bu saldırılardan korunulabilir. Gönderim yöntemi ‘GET’ olduğunda gönderilen parametre ve değeri sayfa adresine eklenir, misal: www.search.com?key=girilen_deger
  - **POST** : Bu yöntemde sunucuya gönderilen parametreler sunucuya gönderilen isteğin (‘request’) gövdesine (‘body’) yazılır; bu istek şifrelenip, paketlenerek gönderildiyse -ki HTTPS protokolünde böyle yapılır- gönderilen parametreleri paket trafiğini izleyen birisi göremez (şifreyi kırması gerekir). Bu yöntem genellikle kullanıcı adı ve şifresi gibi önemli bilgiler gönderilirken kullanılır.
  - **PUT** : Bu yöntem, sunucudaki bir verinin değiştirilmesi / güncellenmesi amacıyla kurulan iletişimde kullanılır.
  - **DELETE** : Sunucudaki bir verinin silinmesini istediğimiz durumda kullanılır.

- Bir API kitâplığından beklenen şey, gelen isteklerin tipine, bağlantı adresine bakarak, hangi fonksiyonla eşleşeceğini otomatik olarak ayarlaması ve eşleştiği fonksiyon içerisinde ilgili parametrelerin fonksiyona verilebilmesi, gönderilen parametre ve veriler için format, değer aralığı, veri tipi gibi yapılandırma atanmasını sağlanması gibi kolaylıklardır.

- Şu anda API'lerde veriler çok büyük çoğunlukla JSON formatında iletilmektedir. API'yi kullanabilmek için API'nin hangi formatta veri döndürdüğünü ve kabûl ettiğini bilmek gerekir.

- ..

## GENEL BAKIŞ

- `fastapi` : FastAPI uygulamasını temsil eden sınıf, isteğin sorgu parametresini, adres parametresini, gövde parametresini, çerezleri, formları, dosyaları ve daha fazlasını temsil eden sınıflar bu paket altında bulunur.
- `fastpi.requests` : İstemciden gelen sorgu isteğini temsil eden sınıf bu başlık altında bulunur.
- ``fastapi.responses` : İstemciye döndürülen cevâbı temsîl eden sınıflar bu paket altındadır.
- `fastapi.datastructures` : Veri tiplerini temsil eden sınıflar buradadır.
- `fastapi.exceptions` : Hatâ istisnalarını temsil eden sınıflar buradadır.
- `fastapi.security` : İstemci doğrulama ve yetkilendirme gibi işlemler için gerekli güvenlik elemanları için sınıflar bulunmaktadır.
- `fastapi.exception_handlers` : İstisnâları ele almak için gerekli yapıları sağlar.
- `fastapi.applications` : Uygulama içerisindeki uygulama tarzındaki yapıları sağlayan sınıflar burada bulunmaktadır.
- `fastapi.param_functions` : İstemciden gelen parametrelerin özü olan sınıflar buradadır.
- `fastapi.encoders` : Bâzı iletişim yapıları bu kitâplık altındadır.

## ADIM ADIM KAPSAMLI API TASARIMI

- FastAPI uygulaması yazarken evvelâ uygulamayı ifâde eden nesneyi oluşturmalısınız:
  
  ```py
  from fastapi import FastAPI
  api = FastAPI()
  ```

- Bundan sonra, bildirimlerle bağlantılar tanımlanır.

- Bundan sonraki örneklerde uygulama isminin `api` olduğunu unutmayın..

- Yukarıdaki kodu bir dosyaya kaydedin, `api.py` ismiyle kaydettiğimizi düşünelim.

- Bu durumda komut satırında FastAPI'yi yüklediğiniz çalışma ortamındayken (eğer bir çalışma ortamı oluşturmadıysanız, bir şey yapmanıza gerek yok), dosyanın bulunduğu dizinde açın ve şu komutu çalıştırın:
  
  ```shell
  fastapi dev api.py
  ```

- Bu, kodunuzu geliştirme ortamında başlatmaktadır. Arayüzünüzü (API) gerçek ortamda yayına alırken `fastapi run api.py` şeklinde yazıp, çalıştırmalısınız.

- ..

#### GET İsteğini Ele Alma

- GET isteği, sunucudan veri istendiği ve sunucuya hassas veri gönderilmediği durumu ifâde etmektedir.

- GET isteğindeki ne verisi istendiği **yalnızca** bağlantı adresi üzerinden belirtilir.

- Bir bağlantı adresini bir fonksiyonla şu şekilde eşleştirilir:
  
  ```py
  @api.get("/")# Buradaki 'get' bağlantı tipini belirtmektedir
  def root():
      return {"Hoşgeldiniz" : "Burası Şehirler API'si"}
  ```

- Benzer şekilde, API'nin hangi ülke şehirleri hakkında bilgi sağladığını belirten bir bağlantı adresi daha yazmak istersek;
  
  ```py
  @api.get("/apiInfo")
  def getInfo():
      json = {}
      json["usableCountries"] = ['Türkiye']
      return json
  ```

#### Adres Parametreleri

- Bağlantı adresi parametresi, adresin değişkeni ifâde ettiği belirtilen kısmı için kullanılan bir deyimdir.

- Misal, her şehir için ayrı ayrı bağlantı adresi tanımlamak istemediğimizden ötürü adresin bir kısmını bir parametre olarak tanımlamalı ve ilgili kısma denk düşen yerin hedef fonksiyona parametre olarak verilmesini sağlamalıyız.

- Bunun için adres parametresi ismi süslü parantez içerisinde yazılır:
  
  ```py
  @api.get('/cities/{plateCode}')
  def getCityByPlateCode(plateCode):
      return {"plateCode" : plateCode}
  ```

- Yukarıdaki kodda adresin `/cities/` kısmından sonra gelen kısmı 'plateCode' isimli bir değişken olarak değerlendirilmekte ve bu değişken `getCityByPlateCode()` fonksiyonuna parametre olarak verilmektedir.

- Bu parametre için tip belirtebilirsiniz:
  
  ```py
  @api.get('/cities/{plateCode}')
  def getCityByPlateCode(plateCode: int):
      return {"plateCode" : plateCode}
  ```

- Böyle yapıldığında yalnızca sayısal değerler plaka kodu ('plateCode' parametresi) olarak verilebilir.

- İleride adres parametresi için değer aralığı belirtme işlemi gösterilecek inşâAllâh.

- `fastapi`'nin zayıf yönü diğer API kitâplıklarında vâr olan (misal, Django, Flask) bir özelliğin desteklenmiyor olmasıdır. Bu özellik aynı adres parametresiyle gelen verilerin farklı veri tipleri sâyesinde farklı fonksiyonlarla ele alınabilmesidir. Misal, hem yukarıdaki fonksiyonu, hem de aşağıdaki kodu aynı API içerisinde doğru şekilde çalıştıramazsınız (ayrı fonksiyonlar olarak olmuyor):
  
  ```py
  @api.get('/cities/{cityName}')
  def getCityByName(cityName: str):
      return {"cityName" : cityName}
  ```

- Eğer şehir ismiyle erişilen fonksiyonu üste yazarsanız, sayısal olarak gelen adres parametresi metîn olarak ele alınır ve alttaki fonksiyonunuz çalıştırılmaz; yanî gönderdiğiniz plaka kodu şehir ismiymiş gibi yorumlanır. Eğer bu fonksiyonu alta yazar ve şehir ismiyle şehir bilgisine erişmeye çalışırsanız, gelen sorguyu ilk fonksiyon ele alır ve gönderdiğiniz şehir isminin `int` tipine çevrilememesi sebebiyle hatâ alırsınız. Evet, bu hiç iyi değil. Aynı bağlantı noktasında ikisini de ele almanın yolu, gelen adres parametresinin sayı olup, olmadığına fonksiyon içerisinde karar vererek gönderilen değerin şehir ismi mi, plaka kodu mu olduğunu tespit eden kodu yazmanızdır:
  
  ```py
  @api.get('/cities/{nameOrPlateCode}')
  def getCityByNameOrPlateCode(nameOrPlateCode: str):
      json = {}
      plateCode = None
      try:
          plateCode = int(nameOrPlateCode)
      except ValueError:
          print("s")
      if plateCode is None:
          json["name"] = nameOrPlateCode
      else:
          json["plateCode"] = plateCode
      return json
  ```

- Yine de statik adres parametrelerini farklı fonksiyonlar da ele alabilirsiniz; fakat kapysayıcı olanı üste yazmalısınız (misal, 'current' ifâdesinin bir önce yazdığımız `getCityByNameOrPlateCode` fonksiyonunu tetiklememesi ve bu fonksiyona girmesi için bu fonksiyonu üste yazmalısınız):

- ```py
  def getCurrentCityInfo():
      # Kullanıcının bağlandığı konuma göre mevcut şehri tespit et
      return {"current" : "Şu an bulunduğunuz şehir ..."}
  ```

> ***NOT :*** Bağlanma yöntemi ve adresi bire bir örtüşen iki fonksiyon tanımlanamaz.

##### Adres parametrelerinin kullanıcı tipler olarak ele alınması

- Adres parametreleri kullanıcı tanımlı tipler olarak da ele alınabilir.

- Adres parametreleri temel veri tipi dışındaki tiplerle de ifâde edilebilir. Misal, başkent isimlerini sunmak istiyorsak bunu şu şekilde yapabiliriz (en verimli yöntem olmayabilir, şu an sadece öğreniyoruz):
  
  ```py
  from enum import Enum
  class CapitalCity(str, Enum):
      urumchi = "urumchi"
      damascus = "damascus"
  @api.get('/capitals/{capitalCity}')
  def getCapitalCityByName(capitalCity: CapitalCity):
      json = {}
      isFound = False
      match capitalCity:
          case City.urumchi:
              json['city'] = capitalCity
              json['info'] = "Uygur topraklarının tutsak başkentidir"
              isFound = True
          case City.damascus:
              json['city'] = capitalCity
              json['info'] = "Özgür Suriye'nin başkentidir"
              isFound = True
      if isFound:
          return json
  ```

- Yukarıdaki kod, sadece iki başkent için çalışmaktadır; eğer farklı bir adresi gönderirsek, hatâ alırız; fakat hatâmız oldukça anlamlı bir hatâdır:
  
  ```json
  {
    "detail":[
    {
      "type":"enum",
      "loc":["path","capitalCity"],
      "msg":"Input should be 'urumchi' or 'damascus'",
      "input":"e",
      "ctx":{
        "expected":"'urumchi' or 'damascus'"
      }
    }]
  }
  ```

- Ayrıca hangi seçenekleri verebileceğimizi gösteren bir kılavuz da dökümantasyona otomatik olarak ekleniyor; fakat her başkent için enum tanımlamak verimli değil.

##### Adres parametrelerini sınırlandırmak

- Adres parametreleri yukarıdaki gibi kolayca tanımlanabilir; fakat `fastapi` içerisinde adres parametrelerini ifâde eden `Path` sınıfını kullandığımızda çok daha fazla yapılandırmaya ve özelliğe sâhip oluruz. Bunu verimli şekilde kullanmak için `typing` kitâplığı altındaki `Annotated` sınıfını kullanabiliriz.

- Misal, adres parametresi için bir değer aralığı belirtebiliriz, bu parametrenin işlevinin ne olduğunun dökümante edilmesi için bir başlık belirtebiliriz:
  
  ```py
  from typing import Annotated
  @api.get('/citiesByPlateCode/{plateCode}')
  def getCityByPlateCode(plateCode: Annotated[int, Path(
          title="plakaKodu, her ili simgeleyen münferid bir numaradır",
          gt=0)]):
      return {"plateCode": plateCode}
  ```

- Yukarıdaki fonksiyon 0'dan büyük numaralı plaka kodlarını kabûl etmektedir. Sıfır veyâ küçük bir plaka numarası girildiğinde gelen `Response` açıklayıcı bir mesaj da içermektedir:
  
  ```json
  {
   "detail":[
    {
     "type":"greater_than",
     "loc":["path","plateCode"],
     "msg":"Input should be greater than 0",
     "input":"-1",
     "ctx":
      {
       "gt":0
      }
    }
   ]
  }
  ```

- Ayrıca `Path` nesnesine verdiğimiz `title` parametresi sebebiyle şu adreste, bir ilgili adres uç noktası (end point) bilgisi arasında bir başlık ekleniyor:
  http://127.0.0.1:8000/openapi.json
  Fakat daha kapsamlı dökümantasyon oluşturmak için başka parametreler de var.

- `Path` nesnesini oluşturulurken `gt` gibi başka parametreler de verilebilir:
  
  - `lt` : 'less than' ('dan az) ifâdesinin baş harflerinden oluşmuştur. Verilen adres parametresinin verilen değerden az olmamasının istendiği durumda kullanılır.
  
  - `ge` : 'büyük veyâ eşit' ('greater or equal') demektir.
  
  - `le` : 'küçük veyâ eşit' ('less or equal') demektir.
  
  - `doc` : İlgili adres parametresinin açıklama metni bu parametreye verilebilir.
  
  - `examples` : İlgili parametrenin nasıl olacağıyla ilgili örnekler belirtmek için kullanılır. Örnekler liste olarak verilmelidir. Bunun amacı kullanıcıyı bilgilendirmek olduğu için metîn olarak verilmesi uygun olabilir.
  
  - `max_length` : Parametre tipi metîn veyâ metîn olarak değerlendirilen (misal, Enum) bir tip olarak işâretlenmişse bu parametre kullanılabilir.
  
  - `include_in_schema = True`: Bu parametre ilgili adres parametresinin dökümantasyonda listelenip, listelenmeyeceğini belirtmek için kullanılır. Eğer parametrenin dökümantasyonda listelenmesini istemiyorsanız `False` değeri vermelisiniz.
  
  - `description` : Adres parametresini ifâde eden bir açıklama eklenebilir.

> ***NOT :*** `typing.List` ile Java'daki generic List gibi bir yapı tanımlayabilirsiniz; yanî liste içindekilerin elemanların tipini belirtebilirsiniz; Python 3.9+ sürümlerinde bunun için `list[str]` yazılması kâfî...

- `pydantic` ile iç içe modeller oluşturabilirsiniz veyâ `pydantic`'in `HttpUrl` gibi hâzır modellerini de kullanabilirsiniz.

> ***NOT :*** Birden fazla tip belirtilebilen yazım şekli:
> `params : str | None = None` (Python 3.10+ sürümlerinde geçerlidir)
> Python 3.8+ için bu şöyledir: `params : Union[str, None]`
> Fakat FastAPI için `None` yazmak, o şeyin zorunlu olmadığını belirtmek için kâfî..

#### Sorgu Parametreleri

- Sorgu parametresi, bir adrese bağlanılırken aralık belirtme, yapılandırma belirtme, sorguyu sınırlandırma, cevâp formatı belirtme gibi amaçlarla gönderilen anahtar-değer ikilisi biçimindeki ziyâde parametrelerdir.

- Sorgu parametreleri bağlantı adresinde yer alan ve bağlantı adresinden hâriç tutulan parametrelerdir.

- Sorgu parametreleri `?` işâretinden sonra başlar ve `&` işâretiyle birbirlerinden ayrılırlar.

- Misal, `cities/1/?filtered=true&population=true` url adresinde soru işâretinden sonra belirtilen 'filtered' ve 'population' parametreleri sorgu parametresidir.

- FastAPI'da sorgu parametrelerini almak için fonksiyona parametre olarak belirtmeniz kâfîdir (bağlantı adresinde belirtmeyiniz):
  
  ```py
  @api.get('/cities/{cityName}')
  def getCityByName(cityName: str, filtered: bool)
      json = {}
      json['cityName'] = cityName
      if filtered:
          for (key, val in kwargs):
              json[key] = val
      else
          pass# Şehrin tüm bilgilerini eklediğimizi düşünelim..
      return json
  ```

- Pek çok sorgu parametresini kolayca ele almak için tüm parametreyi bir metîn olarak alıp, fonksiyon içerisinde ayrıştırabilirsiniz; fakat bu durumda SQL injection saldırısına karşı önlem almalısınız: `q : str | None = None`

- Sorgu parametreleri doğal olarak bir metîndir. Bunları hedef tipe dönüştürmeye zorlamak için, fonksiyon parametresinde tip belirtimi yapabilirsiniz. Bu noktada FastAPI esneklik sunuyor. Misal, `bool` tipindeki bir sorgu parametresi için 'on', 'yes', 'true', '1', 't' ve True' değerlerini `True` olarak kabûl ediyor; bunların karşıt muadillerini de `False` olarak kabûl ediyor.

- Tıpkı adres parametresinde olduğu gibi, sorgu parametresi de bir `fastapi` sınıfıyla ifâde edilir : `Query`. Bu sınıfı kullanarak sorgu parametresi özelleştirilebilir:
  
  ```py
  @api.get('/citiesByPlateCode/{plateCode}')
  def getCityByPlateCode(plateCode: Annotated[int, Path(
          doc = "Plaka kodu ili münferiden simgeleyen bir numaradır",
          title="Plaka kodu", gt=0)],
          asShort: Annotated[bool, Query()] = None):
      json = {}
      json["plateCode"] = plateCode
      if asShort is not None:
          json["asShort"] = asShort
      return json
  ```

- Query sınıfının sık kullanılan bâzı özellikleri şunlardır:
  
  - `min_length` : Sorgu parametresinin asgârî uzunluğunu belirtmek için kullanılır.
  
  - `max_length` : Sorgu parametresinin Azamî uzunluğunu belirtmek için kullanılır.
  
  - `pattern` : Sorgunun bir düzenli ifâde örüntüsüyle belirtilmesi için kullanılır. Böyle yapıldığında, örüntüye uymayan sorgu kabûl edilmez.
  
  - `title` : Dökümantasyonda sorgu parametresini bir başlıkla belirtmek için kullanılır.
  
  - `description` : Sorgu parametresini açıklamak için kullanılır (dökümantasyon için..)
  
  - `alias` : Parametreye takma isim vermek için kullanılır. Bu, kullanıcının göndereceği parametrenin ismini belirlemektedir. Bunu ayrıca belirtmek istemenin bir sebebi Python'da tire ('-') gibi ifâdelerin değişken isminde bulunamaması ve bizim parametre ismimizin tire içermesini istememiz olabilir.
  
  - `deprecated` : Sorgu parametresinin ilerleyen sürümler kaldırılacağını belirtmek için kullanılır, `bool` bir değer verilmelidir.
  
  - `deprecation_message` : Sonraki sürümlerde yayımdan kalkacak parametre için bir açıklama eklemek amacıyla kullanılır.
  
  - `include_in_schema = True` : Bu parametre ilgili sorgu parametresinin dökümantasyonda listelenip, listelenmeyeceğini belirtmek için kullanılır. Eğer parametrenin dökümantasyonda listelenmesini istemiyorsanız `False` değeri vermelisiniz.
  
  - `doc` : Dökümantasyon için açıklama ekleyebilirsiniz.
  
  - `default` : Sorgu parametresi varsayılan değer belirtmek için kullanılır; fakat `fastapi` kitâplığını tasarlayanlar bunu yerine `Annotated` oluşturup, değer atamayı önermektedirler (yukarıdaki gibi).
  
  - `description` : Sorgu parametresini ifâde eden bir açıklama eklenebilir.

- `/cities/` adresine `q: Annotated[list[str] | None, Query()]=None` biçiminde ifâde edilen sorgu parametresi için `/cities/?q=population&q=location` değeri gönderilirse, parametre verisi `q=[population, location]` biçiminde alınır.

> ***NOT :*** `Query` parametrelerinin ele alınması büyük küçük harf duyarlıdır.

- Sorgu parametresinin zorunlu olmadığını belirtmek için o parametreye `None` atanması kâfîdir.

#### Adres ve Sorgu Parametreleri İçin İlâve Doğrulama Kontrollerinin Eklenmesi

- FastAPI'ın parametre için yaptığı doğrulamalardan önce veyâ sonra çalıştırılmasını istediğiniz doğrulama varsa `pydantic`'in `AfterValidator` ve `BeforeValidator` gibi sınıflarını şu şekilde kullanabilirsiniz:
  
  ```py
  q: Annotated[str | None,
      AfterValidator(dogrulama_fonksiyonu_ismi)] = None
  ```

> ***NOT :*** Eğer veritabanı gibi bir dış kaynağa bağlanıp, kontrol yapmanız gerekiyorsa, `BeforeValidator` ve `AfterValidator` yerine `fastapi` ile sunulan bağımlılık (dependency) yapısını kullanmanız daha uygun olur.

- İlgili doğrulama fonksiyonunda şunları yapabilirsiniz:
  
  - Gelen parametre üzerinde yapılan doğrulama işlemi başarılı olduysa, parametreyi doğrudan döndürebilirsiniz.
  
  - Gelen parametre doğru ise (doğrulama başarılıysa) ve parametrenin veri tipini dönüştürmek istiyorsanız, dönüştürülmüş parametreyi göndererek bunu yapabilirsiniz.
  
  - Gelen parametre yanlışsa, yanî fonksiyonda yaptığımız doğrulama menfî (olumsuz) bir sonuç ortaya çıkardıysa `raise` ile hatâ fırlatmalısınız.

- Misal, `getCityByNameOrPlateCode()` fonksiyonuna gelen adres parametresinin tamsayı olduğu durumda değer aralığını kontrol etmek istersek:
  
  ```py
  from pydantic import AfterValidator
  # Doğrulama fonksiyonu:
  def validatePlateCode(id):
      asInt = None
      try:
          asInt = int(id)
      except:
          return id
      if asInt <= 0 or asInt > 81:
          raise ValueError("Plaka kodu [0, 81] aralığında olmalıdır.")
      else:
          return asInt
  @api.get('/cities/{nameOrPlateCode}')
  def getCityByNameOrPlateCode(nameOrPlateCode: Annotated[str, Path(
          max_length=14
          ), AfterValidator(validatePlateCode)]):
      json = {}
      if type(nameOrPlateCode) is int:
          json["plateCode"] = nameOrPlateCode
      else:
          json["name"] = nameOrPlateCode
      return json
  ```

- Eğer `AfterValidator` içerisinde hatâ fırlatılırsa, bu hatâ istemciye döndürülür, diğer durumda `AfterValidator` fonksiyonundan dönen değer ilgili parametreye atanır; yanî plaka kodu gönderildiği durumda tip dönüşümü de yapılabilir.

> ***NOT :*** Doğrulamalar için model kullanmak çoğu zamân iyi bir çözümdür. Misal, e-posta doğrulamasını otomatik olarak, kolayca yapmak için parametre modelinizin ilgili alanının sınıfını `pydantic.EmailStr` olarak ayarlayabilirsiniz.

- ..

#### Sorgu Gövdesi (Request Body)

- Sorgu gövdesi, POST, PUT, DELETE gibi HTTP sorgu yöntemlerinde sunucuya veri göndermek için kullanılan; hemen hemen tüm sorgu yöntemlerinde sunucudan istemciye veri göndermek için kullanılan bir yapıdır. Veri, adres çubuğu üzerinde gözükmez; sorgu isteğiyle berâber gider. Eğer şifreleme varsa, şifreli olarak gider.

- İstemciden gelen sorgu gövdesini bir Python sınıfı olarak almak için `pydantic` kütüphânesini kullanabiliriz; `from pydantic import BaseModel` ile içeri aktarılan `BaseModel` üst sınıf olarak kullanılarak model sınıfı tanımlanabilir ve sorgu gövdesi bu sınıfın bir nesnesi olarak alınabilir; bunun için sorgu gövdesi, fonksiyon parametresi olarak yazılır:
  
  ```py
  from pydantic import BaseModel
  class City(BaseModel):
    plateCode: int
    name: str
    info: str
  
  #....
  
  @api.post('/cities/{plateCode}')
  def addCity(plateCode: int, city: City):
      json = {}
      json["info"]: "Şehir eklendi."
      json["city"] = city
  
  @api.put('/cities/{plateCode}')
  def addCity(plateCode: int, city: City):
      json = {}
      json["info"]: "Şehir bilgisi tazelendi."
      json["city"] = city
  ```

> ***NOT :*** FastAPI, çok karmaşık, müşahhas bâzı durumlar için GET parametresiyle sorgu gövdesi göndermeyi destekliyormuş.

- Gövde parametresi `fastapi` kütüphânesinin `Body` sınıfıyla ifâde edilir.

- `Body` sınıfının kullanışlı bâzı özellikleri şunlardır:
  
  - `doc` : Gövde için dökümantasyon verisi belirtilmek isteniyorsa, kullanılır.
  
  - `default` : Gövde için varsayılan değer verilmek istenmesi durumunda kullanılır.
  
  - `embed` : Gövdenin yalın olarak alınması yerine, bir anahtar değerle alınması isteniyorsa `True` verilmelidir. 2+ sayıda gövde parametresinin olduğu durumda gövde parametreleri otomatik olarak isimle beklenir.
  
  - `example` : Bu API'yi kullanan istemci ve kullanıcılar için nasıl bir gövde parametresi göndermesi gerektiğine dâir bir örnek belirtebilirsiniz.è
  
  - `examples` : Birden fazla gövde parametresi örneği gösterk için kullanılır.
  
  - `openapi_examples` : OpenAPI için müşahhas örnek belirtmek için kullanılır.
  
  - `is_required` : Gövde parametresinin zorunlu olup, olmadığını belirtmek için kullanılır.
  
  - `title` : Gövde parametresi için bir başlık belirtmek istenirse, kullanılabilir.
  
  - `media_type` : içerik
  
  - `gt`, `ge`, `lt`, `le` : Sayısal değerli gövde parametreleri için sırasıyla, 'büyüktür', 'büyük eşittir', 'küçüktür' ve 'küçük eşittir' sınırlamalarını belirtmek için kullanılan parametreler.
  
  - `description` : Gövde parametresini ifâde eden bir açıklama eklenebilir.

- Gövde parametresini anahtar - değer çifti olarak da işâretleyebilirsiniz, dict olarak...
  param : `dict[int, bool]`

> ***NOT :*** JSON sadece metîn tipinde anahtar belirtir; fastAPI ise sunucuya metîn olarak gelen anahtarı hedef tipe dönüştürür ve doğrular.

- ..

#### Kontrolü Genelleştirmek

- Eğer birden fazla fonksiyon parametresinde, benzer sorgu parametrelerinizin olması söz konusu ise, bunu modelleyip, ihtiyacınız olan yerde kullanabilirsiniz. Bunun için `pydantic`'in `BaseModel` sınıfını kullanabilirsiniz. Bunu kullanırken `pydantic` diğer sınıflarına da ihtiyaç duyabilirsiniz. `pydantic`, Java'daki 'Reflection' kitâplığına benzer bir kitâplıktır. Burada sınıfınızı bir model olarak tanımlıyor, alanlarını belirtiyorsunuz:
  
  ```py
  from pydantic import BaseModel, Field, Literal
  class City(BaseModel):
      # Alan tanımlarının aralarındaki farklılığa dikkat edin:
      plateCode : int = Field(06, gt=0, lt=82)
      order_by : Literal['asc', 'desc'] = 'asc'
      counties : list[str] = []
  ```

- Modelinize bir yapılandırma ayarı koymak istiyorsanız model_config isimli bir sözlük tanımlayın. Misal, aşağıdaki kod ziyâde özelliklerin bu model için gönderilemeyeceğini ifâde etmek için yazılır:
  `model_config = {'extra' : 'forbid'}`

- Bir kullanım örneği:
  
  ```py
  class FilterOfCity(BaseModel):
      model_config = {'extra' : 'forbid'}
      order_by : = Literal['asc', 'desc'] = 'asc'
  
  @app.get('/cities/')
  def getCityByName(filters: Annotated[FilterOfCity, Query()]):
  ```

- Kullanıcı şehir verilerini çekerken sadece 'order_by' sorgu parametresi gönderebilir; o parametre için de sadece 'asc' ve 'desc' değerlerini belirtebilir.

- `put` için kullanım örneği:
  
  ```py
  class City(BaseModel):
      plateCode : int
      name: str
      info: str
  
  @app.put('/cities/{plateCode}')
  def updateCity(plateCode: int, city: City):
      ...
  ```

- Eğer birden fazla gövde parametresi gönderilirse, `fastapi` bunların anahtar - değer olarak gönderilmesini bekler. Bu, varsayılan olarak böyledir.

- İkinci bir gövde parametresi gönderildiğinde ve bu, BaseModel sınıfının bir alt sınıfı olarak tanımlanmadığında, fastAPI bunun sorgu parametresi olduğunu varsayar. Bunun bir gövde parametresi olduğunu bildirmek için Body sınıfını kullanın:
  
  ```py
  @app.put('/cities/{plateCode}')
  def updateCity(plateCode: int, city: City,
      bodyParameter: Annotated[int, Body(gt=0)]):
      pass
  ```

- Gövde parametresini bir anahtarla gömülü olarak istiyorsanız `Body(embed=True)` kodunu kullanın. 

- Dilerseniz `Body` için oluşturduğunuz `BaseModel` sınıfının özelliği olan `model_config` nesnesi altında `json_schema_extra` nesnesi altında `examples` belirtin, dilerseniz de `Body` sınıfının `example` özelliğini kullanın:
  
  ```py
  class City(BaseModel):
      plateCode: int
      name: str
      info: str
  @api.put('/cities/{plateCode}')
  def addCity(plateCode: int, city: Annotated[City, Body(
          include_in_schema=False,
          is_required = False,
          media_type="html",
          example = {
              "plateCode" : "6",
              "name" : "Ankara",
              "info" : "Ankara hakkında bilgiler"
              }
          )] = None):
      json = {}
      json["info"]: "Şehir bilgisi tazelendi."
      json["city"] = city
  ```

- Gelen sorgu, adres ve gövde parametrelerini `uuid.UUID`, `datetime.datetime`, `datetime.date` gibi tiplerde almak isteyebiliriz. Bu durumda fastAPI otomatik doğrulama yapmaktadır. UUID için 32 karakter uzunluğunda olması, `datetime` için verinin ISO formatında gönderilmesi gerekmektedir.
  Veri tipi ve gönderilmesi gereken veri formatlarını anlamak için örnekler:
  `UUID` -> '1ada2c6c-4a37-4277-8544-69334a5020b7'
  `datetime` -> 2025-05-12T12:34:43
  `time` -> 12:34:43.343
  `date` -> 2025-05-12

> ***NOT :*** FastAPI'da verileri bir model olarak alıp, daha sonra daha geniş bir model olarak kaydetmek istiyor olabilirsiniz; yanî verilerin veritabanındaki modeli ile, kullanıcıdan alınan modelinin farklı olması isteyebilirsiniz (misal, bir kayıt oluşturulduğunda kayıt târihini kendi sistem saatinizle tutmak, bir id atamak gibi işlemler yapılıp, model genişletilebilir). Bu durumda birden fazla model oluşturup, modeller arasında kolayca geçiş yapmak için modelleriniz `pydantic` modeli olarak tanımlayın ve geçişlerde ``**user.dict()` gibi bir ifâde kullanın.

- ..

#### Başlıkları Ele Almak

- Bir HTTP sorgusunun (Request) başlığını ele almak için, başlık bilgisini temsil eden parametre fonksiyon girdisine başlık olduğu belli edilerek verilmelidir:
  
  ```py
  from fastapi import Header
  @api.get('/cities/{nameOrPlateCode}')
  def getCityByNameOrPlateCode(nameOrPlateCode: Annotated[str, Path(
          max_length=16
          ), AfterValidator(validatePlateCode)],
          header_info: Annotated[str | None, Header()] = None):
      pass
  ```

- Yukarıdaki adres çağrılırken bir başlık bilgisinin verilmesi zorunlu değildir; çünkü varsayılan değer olarak `None` vererek, bunun zorunlu olmadığını belirttik.

- Başlık isimleri, özel bir dönüştürmeye tâbi tutulur. Python kodunda, başlık isminde belirttiğiniz alt çizgi işâretleri, istemcinin göndermesi gereken başlık ismine tire ('-') işâreti olarak yansıtılır. Misal, yukarıdaki fonksiyona istemciden gönderilen bir sorguya bir başlık göndereceğimiz zamân `header-info` yazmalıyız. Bu, `Header` nesnesinin kurucu metoduna parametre vererek değiştirilebilir.

- `Header` nesnesi için bâzı parametreler:
  
  - `convert_underscores=True` : `True` verilirse -ki varsayılanı budur- alt çizgi karakterlerini, '-' ile değiştirir.
  
  - `title` : Header'ı ifâde eden başlık değeri
  
  - `example` : Dökümantasyon için başlık örneği
  
  - `examples` : Dökümantasyon için başlık örnekleri
  
  - `description` : Dökümantasyon için açıklama belirtilmek istenirse kullanılır.

- ..

#### Çerezler

- Çerez, `fastapi` kütüphânesi altındaki `Cookie` sınıfıyla ifâde edilir; kullanımı diğerlerine benzerdir.

- Fazla çerezi engellemek için çerez `BaseModel` sınıfıyla ifâde edilmeli ve bu sınıf içerisinde `model_config` özelliğine `{"extra":"forbid"}` değeri verilmeli.

- ..

- Birden fazla durumda, benzer özelliklere sâhip çerezler kullanabilmek için bir çerez modeli oluşturabilir ve kullanabilirsiniz, tıpkı diğerlerinde olduğu gibi...:
  
  ```py
  from fastapi import Cookie
  class CookieModel(BaseModel):
      sessionId: str
      trackerId: str | None = None
  
  @api.get('/cities/')
  def getCities(cookies: Annotated[CookieModel, Cookie()])
  ```

- ..

#### Geri Dönüşleri (Response) Ele Alma

- Geriye `pydantic` nesnesi döndürebilirsiniz; `fastapi` bunu bir JSON nesnesine çevirir ve döndürür. Bunun için sınıfınızı `pydantic` sınıfı olarak ayarlamalısınız:
  
  ```py
  class City(BaseModel, extra = 'allow'):
      def __init__(self, **kwargs):
          super().__init__()
          for key in kwargs:
              self.__setattr__(key, kwargs[key])
  
  @api.get('/cities/')
  def getCities():
      cities = [
          City(plateCode = 6, name = "Ankara",info = "Şu anki başkent"),
          City(plateCode = 34, name = "İstanbul",
              info = "Târihî Başkentlerimizden birisi"),
          City(plateCode = 13, name = "Bursa",
              info = "Târihî Başkentlerimizden birisi")
          ]
      return cities
  ```

- Yukarıdaki kodu API'ya ilâve edip, `localhost:8000/cities` adresini ziyâret ettiğimizde geriye şu sonuç dönmeli:
  
  ```json
  [
      {
          "plateCode": 6,
          "name": "Ankara",
          "info": "Şu anki başkent"
      },
      {
          "plateCode": 34,
          "name": "İstanbul",
          "info": "Târihî başkentlerimizden birisi"
      },
      {
          "plateCode": 13,
          "name": "Bursa",
          "info": "Târihî Başkentlerimizden birisi"
      }
  ]
  ```

- Ayrıca geri dönüş tipini elle belirtip, o tipte bir nesne oluşturmak için gerekli veriyi vererek veri döndürebilirsiniz. Yukarıdaki örnek, şu şekilde yazılabilir:
  
  ```py
  @api.get('/cities/', response_model=list[City])
  def getCities():
      return [
      {"plateCode" : 6, "name" : "Ankara", "info" : "Şu anki başkent"},
      {"plateCode" : 34, "name" : "İstanbul",
            "info" : "Târihî başkentlerimizden birisi"},
      {"plateCode" : 13, "name" : "Bursa",
            "info" : "Târihî başkentlerimizden birisi"}
      ]
  ```

- Buradaki `response_model` parametresi bir sarmalayıcı ('decorator') sınıftır.

- Geri dönüşleri daha yalın bir şekilde ele alabilirsiniz. Bunun için `Response` ve alt sınıflarını kullanabilirsiniz.

- Geriye döndürülen nesnenin atanmayan özelliklerinin cevâp (Response) nesnesine eklenmemesi için gelen isteği ele alırken, `response_model_exclude_unset` parametresini kullanabiliriz:
  
  ```py
  from pydantic import BaseModel
  class City(BaseModel):
      plateCode: int
      name: str
      info: str | None = None
    @api.get('/cities/', response_model=list[City],
                      response_model_exclude_unset=True)
  def getCities():
      return [{"name": "Ankara", "plateCode":6},
      {"name":"İstanbul","plateCode":34, "info":"Medeniyet başkenti"}]
  ```

- Benzer şekilde, varsayılan değerlerin dışlanması için `response_model_exclude_defaults` parametresine `True` verebilirsiniz; `None` değerli özelliklerin gönderilen cevâbın gövdesine eklenmemesi için `response_model_exclude_none` parametresine `True` verebilirsiniz.

- ..

##### Response ve alt sınıfları

- Cevâp (Response) ile ilgili sınıflar `fastapi.responses` kitâplığı altında bulunuyor.
1. `Response` : Cevâbı simgeleyen temel sınıftır.

2. `RedirectResponse` : Gelen bağlantıyı başka bir adrese yönlendirmek için kullanılan cevâp sınıfıdır. Gelen isteği yönlendirmek istediğiniz adresi `RedirectResponse` nesnesini oluştururken `url` parametresiyle veriniz. Eğer sunucunuz içerisinde, aynı bağlantı portunun bir dalına yönlendirme yapıyorsanız, host ve port numarasını vermenize gerek yok, ondan sonraki kısmını vermeniz kâfî:
   
   ```py
   #Gelen isteği anasayfaya yönlendirmek için şu Response döndürülebilir:
   return RedirectResponse(url='/')
   ```

3. `FileResponse` : Kurucu metoduna şu parametreler verilir:
   
   - `path` : Dosyanın yoludur.
   
   - `status_code: int = 200` : Gönderilen cevâbın durum kodudur.
   
   - `headers = None` : Başlık bilgisi verilir.
   
   - `media_type = None` : İstenilirse, medya tipi belirtilebilir.
   
   - `background : BackgroundTask | None = None` : 
   
   - `filename = None` : Dosyanın istemci tarafından indirildiğindeki ismidir. Eğer bir isim verilmezse dosya, rastgele isimlendirilir. Ayrıca isim vermek, bâzen tarayıcının dosyayı açmak yerine kaydetme seçeneği göstermesine vesîle olur.
     
     Başka parametreleri de vardır.

4. `HTMLResponse` : HTML sayfası döndürürken bu cevâp tipi kullanılabilir. Yapıcı metodu pek çok parametre alır; bâzıları şunlardır:
   
   - `content` : HTML içeriğidir.
   
   - `status_code = 200` : Döndürülen cevâbın durum kodudur.
   
   - `headers` : Başlık bilgisidir.
   
   - `media_type`, `background` parametrelerini de alabilir.

5. `JSONResponse` : JSON biçiminde cevâp döndürmek istediğinizde kullanabilirsiniz. Döndürmek istediğiniz JSON verisini `content` parametresi olarak veriniz. `content` parametresi bir sözlük veyâ bir dizi olabilir.  `status_code`, `headers`, `media_type` ve `background` parametrelerini de alabilir.

6. `StreamingResponse` : Büyük boyutlu veri seti iletmek veyâ gerçek zamânlı veri iletmek amacıyla kullanılabilir.
- Döndürülen cevâbın durum kodunu cevâp nesnesini oluştururken belirtebildiğimiz gibi, isteğin ele alındığı fonksiyon parametresinde de belirtebiliriz. Bu, cevâp nesnesini kendimizin oluşturmadığı ve bir sözlük veyâ metîn veyâ model döndürdüğümüz zamânlarda kullanılabilir:
  
  ```py
  @api.post('/cities/{plateCode}', status_code=201)
  def addCity(plateCode: int, city: City):
      json = {}
      json["info"]: "Şehir eklendi."
      json["city"] = city
  ```

- Eğer hangi durum kodunun ne anlama geldiğini bilmiyorsanız `fastapi.status` kitâplığını kullanabilirsiniz. Bunun içinde enum tarzında değerler bulunmaktadır. Bu değerlerin isimlendirilme tarzı şu şekildedir : HTTP_kodNumarası_kodAnlamı
  Misal, `fastapi.status.HTTP_201_CREATED` değeri 201 kodunu ifâde etmektedir; zâten bu değer tamsayıdır ve 201'dir; fakat isim ile anlaşılır biçimde sunulmaktadır.

- Durum kodlarının aralığı hakkında bâzı bilgiler şöyledir (sınırdakiler aralıklara dâhil):
  
  - **100-199** : Bu aralıktaki kodlar "Information" (bilgi) durumunu ifâde eder. Bu koda sâhip cevâp nesnelerinin bir gövdesi yoktur.
  
  - **200 - 299** : "Successful" (başarılı) kodlarıdır.
  
  - **300 - 399** : "Redirection" (yönlendirme) durumu kodlarıdır. Bu kodlardan biriyle döndürülen cevâbın bir gövdesi olabilir veyâ olmayabilir; fakat 304 ('Not Modified') kodunun bir gövdesi olamaz.
  
  - **400 - 499** : "Client error" (istemci hatâsı) durumlarının kodları bu aralıktadır.
  
  - **500 - 599** : "Server error" (sunucu hatâsı) durumlarının kodları bu aralıktadır. Bu aralıktaki kodları neredeyse her zamân doğrudan kullanmazsınız; çünkü sunucuda bir şeyler ters gittiğinde sunucu bu kodlardan birisini otomatik olarak döndürür.

- Sık kullanılan veyâ bilinmesi gereken bâzı kodlar ise şöyledir:
  
  - **200** : 'Başarılı' durumunu ifâde eden genel koddur; varsayılan koddur.
  
  - **201** : İstemci tarafından yapılan işlem sonucu veritabanında yeni bir kayıt oluşturulduğunda bu 'Created' (oluşturuldu) anlamındaki kod kullanılır.
  
  - **204** : Bu kod 'No content' (içerik yok) anlamına gelir ve istemciye hiçbir şeyin döndürülmeyeceğini ifâde eden bir koddur. Dolayısıyla bu koda sâhip bir cevâp nesnesinin gövdesi olmaz.
  
  - **202** : Bu, isteğin başarıyla alındığı, fakat işlemin başarısızlıkla sonuçlanabilme ihtimâlinin olduğu durumlarda kullanılan koddur.
  
  - **404** : En çok karşılaşılan kodlardan birisi olan bu kod, istemci tarafından gönderilen isteğin adreslenemediğini, istenen verinin bulunamadığını ifâde etmektedir. Bu, hatâlı url bilgisi girildiğinde de olabilir, hatâlı sorgu parametresi veyâ gövde parametresi gönderildiğinde de...
  
  - **401** : "Unauthorized" (yetkilendirilmemiş) anlamındaki bu kod, gelen istek ile istenen verinin döndürülmesi veyâ yapılmak istenen işlemin yapılması için gereken yetkinin istemcide bulunmadığını ifâde etmektedir.

- ..

#### Yalın Kullanım

- fastapi gelen istek ('request') için doğrulamalar yapar, ilgili elemanları (adres parametresi, sorgu parametresi, sorgu gövdesi) ayırır ve bunları belirtilen değerlere eşitler; fakat bunun yerine gelen istek nesnesine doğrudan erişmek istediğiniz durumlar olabilir. Bunun için `fastapi.Request` sınıfını kullanabilirsiniz.
- Kurucu yöntemi şöyledir: `Request(scope, receive, send)`
- `Request` nesnesi üzerinden pek çok özelliğe erişebilirsiniz.

> ***NOT :*** Eğer gelen isteğin `Request` yerine web socket (`fastapi.WebSocket` sınıfıyla temsil edilir) olarak ele alınması gereken durumlar da varsa, isteği daha da yalın olarak almak için `fastapi.requests.HTTPConnection` sınıfını kullanabilirsiniz.

- .

## FORM Modelleri

- ..
