# SPRING

- Spring programlama zamânında nesnelerin ilkledirilmesi, projelerin yayına alınması gibi işleri otomatikleştiren, bunlar için pek çok alt modülü bulunan geniş bir kütüphânedir.

# SPRING CORE

## GENEL BİLGİLER

- Spring'in en temel kütüphânesidir.

- En basit anlamda uygulamanın çalışma zamânındaki nesnelerin otomatik olarak ilklendirilmesi, veritabanından çekilen değerlerin nesnelere aktarılması işlemlerini yapar.

- İlk sürümü 2003 senesinde Apache 2.0 lisansıyla sunulmuş.

- Java için Spring kullanımının %50'leri aştığı düşünülmektedir.

- Kodun nesne ilişkilerinde bağımsız olması için Dependency Injection ve IoC (Inversion of Control) isimli iki kavram karşımıza çıkıyor. Dependency Injection IoC yapısını sağlamak / gerçekleştirmek için kullanılan yöntemdir.

- Spring'in çekirdeği ~2 MB; yanî oldukça hafiftir.

- Spring'te nesnelere 'bean' (fasulye) denir.

## SPRING XML

- Spring'in ilk başta kullanımı 'xml' dosyasıyla olmaktaydı.

- Basit bir ifâdeyle, XML dosyası içerisinde uygulama tarafından hangi nesne istendiğinde, Spring'in buna nasıl cevâp vereceği ve bâzı yapılandırmalar belirtilir.

- Spring xml'in ismi genellikle '**applicationContext.xml**' konulmaktadır.

- Bu dosya içerisinde 'bean' tanımları yapılır; kelîme anlamı 'fasulye' olan 'bean' bileşenleri uygulama içerisindeki nesneleri temsil eden yapılardır.

