# SPRING BOOT ve WEB GELİŞTİRME

## BU DEFTER HAKKINDA

- Bu defteri okumadan evvel JSON ve serîleştirme gibi kavramları bildiğinizden emîn olunuz.

- Spring boot'u daha iyi anlamak için önce Spring defterini okumanızı tavsiye ederim.

- Java ile web geliştirmek istiyorsanız, bu defter iyi bir başlangıç noktası sayılabilir.

- Yazar : Mehmet Akif SOLAK

## GENEL BİLGİLER

- Spring Java'da çeşitli mimariler için altyapı sağlayan, açık kaynaklı bir geliştirme ortamıdır.

- Spring boot ise uygulamalar için varsayılan yapılandırmaları ve bu yapılandırmaları kolayca değiştirme imkânı sunarak uygulamaların hızlıca geliştirilmesini sağlayan, web odaklı bir Spring paketidir.

- Spring boot kod üretimi, otomatik yapılandırma gibi özellikleri destekler ve gömülü bir web sunucusu ile gelir.

- Spring boot Java web geliştirme uygulamalarında uzun süre açık ara en çok tercih edilen geliştirme çerçevesi (framework) olmuştur. Şimdilerde Quarkus de tercih edilir olsa da, Spring boot hâlen yoğun şekilde kullanılmaktadır.

- Spring boot, güvenilir, hızlı ve geniş topluluk desteği bulunan bir web geliştirme ortamıdır.

- Spring 3.0 versiyonu için Java 17 gereklidir.

- Spring boot içerisinde gömülü bir web sunucusuyla berâber gelir ve 'servlet' işlemlerini kullanıcıdan soyutlar; böylece kullanıcıya MVC mimarisinde web uygulamalarını kolayca yazması sağlanır.

- Bir web uygulaması için gerekli olan web sunucusu yazılımı Spring içerisinde Tomcat olarak gelmektedir; fakat bu, başka bir web sunucusu belirtilerek değiştirilebilir.

- Spring boot, Spring ile berâber kullanılır ve Spring'te kullanılan tanımlamaların üzerine inşâ edilir; yeni bildirimler mevcuttur.

