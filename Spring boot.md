# SPRING BOOT

## GENEL BİLGİLER

- Spring boot bir Java uygulamasının hızlıca başlatılması için gerekli yapılandırmaları yazılımcıdan soyutlayan, bilhassa xml kısımlarını yazılımcıdan soyutlayan bir çerçevedir.

- Spring boot Java web uygulamaları için pek çok ayar ve yapılandırmayı sağlama, MVC altyapısı sağlama gibi kolaylıklar sunan bir yazılım geliştirici kitidir (framework).

- Spring 3.0 versiyonu için Java 17 gereklidir.

- Spring boot içerisinde gömülü bir web sunucusuyla berâber gelir ve 'servlet' işlemlerini kullanıcıdan soyutlar; kullanıcıya MVC mimarisinde web uygulamalarını kolayca yazması sağlanır.

- Bir web uygulaması için gerekli olan web sunucusu yazılımı Spring içerisinde Tomcat olarak gelmektedir; fakat başka bir web sunucusu belirtilerek bunu değiştirebiliyorsunuz.

- Spring boot, Spring ile berâber kullanılır ve Spring'te kullanılan tanımlamaların üzerine inşâ edilir; yeni bildirimler mevcuttur.

- Spring boot projesi oluşturmanın hızlı yolu [https://start.spring.io/](https://start.spring.io/) web adresi üzerinden kullanılmak istenen JVM dili (Java, Groovy, Kotlin); dil sürümü, proje derleme ve yapılandırma aracı (Maven veyâ Gradle) ve bağımlılıkların seçilmesi yoluyla proje temel iskelet dosyasını indirmektir.

- Spring boot kullanımında en çok kullanılan temel bağımlılıklar (paketler) şöyledir:
  
  1. spring-boot-starter-web : Bir web projesi başlangıcı için gereken tek bağımlılıktır.

- Bir Spring boot projesinde projeyle ilgili ayarlarımızın belirtildiği ana dosya 'application.properties'dir.

- ..

## TEMEL KULLANIM ve MVC

#### Bir Spring Boot Web Projesini Çalıştırma

- Bir web projesinin Spring boot projesi olduğunu bildirmek için projenin çalıştığı, ana 'main' fonksiyonunun olduğu sınıfın üstüne `@SpringBootApplication`  bildirimi eklenmelidir. Ardından uygulama şu şekilde başlatılmalıdır:
  
  ```java
  @SpringBootApplication
  public class SpringBootWebApp{// Bu sınıf ismini değiştirebilirsiniz.
      public static void main(String[] args){
          SpringApplication.run(SpringBootWebApp.class, args);
      }
  }
  ```

- ..

#### Spring Boot Proje Yayın Portunu Değiştirme

- Bu, iki şekilde yapılabilir:
  
  1. 'application.properties' dosyasına `server.port=8786` yazarak. Siz buradaki '8786' yerine istediğiniz portu yazmalısınız.
  
  2. Java koduyla değiştirilebilir. Bunun için şöyle bir kod eklemelisiniz; buradaki sınıf ismini değiştirebilirsiniz, önemli olan ilgili arayüzü uygulayıp, ilgili fonksiyonda port değişikliğini belirtmenizdir:
     
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
  
  3. ..

#### 'Model' Yapısı Oluşturma

- ..

#### 'Controller' Yapısı Oluşturma

- Bir web MVC projesinde 'Controller', gelen istekleri karşılayan, yönlendiren ve gelen isteklere uygun cevâbı geri döndüren yapıdır.

- Gelen isteklerin esnek biçimde ele alındığı ve cevâbın belli formatta olmasının şart olmadığı durumları sağlayan API çeşidine REST API denir.

- Eğer sadece XML mesajlarının döndüğü ve gelen adres (url)in katı bir formda tutulduğu API mimari yöntemine ise SOAP denmektedir.

- Web uygulamalarında gelen istekler çoğunlukla GET ve POST yöntemlerini kullanır. GET yöntemi isteğin gövdesinde bir veri barındırmadığı ve sunucudan bir veri çekme amacıyla yapılan isteklerde kullanılır. Burada çekilmek istenen veriyi özelleştirmek için sunucuya parametre gönderilir; GET yöntemiyle yapılan isteklerde bu parametre doğrudan bağlantı adresine eklenir. Misal, uygulamadan sadece bir beldenin hava durumu bilgisini çekmek istiyorsak, ilgili ilin plaka kodunu veyâ ismini (API'da hangisini, hangi biçimde belirlediysek) adres çubuğuna parametre olarak gönderebiliriz.

- Spring web mvc projesinde bir sınıfın REST API olduğunu bildirmek için Sınıfın başına `@RestController` bildirimi eklenir. Bu sınıfta ele alınacak istekler, bağlantı adresindeki hangi ek ile eşleşiyorsa, diğer bir deyişle bağlantı adresinde hangi ek görüldüğünde, gelen isteğin bu sınıf tarafından ele alınacağını bildirmek için sınıfın başına `@RequestMapping("uygulamaAdi")` bildirimi eklenir. Buradaki 'uygulamaAdi' aslında bağlantı adresindeki eke karşılık gelmektedir. Misal, bir e - ticâret sitesinin ana adresinin 'eticaret' olduğunu düşünelim. Bu site içerisinde kategori bilgilerinin alındığı alt uygulamanın 'eticaret/kategori' olduğunu düşünelim. Bu durumda kategori için gelen istekleri ele alan sınıfın başına `@RequestMapping("/kategori")` bildirimini eklemeliyiz.

- Spring boot içerisinde fonksiyonun hangi adresle ve hangi yöntemle gelen isteği karşıladığını bildirmek için bildirimleri kullanırız. Eğer gelen istek GET yöntemiyle geldiyse, fonksiyonun (metodun) üzerine `@GetMapping("url")` bildirimini eklemeliyiz; Eğer adres çubuğunda bize bir parametre geldiyse, bunun adres içerisinde bulunduğu yere süslü parantez içerisinde bir isim verilir ve fonksiyon girdi parametresinde bu değerin alınacağını `@PathVariable("parametreIsmi")` bildirimiyle parametrenin önünde belirtmemiz gerekir:
  
  ```java
  @RestController
  @RequestMapping("/api")// websitesi_adresi/api adresine gelen
                              // istekleri ele alır
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
  @RequestMapping("/api")// websitesi_adresi/api adresine gelen
                              // istekleri ele alır
  public class WeatherController{
      WeatherService serv;// İllerin hava bilgisini döndüren servis
      @PostMapping("/add")
      public void addWeatherOfCity(@RequestBody City city,
                                  @RequestBody Weather weather){
          serv.addWeatherOfCity(city, weather);
      }
  }
  ```

- ..

#### İşlemleri Bütüncül İşlem ('Transaction') Yapısıyla Ele Almak

- Bilhassa veri tabanı işlemleri için kullanılan 'transaction' yapısı birbirine bağlı birden fazla işlemin birinde başarısız olunduğunda işlemlerin geriye sarılarak, hiç yapılmamış gibi görünmesi ve sistemin işlemden önceki durumunda olması özelliğini destekleyen ve böylece işlem bütünlüğünü ve inkâr edilemezliği sağlayan bir güvenlik mimarisidir.

- Veritabanı işlemleri yaparken birbirine bağlı işlemleri ve hattâ münferid işlemleri bile bu şekilde yapmak iyi bir yöntem olabilir; zîrâ bu şekilde kayıtlar da yanlış etkilenmemektedir.

- Veritabanında bir 'transaction' açmak için JDBC kullanılarak SQL kodu yazılabilir. Hibernate gibi ORM çözümlerinde bu daha kolayca yapılabilir. Bunun için Hibernate `@Transactional` bildirimini desteklemektedir. Bu bildirimin eklendiği fonksiyonun başında bir 'transaction' açılır ve fonksiyonun sonuna başarıyla ulaşıldığında bu 'transaction' uygulanır ('commit' işlemi) ve kapatılır. Eğer işlem başarısız olursa 'transaction' geriye sarılır ('rollback' işlemi). `org.springframework.annotation.Transactional` kütüphâne adresindeki `@Transactional` bildirimini kullanmalıyız. Bu bildirimi sadece REST API ile veritabanı işlemleri yaptığımızda değil, diğer fonksiyonlarımızda da kullanabiliriz; böylece işlem güvenliği ve bütünselliği arttırılmış olur.

#### Spring Boot Profil Özelliği

- Bu özellik bir arayüzün birden fazla uygulayıcısı olduğu durumda, bu uygulayıcıları isimlendirmek ve kod üzerinde değişiklik yapmadan, yalnızca 'application.properties' yapılandırma dosyası üzerinden hangisinin seçileceğini belirtmek için kullanılır.

- Bunun için ilgili sınıf üzerine `@Profile("profilIsmi")` bildirimi eklenir. Misal, bir web uygulamasında tasarlanan bir resmin birden fazla formatta kullanıcıya verilebildiğini düşünelim. Kullanıcı resmi kaydetmek için tıkladığında seçilen özelleştirmeye göre bu işlemin yapılmasını istediğimizi düşünelim.

#### Uygulamanın Yayına Alınması

- Uygulamayı yayına almak için “complete” dizini içerisinde uçbirim (terminal) açılır ve
  
  Gradle için `./gradlew bootRun`
  
  Maven için `./mvnw spring-boot:run` komutu çalıştırılır.

#### Diğer Bâzı Bildirimler

- `@Configuration` : Uygulama fasulyelerinin tanımlandığı yere uygulama bağlam bilgisinin tanımlandığı yer diyebiliriz. Bu sınıfın tepesine bu bildirimi ekleyerek, SpringBoot'un bu sınıftaki yapılandırmaları uygulamaya geçirmesini bekliyoruz

- ..

## BİRİM TESTLERİN EKLENMESİ

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

- Tabii bunları kullanmak için de ayrıca test kodları yazmak gerekiyor.

#### SPRING DEVTOOLS

- IntelliJ IDEA geliştirme ortamında bağımlılıkları eklediğimizde dahî otomatik yenileme özelliği çalışmıyor. Bunun için 'File->Settings->Advanced Settings' yolundaki 'Allow auto make to start even if developed project is currently running' ayarını aktif hâle getirmemiz gerekiyor. Eğer hâlen çalışmazsa shift tuşuna iki kez bastıktan sonra 'registry' yazıp, gelen 'Registry' seçeneğini tıklayıp, açılan pencerede bulunan 'ide.windowSystem.autoShowProcessPopup' seçeneğini aktif hâle getirelim.

- ..