- Bu XML dosyası içerisinde basitçe şunlar yer alır:
  
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context.xsd">
  <bean></bean><!--Fasulye tanımları burada yapılır-->
  </beans>
  ```

- Fasulye tanımlarken her fasulye için 'id' vermeliyiz; bu, Spring'ten nesne istenirken kullanılacak olan münferid bir isimdir. Geriye döndürülecek nesnenin hangi sınıfın örneği olduğunu 'class' özelliğiyle belirtiyoruz; buradaki şuna dikkat edelim: sınıfın paket tam mevkîsini yanî paket ismini de yazmamız gerektiğini unutmamız gerekiyor:
  
  ```xml
  <bean id="db" class="Base.MySQLDAL"></bean>
  <!-- Yukarıdaki kod Spring'ten 'db' isminde bir nesne istendiğinde
  Spring'in Base paketi altındaki 'MySQLDAL' sınıfının bir örneğini
  döndüreceğini ifâde ediyor-->
  ```

- Bu XML yapılandırma dosyasını uygulama içerisine 'ClassPathXmlApplicationContext' sınıfı örneği olarak aktarmalı ve o nesne üzerinden 'getBean()' yöntemiyle nesneleri almalıyız:
  
  ```java
  ClassPathXmlApplicationContext context;
  context = new ClassPathXmlApplicationContext(
      "applicationContext.xml"
  );
  MySQLDAL dal = context.getBean("db", MySQLDAL.class);
  ```

- `getBean()` yönteminin ilk parametresi istenen nesnenin 'id' özelliğidir. İkinci parametresi ise istenen nesnenin hangi sınıftan bir nesne olarak istendiği bilgisidir. Eğer ikinci parametre verilmezse, istenen nesne `Object` nesnesi olarak gelir.

#### Fasulyeler İçin Yapıcı Fonksiyon Girdi Parametresi Belirtme

- Sınıf örnekleri oluşturulurken her zamân doğrudan oluşturulamayabilir; misal, sınıf yapıcı fonksiyonunda girdi parametresi istiyor olabilir. Bu durumda `<bean>` etiketi içerisinde yapıcı fonksiyon parametresi belirtmeliyiz. Yapıcı fonksiyon parametresi şu etiketlerle belirtilir:
  
  ```xml
  <constructor-arg name="host" value="localhost"/>
  <!-- Yapıcı fonksiyondaki 'host' parametresine 'localhost' değeri
  verilerek nesne oluşturulur-->
  ```

- Birden fazla yapıcı fonksiyon parametresi olduğunda bunların sırasının bir önemi yoktur; zîrâ 'name' özelliğiyle o yapıcı fonksiyon parametresinin hangi parametreye denk düştüğünü belirtiliyor.
  
  > ***NOT :*** Nesne oluşturulurken yapıcı fonksiyona parametre geçilmesine 'construction injection' (yapıcı fonksiyon veri aktarımı) denir. Nesnelerin özelliklerine değer aktarılırken tercih edilen yöntem budur; fakat başka bir yöntem de vardır.

- ..

#### Nesne (Fasulye) Özelliklerine Değer Aktarılması

- Nesnelere değer aktarılması için izlenen bir yöntem, bu değerlerin yapıcı fonksiyon ile aktarılmasıdır; fakat nesne oluşturulurken yapıcı fonksiyona parametre olarak verilmeyen özelliklere de değer atanmasını isteyebiliriz; veyâ yapıcı fonksiyon parametresinin kimi zamân nesne oluşturulurken belirtilmeyip, nesne  oluşturulduktan sonra belirtilmesini isteyebiliriz. Bu tür durumlar için kullanılan yönteme 'setter-injection' (Değerlerin 'set' yöntemiyle aktarılması) denmektedir. Bu yöntemi kullanabilmek için nesnenin ilgili özelliklerinin 'setter' yönteminin olması gerekmektedir. Misal, 'Student' sınıfı içerisindeki, 'int classNo' özelliğine bu usûlle değer atanmasını istiyorsak, 'Student' sınıfı içerisinde 'public setClassNo(int no)' isimli bir yöntemimizin olması gerekiyor. Ardından XML dosyasına şu kodları eklemeliyiz:
  
  ```xml
  <bean id="ogrenci" class="UygulamaPaketAdi.Student">
      <property name="classNo" value="17"></property>
  </bean>
  <!-- İlgili özelliğin 'int' tipinde olmasına rağmen tırnak
      içerisinde yazıldığına dikkat ediniz!-->
  ```

- ..

#### XML Dosyası İçerisinde Değer Bazlı Tanımlar

- Spring'ten bir nesne yerine bir liste isteyebiliriz; veyâ bir nesnenin oluşturulması için Spring'in bir listeye ihtiyacı olduğu durumlar olabilir. Bu gibi durumlarda Spring bu liste tipi değeri yine Spring yapılandırma dosyası içerisinde arayıp, getirebilmelidir. Bunun için Spring 'applicationContext.xml' yapılandırma dosyası içerisinde liste, harita gibi değer bazlı veriler tanımlanabilir.

- Spring içerisinde 'list', 'map' ve 'set' veri tiplerinde değer barındırılabilir.

- Liste için `<list></list>` etiketleri kullanılır; bu etiketler içerisinde elemanlar referans `(<ref></ref>`) veyâ değer (`<value></value>`) olarak barındırılabilir; referans elemanlar o elemanın Spring'ten isteneceği anlamına gelir; değer bazlı elemanlar ise xml dosyasında belirtilen değerin kullanılacağı anlamına gelir:
  
  ```xml
  <bean name="envVars">
      <property>
          <list>
              <value>bash</value>
              <ref bean="os.seperator"></ref>
          </list>
      </property>
  </bean>
  ```

- 'set' veri yapısı içerisinde yalnızca münferid değerler barındırabilen, yanî bir değerden sadece bir tâne barındırabilen bir listevârî veri yapısıdır. Spring XML içerisinde 'set' tipinde değişkenler olabilir, bunun için `<set></set>` etiketleri kullanılır:
  
  ```xml
  <set>
      <value>Mehmet</value>
      <value>Ali</value>
      <value>Hasân</value>
  </set>
  ```

- Harita için `<map></map>` etiketleri kullanılır. Her bir değer - anahtar çifti etiket içerisinde şu şekilde tanımlanır:

- ```xml
  <entry key="anahtar" value="deger"/>
  ```

- 'Properties' sınıfından bir değer eklenebilir:
  
  ```xml
  <property>
      <props>
          <prop key="binDir">../bin</prop>
          <prop key="versionNum">3.21</prop>
      </props>
  </property>
  ```

- ..

#### Uygulama Yapılandırma Dosyasına Statik Değerlerin Aktarımı

- Yapıcı fonksiyon parametrelerini değiştirmek için XML dosyasını değiştirmemiz gerekiyor. Bu işlem çok büyük XML yapılandırma dosyalarında zor olabilir. Bunun yerine bu değerlerin bir yerden çekilmesini isteyebiliriz. Bunun için öncelikle, Spring yapılandırma dosyamıza bu değerlerin aktarılması gerektiğini belirtmeliyiz:
  
  ```xml
  <context:property-placeholder location="classpath:values.properties"/>
  <!-- Buradaki 'location' dosyanın konumunu ifâde ediyor,
      'classpath' proje dizinini belirten bir değişken,
      'values.properties' ise dosyamızın ismi -->
  ```

- XML dosyasına aktarmak istediğimiz değerler için 'values.properties' dosyası içerisindeki tanımlarımız şu şekilde olmalı:
  
  ```properties
  mysqlHost=3306
  db.userName=root
  schemaName=basitnotlar
  ```
  
  'values.properties' dosyasındaki metînsel değerlerin tırnak içerisinde yazılmadığına dikkat ediniz.

- Bunu yaptıktan sonra `<bean>` tanımı içerisine şu kodu ekleyerek, ilgili yapıcı fonksiyonun girdi parametresinin atanması sağlanabilir:
  
  ```xml
  <constructor-arg name="host" value="${mysqlHost}"/>
  <!-- XML içerisinde tanımlanmış bir değişkene
  bir metîn içerisinde '${degisken_adi}' biçimindeki kodla erişilir
  -->
  ```

- ..

> ***NOT :*** Hatâdan kaçınmak için kaynak ('resource') dosya yolunu 'classpath' ön işleciyle belirtin

> ***NOT :*** Eğer değer aktarımı yapılan dosyada aynı isimde birden fazla kayıt varsa, bu durumda en son tanımlanan kayıt geçerli olur.

> ***NOT :*** XML dosyasına başka XML dosyasını dâhil etmek için `<import>` etiketi kullanılır; bu etiket kullanıldığında kaynak olarak verilen xml dosyasında 'bean' tanımları, 'property placeholder' tanımları da içe aktarılır:
> 
> ```xml
> <import resource="baskaXml.xml"/>
> ```
> 
> Eğer içe aktarılan dosyadaki tanımlamalar ('bean', 'property-placeholder') ile mevcut dosyadaki tanımlamalar arasında bir çakışma olursa, mevcut dosyadakiler geçerli olur.

- ..

## SPRING ANNOTATION

- Spring'i XML dosyası üzerinden yapılandırmak çok mâliyyetli bir işlemdir. Hem fazla metîn, hem de fazla işgücü gerektiren bu yapı, değişkenlik için uygun değildir.

- Bu sebeple Spring için yeni bir yöntem olan bildirim (notasyon, 'annotation') bazlı yapılandırma eklenmiştir.

- Bu yeni biçimi tanırken, evvelâ 'bean' tanımlarımızı 'applicationContext.xml' dosyasından, sınıf üzerine taşıyalım, inşâAllâh. Hangi nesne (fasulye, 'bean') tanımı hangi sınıftan bir nesne üretiyorsa o sınıfa gidip, sınıfın başına `@Component("beanID")` notasyonunu ekliyoruz:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      //.;.
  }
  ```

- Bunu yaptktan sonra 'applicationContext.xml' dosyası içerisinde bu sınıfların taranması gerektiğini belirtmemiz gerekiyor; bunu belirtmezsek Spring bu sınıflardaki bildirimleri taramayacağından istenen nesneyi üretemeyecektir:
  
  ```xml
  <context:component-scan base-package="Base"></context:component-scan>
  <!-- 'base-package' özelliğine notasyon taraması yapılacak paketi
          yazmalıyız-->
  ```

- Bu biçimle XML dosyası içerisindeki fasulye tanımlamalarından kurtulduk; fakat fasulyeleri tanımlarken hâlen bir işgücü harcaması yapmamız gerekiyor. Bunu daha da kolaylaştırmak ve tek bir merkezden idâre etmek için 'applicationContext.xml' yapılandırma dosyamızı da bir sınıfla yapma özelliğini kullanmalıyız.

- Bir sınıftaki yapıcı fonksiyon değerinin veyâ bir özelliğin bir dosyadan çekilen veri ile ilklendirilmesini istiyorsak  `@Value()` bildirimini kullanmalıyız. Bunun için ilgili özellik üstüne veyâ ilgili parametrenin öncesine bu notasyonu eklemeliyiz:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      @Value("${mysqlHost}")
      int host;
      //.;.
  }
  ```

- Eğer yukarıdaki bildirimi kullanırsak ve değişkenimiz private erişim belirtecine sâhip olsa ve değişken için 'setter' yöntemi olmasa bile yine de hatâ vermiyor.

#### Yapıcı Fonksiyon Girdi Parametresi Belirtme

- Yapıcı fonksiyon girdi parametresi için de `@Value()` bildirimini kullanabiliriz:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      public MySQLDAL(@Value("${mysqlHost}"){/*.;.*/}
  }
  ```