- Spring boot projesi oluşturmanın hızlı yolu [https://start.spring.io/](https://start.spring.io/) web adresi üzerinden kullanılmak istenen JVM dili (Java, Groovy, Kotlin); dil sürümü, proje derleme ve yapılandırma aracı (Maven veyâ Gradle) ve bağımlılıkların seçilmesi yoluyla proje temel iskelet dosyasını indirmektir.

- Bir Spring boot projesinde projeyle ilgili ayarlarımızın belirtildiği ana dosya '**application.properties**'dir.

## BAŞLANGIÇ

#### Spring Boot Bağımlılığını Projeye Ekleme

- Bunun için **pom.xml** dosyasına şu bağımlılıklar eklenir:
  
  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId> <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
  </dependency>
  ```

- ..

#### Bir Spring Boot Web Projesini Çalıştırma

- Bir web projesinin Spring boot projesi olduğunu bildirmek için projenin çalıştığı, ana 'main' fonksiyonunun olduğu sınıfın üstüne `@SpringBootApplication` bildirimi eklenmelidir. Ardından uygulama şu şekilde başlatılmalıdır:
  
  ```java
  @SpringBootApplication
  public class SpringBootWebApp{// Bu sınıf ismini değiştirebilirsiniz
      public static void main(String[] args){
          SpringApplication.run(SpringBootWebApp.class, args);
      }
  }
  ```

- ..

#### Spring Boot Web Uygulamasının Yayın Portunu Değiştirme

- Bu, iki şekilde yapılabilir:
  
  1. **application.properties** dosyasına `server.port=8786` yazarak yayın portunu 8786 yapabilirsiniz; elbette buraya farklı bir port numarası da girebilirsiniz.
  
  2. Java kodu üzerinden bunu yapabilirsiniz. Bunun için şöyle bir kod eklemelisiniz; buradaki sınıf ismini değiştirebilirsiniz, önemli olan ilgili arayüzü uygulayıp, ilgili fonksiyonda port değişikliğini belirtmenizdir:
     
     ```java
     public class AppPortConfigure implements
                  EmbeddedServletContainerCustomizer{
        @Override
        public void customize(ConfigurableEmbeddedServletContainer 
                                                        container){
            container.setPort(8786);
        }
     }
     ```

- ..

#### Uygulamanın Yayına Alınması

- Uygulamayı yayına almak için “complete” dizini içerisinde uçbirim (terminal) açılır ve
  
  Gradle için `./gradlew bootRun`
  
  Maven için `./mvnw spring-boot:run` komutu çalıştırılır.

- ..

## WEB UYGULAMALARINDA MİMARİLER

#### MVC Mimarisi

- MVC (Model - View - Controller) mimarisi web tabanlı uygulamalarda en çok tercih edilen mimarilerden birisidir. Bu mimaride,
  
  - **Controller** : Gelen isteği karşılayan yapıdır. Gelen isteğin metot türüne (GET, POST, PUT vs.), isteğin yapıldığı bağlantı adresine ve istekle gelen bilgilere göre sunucuda hangi fonksiyonun bu isteği ele alacağını belirten bir yapıdır.
  
  - **View** : Kullanıcıya gösterilen arayüzdür. Bu, yalın bir web uygulamasında HTML - CSS yapıları, React ile geliştirilmiş bir web uygulamasında bir Component, Flutter ile geliştirilmiş bir uygulamada bir Widget olabilir.
  
  - **Model** : **Controller** ile **View** arasındaki veri alışverişinin biçimini belirten şablondur; verinin biçimidir. Misal, Java'da kullanıcı bilgilerini tutmak için oluşturulan bir 'User' sınıfı bir modeldir. Kontrolcü, eğer bir veri gönderecekse bu model nesnesini döndürür. 

- MVC mimarisinde sunucuya gönderilen isteğin gövdesi (eğer varsa), model biçiminde olmalıdır. Benzer şekilde sunucudan kullanıcıya döndürülen veri de model biçiminde olmalıdır.

#### REST Mimarisi

- MVC, web uygulamalarının temelidir; fakat REST mimarisi, bilhassa API tasarımında en çok kullanılan mimaridir.

- Rest API, kaynak odaklı, basitleştirilmiş, veri iletim formatı olarak JSON'un kullanıldığı bir web servisi çeşididir.

- REST API, protokol olarak HTTP'i kullanır.

- REST API'nin en temel özelliği bağlantı adres noktalarının (endpoints) ve bağlantı tipinin (GET, POST, PUT, PATCH, DELETE) uygulanacak işlemi ifâde etmek için yeterli olmasıdır. Misal, `/products/{id}` bağlantı adresine bir **GET** isteği attığınızda ilgili `id` değerindeki ürüne erişmek istediğinizi belirtmiş olursunuz. Aynı adrese bir **POST** isteği attığınızda, ilgili `id` değerine sâhip bir ürün oluşturmuş olursunuz (tabi durumda ürün bilgilerini isteğin gövdesine (request body) yazmalısınız).

- REST mimarisi **stateless** (durumdan bağımsız, durumsuz) bir mimaridir. Bu özellik, gelen her isteğin ayrı ayrı ele alındığını ve bir isteğin ele alınmasının diğer isteğin ele alınmasını etkilemediğini ifâde eder.

- REST'in durumdan bağımsız yapısı sebebiyle ölçeklenebilirliği yüksektir, test edilmesi kolaydır; hatâ ayıklaması ve entegrasyonu kolaydır.

- REST mimarisinde HTTP metotlarının anlamları:
  
  - **GET** : Eğer sunucudan veri çekilmek isteniyorsa bu HTTP metodu kullanılır. Bu metotta, isteğin gövdesine herhangi bir veri yazılmaz; bağlantı adresi ve bağlantı adresiyle gönderilen parametreler istemci bilgisayarın sunucudan ne istediğini belirtir.
  
  - **POST** : Eğer sunucuya bir veri eklenmesi isteniyorsa bu metot kullanılır. Eklenmek istenen veri gönderilen isteğin parametresine yazılır; bu veri, eklenmek istenen verinin serîleştirilmiş hâlidir.
  
  - **PUT** : Eğer sunucudaki bir verinin değiştirilmesi / tazelenmesi isteniyorsa bu metot kullanılır. Bu metot kullanıldığında değiştirilmek istenen verinin tümü sunucuya gönderilir ve sunucu ilgili nesneyi veritabanına kaydeder.
  
  - **PATCH** : Eğer verimiz çok büyükse ve biz verinin sadece bir parçasını değiştirmek istiyorsak, bu durumda verinini tümünü sunucuya göndermek gereksiz işlem yükü ve trafik oluşturur; bant genişliğini daraltır. Böyle bir durumda, verinin sadece değiştirilmesini istediğimiz parçasını sunucuya gönderirken **PATCH** metodunu kullanırız.
  
  - **DELETE** : Sunucuda bir silme işlemini tetiklemek istediğimiz durumlarda bu metot tipini tercih etmeliyiz.

- REST mîmârîsinde MVC'den farklı olarak kullanıcıya model (HTML) yerine kaynak (JSON olarak) döndürülür. Geriye dönen cevâp JSON yerine XML de olabilir; bu durum API dökümantasyonunda bildirilir; fakat daha az mâliyetli (bayt olarak) olması, veri tiplerinin daha kolay ifâde edilmesi, nesne yönelimli yaklaşıma daha uygun olması gibi sebeplerden ötürü JSON tercih edilir.

## BİLDİRİMLER ve KULLANIM

- Web uygulamasının en temel yapılarından birisi gelen isteğin karşılanmasıdır. Gelen istekleri karşılayan yapıya **Controller** denmektedir.

- Spring'te bir sınıfın **Controller** olduğunu belirtmek için `@Controller` bildirimi, ilgili sınıfın imzasının üstüne eklenir.

- Bir sınıfın **REST Controller** olduğunu belirtmek için ise `@RestController` bildirimi kullanılmalıdır.

- `@RestController`'ın `@Controller`'dan farkı **Controller**'dan geriye döndürülen verinin otomatik olarak JSON'a serîleştirildiğini ve `HttpResponse` nesnesine eklendiğini belirtmesidir. Bu durumda `@RestController`, `@Controller` + her metot için `@ResponseBody` bildirimlerinin birleşimidir

- Eğer konuya yeni başladıysanız, anlayamamış olabilirsiniz; açıklamak istersek;

- İstemciden gelen istekler, kontrolcünün bir metoduna denk düşer (hangi metoda denk düşeceğini biz belirtiyoruz); bu fonksiyon da arkaplandaki ilgili işlemleri tetikler ve en son kullanıcıya bir cevâp döndürür. REST mimarisinde döndürülen cevâbın bir gövdesi vardır ve bu JSON formatındadır. Bu JSON formatı içerisinde ilgili nesnenin serîleştirilmiş hâli vardır; fakat bu serîleştirme işlemini Spring kendisi yapar; biz sadece döndürmek istediğimiz nesneyi belirtiriz.

- `@RestController` sınıfında ele alınacak istekler, bağlantı adresindeki hangi ek ile eşleşiyorsa, diğer bir deyişle bağlantı adresinde hangi ek görüldüğünde, gelen isteğin bu sınıf tarafından ele alınacağını bildirmek için sınıfın başına `@RequestMapping("uygulamaAdi")` bildirimi eklenir. Buradaki 'uygulamaAdi' aslında bağlantı adresindeki eke karşılık gelmektedir. Misal, bir e - ticâret sitesinin ana adresinin 'eticaret' olduğunu düşünelim. Bu site içerisinde kategori bilgilerinin alındığı alt uygulamanın 'eticaret/kategori' olduğunu düşünelim. Bu durumda kategori için gelen istekleri ele alan sınıfın başına `@RequestMapping("/kategori")` bildirimini eklemeliyiz:
  
  ```java
  @RestController
  @RequestMapping("/api")// Bu sınıf websitesi_adresi/api adresine gelen
                         // istekleri ele alır
  public class WeatherController{
      //.;.
  }
  ```

- Spring boot içerisinde fonksiyonun hangi adresle ve hangi yöntemle gelen isteği karşıladığını bildirmek için bildirimleri kullanırız. Eğer gelen istek GET yöntemiyle geldiyse, fonksiyonun (metodun) üzerine `@GetMapping("url")` bildirimini eklemeliyiz; **Eğer adres çubuğunda bize bir parametre değişkeni geldiyse**, bu değişkenin adres içerisindeki yerine süslü parantez içerisinde bir isim verilir ve `@PathVariable("parametreIsmi")` biçimindeki bildirimle bu parametrenin fonksiyona verileceği belirtilir:
  
  ```java
  @RestController
  @RequestMapping("/api")
  public class WeatherController{
      WeatherService serv;// İllerin hava bilgisini döndüren servis
      @GetMapping("/")// websitesi_adresi/api isteği geldiğinde karşılar
      public String getAllWeathers(){
          return serv.getAllWeathers();
      }
      @GetMapping("/{plateCode}")//Misal : websitesi_adresi/api/34
      public String getCityByPlateCode(@PathVariable int plateCode){
          return serv.getWeatherByPlateCode(plateCode);
      }
  }
  ```

- Eğer ele alınmak istenen isteğin türü POST ise `@PostMapping("url")` bildirimi eklenmelidir. İstek parametresinde gelen değer ise `@RequestBody` bildirimiyle alınabilir. Burada önemli olan bir husus şudur : Spring istek gövdesinde gelen JSON nesnelerini Java nesnelerine otomatik olarak dönüştürebilir; böylece fonksiyon girdi parametresi olarak ilgili nesnenin sınıfını yazabiliriz:
  
  ```java
  @RestController
  @RequestMapping("/api")
  public class WeatherController{
      WeatherService serv;// İllerin hava bilgisini döndüren servis
      @PostMapping("/add")
      public void addWeatherOfCity(@RequestBody City city,
                                  @RequestBody Weather weather){
          serv.addWeatherOfCity(city, weather);
      }
  }
  ```

- Spring, gelen **POST** isteğinin gövdesinde bizim Java'da tanımladığımız `City` ve `Weather` ismindeki sınıfların JSON hâlini bekler; bunları bulur, `City` ve `Weather` nesnelerine çevirir ve bu nesneleri `addWeatherOfCity()` metoduna parametre olarak verir.

- Spring'te gelen isteğin ele alınması için `@RequestMapping` bildirimi kullanılır. Bu bildirimin `path` parametresi hangi adresle gelen bağlantının ele alınacağını gösterir. Bu bildirimin `method` parametresine `GET`, `POST` ve diğer HTTP metotlarından birisi belirtilerek, ilgili adrese, sadece ilgili HTTP metoduyla gelen isteklerin ele alınacağı belirtilebilir. Bunun kısayolları da vardır:
  `@RequestMapping("/", method=RequestMethod.GET)` = `@GetMapping("/")`

- Metot tipleri için kullanılabilen bildirimler (anotasyonlar) şunlardır:
  
  - `@GetMapping` : **GET** isteğini karşılayan metodun üzerine konur.
  
  - `@PostMapping` : **POST** isteğini karşılayan metotlarda kullanılır.
  
  - `@PutMapping` : **PUT** isteğini karşılayan metotlarda kullanılır.
  
  - `@PatchMapping` : **PATCH** isteğini karşılayan metotlarda kullanılır.
  
  - `@DeleteMapping` : **DELETE** isteğini karşılayan metotlarda kullanılır.

- Gelen isteği ele alan bu bildirimlerinin özellikleri şunlardır:
  
  - `name` : Pek kullanılan bir özellik değildir; log kayıtlarının ve hatâ ayıklama notlarının daha okunabilir olması gibi amaçlarla kullanılabilir.
  
  - `value` : Metodun hangi adresle gelen isteği karşılayacağı bilgisidir.
  
  - `path` : `value` parametresinin bir başka ismidir, aynı işlevi yapar.
  
  - `params` : Gelen istekte mutlaka olmasını istediğimiz bir parametre varsa onu burada belirtebiliriz. Bu parametreyi aynı isimde fonksiyondan almak için bu parametreyi fonksiyon girdi parametreleri arasına eklemeliyiz. İstersek bu parametrenin belli bir değere eşit olması veyâ eşit olmaması durumunda ilgili isteğin ele alınacağını belirtebiliriz. Ayrıca bir parametrenin gelen istekte olmamasını ilgili parametre isminin başına `!` işâreti koyarak şart koşabiliriz. Parametreler varsayılan olarak büyük küçük harf duyarlıdır:
    
    ```java
    // Aşağıdaki kod http://localhost:8080/api/fetch?id=2 gibi
    // bir isteği ele alır
    @GetMapping(value="fetch", params="id")
    public ResponseEntity<String> fetchData(int id){return null;}
    
    // Aşağıdaki kod http://localhost:8080/api/fetch?id=2 isteğini ele
    // almaz; "id" belirtilmeyen istekleri ele alır
    @GetMapping(value="fetch", params="!id")
    public ResponseEntity<String> fetchDataWithoutId(){return null;}
    
    // Aşağıdaki kod yalnızca http://localhost:8080/api/fetch?id=2
    // isteğini ele alır
    @GetMapping(value="fetch", params="id=2")
    public ResponseEntity<String> fetchSpesific(int id){return null;}
    ```
  
  - `headers` : Gelen istekleri filtrelemek için isteğin başlık bilgisinde olmasını istediğiniz şeyleri buraya yazabilirsiniz. Misal,
    `headers={"content-type=aplication/json"}` parametresi
    `consumes="application/json"` parametresi ile aynı anlama denk gelmektedir.
  
  - `consumes` : Gelen isteğin içerik tipini (`content-type`) belirtmek için kullanılır. Misal, `application/json` yapılırsa içerik tipi JSON olmayan istek ele alınmaz.
  
  - `produces` : Dönen cevâbın içerik tipini belirtmek için kullanılır. Aynı zamânda bu, cevâp olarak belirttiğimiz cevâbı beklemeyen (kabûl etmeyen) istemcilerin isteklerinin bu metoda gelmeyeceğini belirtir; yanî istekleri filtrelemek için de kullanılabilir. Misal, aynı işi yapan iki istemci servisiniz var; fakat birisi JSON ile, diğeri ise XML ile çalışıyor. Bu durumda şöyle bir kod yazabilirsiniz:
    
    ```java
    @GetMapping(value="transcript/{studentId}",
                produces = "application/json")
    public Transcript getTranscript(@PathVariable int studentId){}
    
    // XML bekleyen istemcinin isteği aşağıdaki metoda yönlendirilir:
    @GetMapping(value = "transcript/{studentId}",
                produces = "application/xml")
    public Transcript getTranscript(@PathVariable int studentId){}
    ```

- Dilerseniz, bir metodun birden fazla adresle eşleşmesini sağlayabilirsiniz:
  
  ```java
  @GetMapping(value={"home", "anasayfa"})
  public ResponseEntity<String> getHomePage(){return null;}
  ```

- Benzer şekilde, diğer özellikler için de birden fazla değer atanabilir. Birden fazla değer atanırken değerlerin `{}` içerisinde yer aldığına dikkat ediniz.

- Dilersek, adres parametrelerini belirtirken düzenli ifâdeler kullanabiliriz. Bunun için şu yazım biçimi kullanılır: `degiskenIsmi:duzenlIfade`. **Bu, adres parametreleri için geçerlidir.**

- Misal:
  `@GetMapping(value="{id:[0-9]+}")` : Sıfır ve pozitif tam sayıları kabûl eder
  `@GetMapping(value="{id:\\d+}")` : Sıfır ve pozitif tam sayıları kabûl eder

- ..

> ***NOT :*** `@RequestMapping` ve türevlerini tanımlarken `params` özelliğine verdiğiniz parametreleri fonksiyon imzasında girdi olarak alırken `@RequestParam` diye belirtmeniz gerekmez.

- ...

> ***NOT :*** Web geliştirme ortamlarının istek karşılayıcı (**Controller**) yapılarının gelen adresleri ele alırken uyguladığı yaklaşımlar farklı olabilmektedir. Buradaki ilk yaklaşım gelen adresin hangi metotla eşleştiğini yukarıdan aşağıya denemek ve eşleşen ilk metotu çalıştırmaktır. Bu yaklaşımın aksine Spring, müşahhas olana öncelik verebilmektedir, sırası en altta olsa bile.. Misal aynı bağlantı adresi için, `params="id=2"` özelliğiyle tanımlanmış bir `@GetMapping` isteği, `params="id"` özelliğiyle tanımlanmış bir `@GetMapping` isteğinden sıra olarak altta olsa bile, `id=2` parametresiyle gelen isteği kapmaktadır.

- ..

#### İstekle Gelen Parametre Değişkenleri, Sorgu Değişkenleri ve Gövde Değeri

- Sunucuya gelen isteklerin içerdiği parçalar birkaç kısma ayrılır:
  
  - **Adres değişkeni** : İstek gönderilen adresin bir kısmının dinamik olarak bir değişkene karşılık düşürülmesi işleminde, bir değişkene karşılık düşürülen kısımdır.
  
  - **Sorgu değişkeni** : Gelen istekte `?` işâretinden sonra anahtar - değer çifti olarak belirtilen ve anahtar - değer çiftinin arasına `&` işâreti konan değerdir.
  
  - **Gövde Değeri** : Gelen isteğin gövdesindeki değerdir. Bu değer, içerisinde birden fazla değişken barındıran bir toplu değer de olabilir.

- Şu misal bu üç yapıyı daha iyi açıklayabilir:
  `https://www.weather.com/api/ankara?type=celcius&day=saturday`
  Buradaki `https://www.weather.com` sunucunun ana adresidir.
  `/api` : `@RequestMapping` ile belirtilen ve sınıf tarafından buraya gelen isteklerin ele alındığı, hangi uygulamanın seçildiğini (dolayısıyla hangi Controller'ın seçildiğini) belirten alt uygulama ismidir.
  Sonrasında gelen `ankara` ifâdesi şehir ismini ifâde etmektedir değişebilmektedir; bu sebeple **parametre değişkenidir.**
  Ardından gelen `?` karakterinden sonraki kısımlar **sorgu değişkenleridir**.
  Buna göre, `type` ve `day` isimli değişkenlerimiz var ve bunların değer verilirken değer ile değişken ismi arasına `=` işâreti konur. Bu değişkenlerin neler olduğunu ve zorunlu olup, olmadığını biz belirliyoruz.
  Gövde değeri ise, sorguyla berâber gönderilen, fakat sorgunun bağlantı adresi içerisinde değil, gönderilen isteğin gövdesinde bulunan değerdir. HTTPS yöntemi kullanıldığında bu gövde değeri de şifrelendiğinden şifreli haberleşilmiş olunur.

- **Adres değişkeni** sorgunun adreslenmesi (ele alınması) için gereklidir; istenen kaynağı ifâde ederler.
  **Sorgu değişkenleri** istenen verinin ne olacağı, nasıl olacağıyla ilgili filtre, biçim gibi özelliklerin belirtildiği değişkenlerdir.
  **Gövde değeri** ise, form verilerinin, hassas verilerin gönderildiği veyâ sunucuya eklenmek istenen bir kaynak değerinin gönderildiği yapıdır.

- **Gövde değeri**nin alınması için `@RequestBody` bildirimi, **adres değişkeni**nin ele alınması için `@PathVariable` değişkeni, sorgu değişkeninin ele alınması için `@RequestParam` değişkeni kullanılır:
  
  - `@RequestBody` : Gelen istekle berâber bir sorgu gövdesinin beklendiğini ifâde eder. Kullanıldığında bu sorgu gövdesinin `required` parametresinin varsayılan değeri `true`'dur; bu, sorgu gövdesinin zorunlu olduğu anlamını ifâde eder. Sorgu gövdesi zorunluysa ve gönderilmemişse hatâ fırlatılır. Kullanımı şöyledir:
    
    ```java
    @PostMapping("/add")
    public void addWeatherOfCity(@RequestBody City city,
                                @RequestBody Weather weather){
        serv.addWeatherOfCity(city, weather);
    }
    ```
  
  - `@PathVariable` : İsteğin bağlantı adresindeki isimlendirilmiş bölümü ifâde eder. Bunu fonksiyona rahatça geçebilmek için bu bildirim kullanılır. `name`, `value` ve `required` parametreleri vardır:
    
    ```java
    @GetMapping("/{plateCode}")//Misal : websitesi_adresi/api/34
    public String getCityByPlateCode(@PathVariable int plateCode){
        return serv.getWeatherByPlateCode(plateCode);
    }
    ```
  
  - `@RequestParam` : Sorgu değişkenleri bu şekilde alınır. Alınmak istenen sorgu değişleni fonksiyona girdi olarak yazılır ve önüne bu bildirim eklenir. Spring, ilgili sorgu değişkenini fonksiyona iletir. Bu bildirimin `name`, `value`, `required`, `defaultValue` parametreleri vardır:
    
    ```java
    @GetMapping("/{plateCode}")//Misal : websitesi_adresi/api/34
    public String getCityByPlateCode(@PathVariable int plateCode,
        @RequestParam(required=false, defaultValue=1) int numOfDays){
        return serv.getWeatherByPlateCode(plateCode);
    }
    ```

- ..

#### Spring boot ve Spring Web ile İlgili Diğer Bâzı Bildirimler

- Spring, modüler bir geliştirme ortamıdır; pek çok Spring bildirimi web projesinde veyâ başka projelerde kullanılabilir. Bu sebeple `org.springframework.web.bind.annotation` altında olmayan bâzı bildirimlere de burada değinmek lazımdır:

- `@Component` : Bir bileşenin Spring nesnesi (bean) olduğunu belirtmek için kullanılır. `@Controller`, `@Service` gibi alt bildirimler birer `@Component`'tir. Bu bildirimin olduğu sınıf Spring tarafından otomatik oluşturulabilir; Spring bunun için parametresiz kurucu fonksiyona ihtiyaç duyabilir. **!** `@Component` bildiriminin `@Bean` bildiriminden farkı, `@Bean` bildirimini bir metot üzerinde kullanarak, ilgili nesneyi o metot içerisinde bizim oluşturmamızdır. `@Component` bildiriminde ise nesne Spring tarafından oluşturulur. 

- `@Service` : `@Component`'in özelleştirilmiş hâlidir. İlgili sınıfın iş kodlarını barındırdığını belirtir, kod okunabilirliğini arttırmak için kullanılır.

- `@Configuration` : Uygulama nesnelerinin (beans) tanımlandığı yere uygulama bağlam bilgisinin tanımlandığı yer diyebiliriz. Bu sınıfın tepesine bu bildirimi ekleyerek, Spring Boot'un bu sınıftaki yapılandırmaları uygulamaya geçirmesini bekliyoruz.

- `@Autowired` : Bir alan (özellik) tanımının üzerine eklenebilen bu bildirim Spring'in ilgili alan için gereken nesneyi üretip, ilgili alana otomatik olarak atamasını sağlamak için kullanılır. Bu, bir arayüzün uygulamanızda sadece bir uygulayıcısı varsa, o arayüz nesnesini oluşturma işinin otomatik olarak yapılması işleminde sıklıkla kullanılır. Eğer bir arayüz tipinde bir alan için bunu verdiyseniz ve bu arayüzün birden fazla uygulayıcısı varsa, Spring hangi uygulayıcının seçilip, yerleştirileceğini anlayamaz ve bu sebeple bu tür durumlarda `Primary()` veyâ `Qualifier()` bildirimleri de kullanılır.

- `@ResponseStatus` : Metodun üzerine eklenebilir. İlgili metotla dönen cevâbın (response) durum kodunu belirtir; okunabilirliği arttırır, kodlama hızını arttırır. İçerisine parametre olarak `org.springframework.HttpStatus` kitâplığı altındaki bir değeri (enum) alır.

- `@ResponseBody` : Metodun üstüne eklenebilir. İlgili metodun döndürdüğü nesnenin (response) nesnesinin gövdesine bağlanacağını ifâde eden bir bildirimdir. Eğer `@RestController` kullanıyorsanız bunu yazmanıza gerek yoktur; çünkü `@RestController` bildirimiyle süslenmiş sınıf içerisindeki tüm `@RequestMapping` bildirimiyle süslenmiş metotlar zâten bu bildirimi taşımaktadırlar. `@GetMapping`, `@PostMapping` gibi bildirimlerin aslında birer `@RequestMapping` bildirimi olduğunu unutmayınız (`@RequestMapping(method=RequestMethod.GET)` = `@GetMapping`).

- `@ModelAttribute`: MVC yapısında, isim vererek ilgili modeli almayı sağlayan bildirimdir.

- `@CrossOrigin` : `@Controller` sınıfının tepesine veyâ herhangi bir `@RequestMapping` metodunun üstüne eklenebilir. Çapraz alan iletişimi sağlar.

- `@Profile` : Bu özellik bir arayüzün birden fazla uygulayıcısı olduğu durumda, bu uygulayıcıları isimlendirmek ve kod üzerinde değişiklik yapmadan, yalnızca 'application.properties' yapılandırma dosyası üzerinden hangisinin seçileceğini belirterek ilgili arayüz için ilgili sınıfın kullanılmasını sağlayan temel bir Spring bildirimidir. Sınıf üzerine `@Profile("profilIsmi") şeklinde bildirim eklenir.`

## BİRİM TESTLERİNİN EKLENMESİ

- Spring Boot, Spring Test ile bâzı testlerin yapılması için araçlar sağlar.

- Bunun için uygulamaya ilgili bağımlılığın eklenmesi gerekmektedir.

- Gradle için, “build.gradle” dosyası içerisine `testImplementation('org.springframework.boot:spring-boot-starter-test')` kodu eklenmelidir.

- Maven için, “pom.xml” dosyası içerisine, `<dependencies></dependencies>` etiketleri arasına şu kod eklenmelidir:
  
  ```xml
  <dependency>
      <groupId>spring.framework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
  </dependency>
  ```

- Tabi bunları kullanmak için de ayrıca test kodları yazmak gerekiyor.

## SPRING DEVTOOLS

- Spring devtools, Spring web uygulaması geliştirirken yeni eklenen özelliğin uygulamanın durdurulup, yeniden baştan başlatılmasına gerek kalmadan yayına alınmasını sağlayan özelliği barındıran bir pakettir.

- Bu paketi eklemek için **pom.xml** dosyasına şu bağımlılığı ekleyin:
  
  ```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
  </dependency>
  ```

- IntelliJ IDEA geliştirme ortamında bağımlılıkları eklediğimizde dahî otomatik yenileme özelliği çalışmıyor. Bunun için 'File->Settings->Advanced Settings' yolundaki 'Allow auto make to start even if developed project is currently running' ayarını aktif hâle getirmemiz gerekiyor. Eğer hâlen çalışmazsa shift tuşuna iki kez bastıktan sonra 'registry' yazıp, gelen 'Registry' seçeneğini tıklayıp, açılan pencerede bulunan 'ide.windowSystem.autoShowProcessPopup' seçeneğini aktif hâle getirelim.

## HATÂLARI ELE ALMAK

- Hatâları ele almak için `try{}catch()` yapısını kullanabilirsiniz elbette; fakat aynı tipte hatânın pek çok yerde oluşması muhtemeldir. Bunun için hatâları bir fonksiyonda da birleştirebilirsiniz. Spring, hatâlar için bir fonksiyon yazıp, o fonksiyonla hangi tip hatânın (istisnânın) ele alınabileceğini daha kolay kodlamanızı sağlar.

- Bunun için `@ExceptionHandler` bildirimi kullanılır.

- `@Controller` sınıfı içerisinde bir metodun başına `@ExceptionHandler` bildirimi ekleyerek o metodun belirttiğiniz tipteki hatâları (istisnâları) ele almasını sağlayabilirsiniz:
  
  ```java
  @RestController
  public class WeatherController{
      @GetMapping("{cityName}")
      public Weather getWeatherByCity(@PathVariable String cityName){
          throw new IllegalArgumentException("hata notu");
      }
      @ExceptionHandler
      public ResponseEntity<String> handleException(
                      IllegalArgumentException exc){
          System.err.println("exc : " + exc.toString());
          return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                  .body(exc.getMessage());
      }
  }
  ```

- Bu şekilde yapıldığında `handleException()` metodu sadece ilgili **Controller**'da fırlatılan hatâyı ele alır.

#### Genelleştirilmiş Hatâ İdâresi

- `@ControllerAdvice` bildirimi hatâları daha merkezî olarak ele almamız sağlar. Bu bildirim bir sınıfın tepesine eklenir ve bu sayede sınıf tüm **Controller** yapılarından fırlatılan mesajları ele alabilir.

- `@ControllerAdvice` bildirimi eklenen sınıfın metotları `@ExceptionHandler`, `@InitBinder` ve `@ModelAttribute` bildirimleriyle süslenmiştir; fakat biz, ilgili metodun hangi istisnâyı ele alacağını belirtmek için sınıfın üstüne bir `@ExceptionHandler` bildirimi ekleriz:
  
  ```java
  import org.springframework.http.ResponseEntity;
  import org.springframework.web.bind.annotation.ControllerAdvice;
  import org.springframework.web.bind.annotation.ExceptionHandler;
  import org.springframework.http.HttpStatus;
  import java.io.IOException;
  @ControllerAdvice
  public class ExceptionManager(){
      @ExceptionHandler(IOException.class)
      public ResponseEntity<String> handleIOException(IOException exc){
          return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
              .body(exc.getMessage());
      }
  }
  ```

- Hatâları ele aldığımız metotlarda kullanıcıya cevâp döndürmemiz gerekmektedir. Bu sebeple geriye `ResponseEntity` nesnesi döndürülür.

- Yukarıdaki koda göre, `handleIOException()` metodu sadece `IOException` istisnâlarını ele almaktadır; eğer birden fazla hatâ çeşidini ele almasını istiyorsak bunları dizi tanımıyla belirtebiliriz:
  
  ```java
  @ExceptionHandler({IOException.class, ClassNotFoundException.class})
  public ResponseEntity<String> handleIOException(IOException exc){
          return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
              .body(exc.getMessage());
      }
  ```

- `@ControllerAdvice` bildiriminin REST'e özel versiyonu `@RestControllerAdvice`bildirimidir. Bunun `@ControllerAdvice` bildiriminden farkı 

- `@ControllerAdvice` ve `@RestController` bildirimleri şu özelliklere sâhiptir:
  
  - `value : String[]` : İlk parametredir. Ele alacağı istisnâların tiplerini ifâde eder. Bu parametrenin takma ismi ise şudur: `basePackages`.
  
  - `basePackages : String[]` : 
  
  - `basePackageClasses : Class<?>[]` : 
  
  - `assignableTypes : Class<?>[]` : 
  
  - `annotations : Class<? extends Annotation>[]` : ..

- Yukarıdaki koddaki gibi dönen HTTP kodunu elle belirtmek yerine bildirimle de belirtebiliriz:
  
  ```java
  @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
  @ExceptionHandler({IOException.class, ClassNotFoundException.class})
  public ResponseEntity<String> handleIOException(IOException exc){
      //.;.
  }
  ```

- ..