- .. 

> ***NOT :*** Hem 'applicationContext.xml' yapılandırma dosyası, hem de notasyonlar kullanıldığında dosyadan değer aktarımı işlemini XML'de yapmak daha doğru olur; çünkü `@PropertySource()` notasyonunu yazdığımızda bu kaynak dosyadaki değerleri XML içerisinde kullanamıyoruz. XML'in bir  Spring işlenme sırasında bir önceliği var gibi duruyor.

- ..

> ***NOT :*** Hatâdan kaçınmak için sınıf içerisinde `@Autowired` bildirimiyle süslenmiş özellikler için 'setter' yöntemi oluşturun, barındırın.

- ..

## SPRING CLASS-CONFIG (SINIF ile YAPILANDIRMA)

- Spring XML yapılandırma dosyamızın karşılığı olarak bir sınıfı Spring yapılandırma sınıfı olarak atayalım. Bunun için `@Configuration` notasyonu kullanılır:
  
  ```java
  @Configuration
  public class SpringIDARE{
      //.;.
  }
  ```

- Bunu yaptıktan sonra uygulama içerisindeki 'ClassPathXmlApplicationContext' tipinden olan 'context' nesnemizi 'AnnotationConfigApplicationContext' sınıf örneğiyle değiştirmeliyiz; bu da 'ApplicationContext' arayüzünü uygulayan bir sınıftır:
  
  ```java
  AnnotationConfigApplicationContext context
      = new AnnotationConfigApplicationContext(SpringIDARE.class);
  // Girdi parametresi olarak yapılandırma sınıfımızı veriyoruz.
  ```

- 'applicationContext.xml' yapılandırma dosyasında belirttiğimiz sınıf tarama kodunun notasyon karşılığı şu şekildedir:
  
  ```java
  @ComponentScan("Base")
  @Configuration
  public class SpringIDARE{}
  ```

- 'applicationContext.xml' yapılandırma dosyasında belirttiğimiz statik değerlerin bir dosyadan okunması işleminin bildirim karşılığı şu şekildedir:
  
  ```java
  @PropertySource("classpath:values.properties")
  @ComponentScan("Base")
  @Configuration
  public class SpringIDARE{}
  ```

- Spring kullanırken işimiz kolaylaşmış olsa da, hâlâ işimizde gereksiz bir yük var; o da 'bean' tanımı yapmak istediğimiz sınıfların üzerine notasyon eklemek. Ayrıca aynı notasyonu birden fazla sınıfa verdiğimizde hatâ alıyoruz; fakat bu hâliyle, bir sınıfa bir bildirim eklerken bu bildirimi daha evvel kullanmadığımızdan emîn olmalıyız. Bu gibi sebeplerden ötürü fasulye ('bean') tanımlarımızı da Spring yapılandırma sınıfımız içerisinde yapmak isteyebiliriz. Bunun için sınıf içerisinde yöntemler yazıyoruz ve bu yöntemler üzerine bildirim ekleyerek Spring'e bunların birer fasulye olduğunu belirtiyoruz. Bunun için `@Bean` bildirimini kullanmalıyız. Ayrıca artık her fasulye tanımı için 'id' belirtmemize gerek yok; yöntemin ismi aynı zamânda nesne istenirken kullanılan münferid 'id' değeridir:
  
  ```java
  @PropertySource("classpath:values.properties")
  @ComponentScan("Base")
  @Configuration
  public class SpringIDARE{
      @Bean
      public MySQLDAL db(){
          return new MySQLDAL();
      }
  }
  ```

- ..

#### Çalışma Zamânında Dış Kaynaktan Değer Aktarımına Erişme

- Spring fasulyelerini Java nesneleri olarak çalışma zamânında döndüren bir yapılandırma yaptığımızda dış kaynaktan alınan dosyaların uygulama içerisine doğrudan aktarılabiliyor olması gerekir. Bunu dosya okuma yoluyla biz de yapabiliriz; fakat, madem bu işleri yapması için Spring çerçevesini kullanıyoruz, o hâlde Spring üzerinden nasıl erişilebileceğini görmeliyiz:

- Bunun için `org.springframework.core.env.Environment` sınıfından bir nesne oluşturmalıyız. Bu nesnenin üzerine `@Autowired` bildirimini ekleyerek nesnenin otomatik olarak ilklendirilmesi sağlanabilir

- Ardından `Environment` sınıf örneğinin yöntemlerini kullanabiliriz:
  
  ```java
  @PropertySource("classpath:values.properties")
  @ComponentScan("Base")
  @Configuration
  public class SpringIDARE{
      @Autowired
      Environment env;
      @Bean
      public MySQLDAL db(){
          return new MySQLDAL(env.getProperty("mysqlHost",
          Integer.class));
      }
  }
  ```

- `getProperty()` yöntemi birinci parametre olarak istenen değerin ismini, ikinci parametre olarak değerin dönüştürüleceği ('casting') veri tipinin sınıfını alır. Eğer ikinci parametre verilmezse geriye Object tipinde bir değer döndürülür.

### SPRING'TE NESNE ('BEAN') KAPSAMI

- Biz Spring'ten bir sınıf örneği istediğimizde Spring bize istediğimiz sınıfın örneğini döndürüyor; peki, her defasında aynı nesneyi mi döndürüyor?
  Varsayılan olarak, evet; fakat bu ayarı değiştirmek isteyebiliriz.

- Spring'ten her bir nesne talebinde yeni bir örnek mi döndüreceği, yoksa daha evvel ürettiği nesneyi mi döndüreceği ilgili kural düzenine 'kapsam' denir.

- Spring'te 5 çeşit kapsam vardır:
  
  1. **"singleton" (münferid, tekil)** : Tanımlanan her fasulyeden ('bean') yalnızca bir tâne üretilir; gelen her talepte aynı nesne döndürülür. Varsayılan kapsamdır.
  
  2. **"prototype" ("örneklem")** : Her istek için yeni bir nesne üretilir.
  
  3. **"request" (istek)** : 'prototype' modelinin Spring web için olan versiyon gibidir. Gelen her HTTP isteğinde yeni bir nesne döndürülür.
  
  4. **"session" (oturum)** : Her HTTP oturumunda bir nesne oluşturulur. Misal, 'UserInfo' isimli, kullanıcı bilgilerini tutan, 'bean' tanımında 'session' kapsamına sâhip bir sınıfımızın olduğunu düşünelim. Bu web uygulamasında siteye giriş yapan her kullanıcı için ayrı ayrı sınıf örneği üretilirken bir kullanıcının yaptığı işlemlerden ötürü kullanıcı bilgilerine iki kez erişmek istediğinde, bu kullanıcının ikinci isteği için yeni bir nesne üretilmez; zîrâ 'session' kapsamında, kullanıcı oturum açtığında (daha doğrusu tarayıcıda 'session' oluştuğunda) bir örnek üretilir ve o oturum için yeni bir sınıf örneği üretilmez.
  
  5. **"globalSession (küresel oturum)** : Bu kapsamda her HTTP isteğinde yalnızca bir nesne oluşturulur. Herkese aynı hizmetin verildiği ve hizmetin verilen kişiler bakımından birbirinden bağımsız olmadığı (olmasına gerek olmadığı) gibi durumlarda kullanılabilir.

- Spring'te hem 'xml' ile, hem de bildirim (notasyon) ile sınıf kapsamı belirtilebilir:
  
  ```xml
  <bean id="UserInfo" class="com.web.User" scope="session"></bean>
  ```
  
  ```java
  @Scope("session")
  public class UserInfo{/*.;.*/}
  ```

- ..

### OTOMATİK ZERK (ENJEKSİYON, AKTARMA) ve FIRLATILABİLECEK HATÂLAR ÜZERİNE

- Bir sınıfın bir özelliğini veyâ bir fonksiyonun bir parametresini otomatik olarak atayarak sınıf örneği oluşturma işlemini kolaylaştıran bir sistemdir.

- `@Autowired` bildirimiyle yapılır.

- Bir sınıfın yapıcı fonksiyonunda bir arayüz olduğunu ve bu sınıfın başka yapıcı yöntemi olmadığını düşünelim; bu sınıfın bir örneğini oluşturmak için bu arayüzü sınıf yapıcı fonksiyonuna parametre olarak vermemiz gerekiyor. Daha önce gördüğümüz gibi, bunu yapıcı yöntem parametresi ('constructor-arg) ile şekildeki gibi yapabiliyoruz:
  
  ```xml
  <bean id="EntityManager" class="Base.EntityManager">
      <constructor-arg name="dal" ref="db"/>
  </bean>
  ```

- Eğer 'class-config' yapılandırmasıyla çalışıyorsak ilgili 'bean' için yazdığımız fonksiyonu çağırarak bunu yapabiliriz:
  
  ```java
  @Configuration
  public class SpringIDARE{
      @Bean
      public INoteDAL db(){/*.;.*/}
      @Bean
      public EntityManager entityManager(){
          return new EntityManager(db());
      }
  }
  ```

- Fakat bâzı durumlarda zerk (injection) işleminin otomatik olarak yapılmasını isteyebiliriz. Bildirim (notasyon) ile tanımlamada `@Autowired` bildirimi kullanılarak bu yapabilir.
  
  ```java
  public class EntityManager{
      @Autowired
      public EntityManager(INoteDAL dal){/*.;.*/}
  }
  ```

- ***!!! :*** XML ile yapılandırmada Spring zerk işlemini otomatik olarak yapar; herhangi bir bildirimde bulunmamıza gerek yok; yalnızca zerk edilecek bağımlılığın XML içerisinde fasulye ('bean') olarak tanımlanmış olması lazımdır; fakat XML içerisinde aynı arayüzü uygulayan birden fazla 'bean' tanımı yapılmışsa, Spring bu bağımlılığı otomatik zerk edemez ve `NoUniqueBeanDefinitionException` hatâsı verir. Bu durumda, bu bağımlılık için bir `<constructor-arg>` yazmalıyız.

- ***!!! :*** Eğer INoteDAL arayüzünü uygulayan birden fazla sınıf varsa ve bu sınıflar için birden fazla bean tanımı yapılmışsa uygulama hatâ verir. Bu arayüzü uygulayan birden fazla sınıfın olması otomatik zerk işlemi için sorun değildir; bu sınıfların birden fazlası için 'bean' tanımlamış olmamız, yanî birden fazlası için `@Component` bildirimini kullamış olmamız veyâ -XML yapılandırması kullanıyorsak- birden fazlası için `<bean></bean>` etiketi oluşturmuş olmamız sorundur.

- Bu sorunu çözmenin iki yolu var. Birincisi zerk etmek istediğimiz parametre ismini ilgili arayüzü uygulayan 'bean' tanımlarından birisi olarak (istediğimiz hangisi ise) yazmak. Bu durumda Spring, ismi parametre ismiyle aynı olan sınıfı zerk edecektir.
  İkincisi ise, parametresini zerk etmek istediğimiz fonksiyonun üstüne `@Qualifier`  bildirimiyle bunu belirtmek:
  
  ```java
  public class EntityManager{
      @Autowired
      @Qualifier("MySQLDAL")
      public EntityManager(INoteDAL dal){/*.;.*/}
  }
  ```

- Konuyu bir yapıcı yöntem parametresini zerk etme üzerinden anlatmış olsak da, `@Autowired` bildirimi özellik için de kullanılabilir:
  
  ```java
  public class EntityManager{
      @Autowired
      @Qualifier("MySQLDAL")
      INoteDAL dal;
      public EntityManager(){/*.;.*/}
  }
  ```

- XML yapılandırmasında otomatik zerk işlemi yapılmaz; bu bildirimleri ekleyip, `<context:component-scan>` etiketi eklersek yapılır.

- `@Autowired` bildiriminin kullanıldığı bir diğer durum ise, birden fazla yapıcı yöntem olması durumunda Spring'in hangisini seçeceğine karar vermesini sağlamak içindir:
  
  1. Eğer parametresiz bir yapıcı yöntem varsa, aksini belirtmezseniz Spring onu seçer.
  
  2. Birden fazla yöntem varsa ve siz bir tânesine `@Autowired` bildirimi eklemişseniz, Spring onu seçer.

- ..

### Özelliklerin Atanması

- Özelliklere değer atanması için Spring'in özelliğe erişmeye ihtiyacı vardır. Bunun için de 

- 1. XML ile özellik atama : `<property>` etiketi kullanılır. Temel veri tiplerinde doğrudan değer vermek için 'value' özelliği, başka bir 'bean'in referansının atanması için 'ref' özelliği kullanılır:
     
     ```xml
     <context:property-placeholder location="classpath:val.properties/>
     <bean id="entityManager" class="Base.EntityManager">
         <property name="dal" ref="db"></property>
         <property name="version" value="3.1"></property>
         <property name="osName" value="${osName}"></property>
         <!--'val.properties' isimli dosyada tanımlanan 'osName' isimli
         değişken üçüncü özelliğe atanırken kullanılıyor-->
     </bean>
     ```
  
  2. Bildirim (notasyon, 'annotation' ile) : Bildirim ile değer atanırken kullanılabilecek birkaç bildirim vardır:
     
     ```java
     public class EntityManager{
         @PropertySource("classpath:values.properties")
         @Resource("name=db")
         INoteDAL dal;
         @Value("3.1")
         float version;
         @Value("${osName}")
         String osName;
     }
     ```
  
  3. Fasulye ('bean')leri Java koduyla tanımladığımız durumda, nesnelerin özelliklerini doğrudan veyâ 'setter' yöntemi aracılığıyla atayabiliriz:
     
     ```java
     @Configuration
     @PropertySource("classpath:values.properties")
     public class SpringIDARE{
         @Autowired
         Envoirenment env;
         @Bean
         public INoteDAL db(){/*.;.*/}
         @Bean
         public EntityManager entityManager(){
             EntityManager manager = new EntityManager();
             manager.setOsName(env.getProperty("osName", String.class));
             manager.setVersion(3.1);
             manager.setDal(db());        
             return manager;
         }
     }
     ```

- ..

### DİĞER BÂZI BİLDİRİMLER (NOTASYONLAR)

- `@Service` : Hizmet veren yapılar, iş katmanları için bu bildirim kullanılır.

- `@Repository` : 'bean' tanımlarının  yapıldığı yer olduğunu belirtmek için kullanılır.

- `@Controller` : Spring Web MVC'de gelen istekleri idâre eden, karşılayan katman olan 'Controller' katmanı olduğunu belirtmek için kullanılır. Spring boot ile `@RestController` gibi bildirimler çok kullanılır; web servisleri için kullanılan bir bildirimdir.

..
