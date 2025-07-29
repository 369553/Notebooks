# SPRING

## BU DEFTER HAKKINDA

- Bu defteri okumadan şu konuları bildiğinizden emîn olunuz:
  
  - Temel Java bilgisi
  
  - Java ile nesne yönelimli programlama bilgisi
  
  - XML dosya formatının genel yapısı (Spring context XML kısmı için)

- Bu defter, Spring'in temelini, "neden"ini, "nasıl"ını anlamak için iyi bir referans kaynak olma amacıyla oluşturulmuştur.

- Bu defter, Spring'in temel kütüphânesi olan Spring context ve Spring core kitâplığını konu edinmektedir; Spring'in Data JPA, Boot, Security gibi farklı alt kitâplıkları da vardır.

- Yazar : Mehmet Akif SOLAK

## GENEL BİLGİLER

- Spring, Java ile kurumsal uygulama geliştirmede en çok kullanılan kitâplıklardan birisidir.

- Spring'in ilk sürümü 2003 senesinde Apache 2.0 lisansıyla sunulmuş.

- Spring'in çekirdeği yaklaşık 2 MB boyutundadır; yanî oldukça hafiftir.

- Spring'in yaptığı temel işlem bir Java uygulamasının ihtiyaç duyduğu nesneleri oluşturmak, yönetmek; bağımlılıkları ele almak ve bunu otomatize etmektir, Spring'in oluşturduğu ve idâre ettiği Java nesnelerine **bean** denilir.

- Bu işlem için Spring'in yaptığı şey, uygulamadaki sınıfları tanımak (bunu biz tanıtıyoruz), nasıl oluşturulduklarını tanımlamak ve bu nesneleri kullanıcıya istediği zamân sunmaktır.

- Bilindiği üzere, nesne yönelimli programlamada bir nesne içerisinde birden fazla nesneye atıf olabilmektedir; hattâ bâzı nesnelerin oluşturulması için başka nesnelere ihtiyaç vardır. Bu durumda, bağımsız olan nesnenin ilk önce oluşturulması ve bağımlı olan nesnenin bu bağımlılığının giderilerek sonra da onun oluşturulması gerekir.

- Bu durum, bizi bağımlılıkların yönetilmesi başlığına götürür. Spring'in amacı, uygulamanızdaki bağımlılıkların tek bir yerden kontrol edilmesidir; bu, bağımlılıkların teke indirgenmesi olarak da îzâh edilebilir.

- Maven derleme ve proje idâre aracında, Spring'i projeye eklemek için **pom.xml** dosyasındaki bağımlılıklar (`<dependencies>`) kısmına şunları eklemeliyiz:
  
  ```xml
  <!-- Spring core: -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.1.5.RELEASE</version>
  </dependency>
  <!-- Spring context: -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.1.5.RELEASE</version>
  </dependency>
  ```

- ..

#### Genel Çalışma Yapısı

- Bağımlılıkların ele alınması hususunda Spring iki usûl kullanmaktadır:
  
  1. **Dependency Injection (DI) (Bağımlılığın zerk edilmesi)** : Bir sınıfın nesnesinin çalışabilmesi veyâ oluşturulabilmesi amacıyla ihtiyaç duyulan bağımlı nesnelerin ilgili nesneye zerk edilmesine verilen isimdir. Bu, basitçe kurucu metodun parametrelerinin zerk edilmesi veyâ sınıftaki ilgili alanların (fields) değerlerinin o alanlara zerk edilmesi işlemidir. Bunu kendimiz yapmak istesek Java Reflection API'yı kullanabiliriz; fakat bu işi otomatize etmek için Spring gibi bir araç yazmalı veyâ kullanmalıyız. Spring'te bağımlılıkların zerk edilmesiyle ilgili üç çeşit işlem bulunmaktadır:
     
     - **constructor-arg injection** : Yapıcı metodun parametrelerinin yapıcı metoda geçirilmesiyle ilgili sınıfın nesnesinin üretilmesi sağlanır.
     
     - **setter injection** : Üretilen nesnenin çalışabilmesi için gerekli alanların özelliklerinin ilgili alanlara zerk edilmesi için, o alanların **setter** metodunun kullanılması işlemidir. Misal, bir nesnenin **id** alanına bir değer zerk etmek istediğimizde sınıfın `getId()` metodu veyâ `get_id()` metodu kullanılır.
     
     - **field injection** : Java Reflection API gibi kitâplık(lar)la ilgili sınıfın ilgili alanına verilen değerin atanması (zerk edilmesi) işlemidir.
  
  2. **Inversion of Control (Bağımlılıkların tersine çevrilmesi)** : bağımlılıkların zerk edilmesi (**dependency injection**) aslında bağımlılıkların tersine çevrilmesi için yapılan bir işlemdir. Buna göre hangi nesneye hangi bağımlılığın zerk edileceği bilgisi nesneler tarafından belirlenmemelidir. Bu bilgi, Spring'in nesnelerin üretilmesi için esas aldığı bir bağlam (**context**) bilgisi belgesine bakarak elde edilmeli ve Spring tarafından ilgili bağımlılık zerk edilerek nesne üretilmelidir. Bu bağlam bilgisi için eskiden XML yapısı kullanılırken, artık basitliği ve okunabilirliği sebebiyle bildirim (**annotation**) yapısı tercih edilmektedir.

- Spring'te bağımlılıkların zerk edilmesi için kullanılan iki farklı metot vardır. Birincisi XML dosyasıyla yapılandırma belirtme üzerinedir; ikincisi ise bu işlemin bildirimler (annotations) ile yapılması üzerinedir. Günümüzde XML tabanlı yapılandırma tercih edilmemektedir; çünkü XML tabanlı yapılandırmanın okunabilirliği az, hatâya sebebiyet verebilirliği yüksek, kodlanması yavaştır.

- Daha iyi anlaşılması açısından Spring XML bölümünü de okumanızı tavsiye ederim.

## SPRING XML

- XML dosyası, basit bir ifâdeyle, hangi isimde nesne istendiğinde, Spring'in hangi nesneyi vereceğini ve o nesneyi oluştururken neleri o nesneye zerk edeceğini belirten bir yapılandırma dosyasıdır.
  
  - Spring xml dosyasının ismi genellikle '**applicationContext.xml**' konulmaktadır.

- Bu dosya içerisinde 'bean' tanımları yapılır; kelîme anlamı 'fasulye' olan **'bean'** bileşenleri uygulama içerisindeki nesneleri temsil eden yapılardır.

- Bu XML dosyası kabaca şöyledir:
  
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context.xsd">
  <bean></bean><!--Nesne tanımı burada yapılır-->
  </beans>
  ```

- Nesne tanımları `<beans></beans>` etiketleri içerisinde yazılmalıdır ve her nesne `<bean>` etiketiyle belirtilmelidir.

- Dilerseniz, yukarıdaki kodda referans olarak verilen adresleri ziyâret ederek, nesne tanımlama hakkındaki tüm anahtar kelîmelere bakabilirsiniz.

- Basit bir nesne tanımı şöyledir:
  
  ```xml
  <bean id="db" class="Base.MySQLDAL"></bean>
  <!-- Yukarıdaki kod Spring'ten 'db' isminde bir nesne istendiğinde
  Spring'in Base paketi altındaki 'MySQLDAL' sınıfının bir örneğini
  döndüreceğini ifâde ediyor-->
  ```

- Nesne (**bean**) tanımlarken her nesne için **id** özelliği vermeliyiz; bu, Spring'ten nesne istenirken kullanılacak olan münferid bir isimdir. Geriye döndürülecek nesnenin hangi sınıfın örneği olduğunu ise **class** özelliğiyle belirtiyoruz; yanî Spring **class** ile belirtilen sınıfın nesnesini üretip, döndürecektir. **Burada sınıfı paket ismini de içerecek şekilde tam mevkîsini belirterek yazmamız gerekiyor.**

- Bu XML dosyasıyla birlikte nesnenin nasıl oluşturulacağını Spring'e göstermiş olduk. Şimdi yapmamız gereken Spring'in başlatılmasını sağlamak için bu yapılandırma dosyasını Spring'e tanıtmaktır. Bunun için Java kodu yazıyoruz. Uygulamamızda nesneleri kullanmadan önce, şu satırları çalıştırmalıyız:
  
  ```java
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.
                             support.ClassPathXmlApplicationContext;
  ApplicationContext context;
  context = new ClassPathXmlApplicationContext(
      "applicationContext.xml"
  );
  MySQLDAL dal = context.getBean("db", MySQLDAL.class);
  ```

- `getBean()` metodunun ilk parametresi istenen nesnenin 'id' özelliğidir. İkinci parametresi ise istenen nesnenin hangi sınıftan bir nesne olarak istendiği bilgisidir. Eğer ikinci parametre verilmezse, istenen nesne `Object` nesnesi olarak gelir.

> ***NOT :*** Bir Maven projesinde sadece dosya ismi vererek dosyaya erişmek istiyorsak bu dosya proje dosya yolu listesindeki bir dizin altında bulunmalıdır. Yaygın olarak `/src/main/resources` dizini tercih edilmektedir.

- ..

#### 1) Kurucu Metoda Parametre Zerki (constructor-arg injection)

- **Spring, nesneleri oluştururken parametresiz kurucu metotları kullanır**.

- **Eğer sınıfın parametresiz kurucu metodu yoksa, Spring o sınıfı yapılandırma olmadan oluşturamaz.**

- Sınıfın ihtiyaç duyduğu bağımlılıkları kurucu metotta alması gerekebilir; bu durumda, bu kurucu metoda verilmesi gereken bağımlılıkların hangi nesneler olduğunu Spring içerisinde tanımlamamız gerekir.

- Bu durumda, `<bean>` etiketi içerisinde kurucu metot parametresini / parametrelerini belirtmemiz gerekiyor:
  
  ```xml
  <constructor-arg name="host" value="localhost"/>
  <!--Yapıcı metodun 'name' parametresine 'localhost' değeri verilir-->
  ```

- Yukarıdaki XML kodu, bir yapıcı metoda statik bir değer verilmesini sağlamaktadır. Şu kadarı var ki, yapıcı metoda vermemiz gereken değer `int`, `String` gibi temel veri tipinden bir değer olmayabilir.

- Eğer yapıcı metoda vermemiz gereken parametre bir nesne ise, önce o nesnenin oluşturulması gerekmektedir. Bunun için yapılması gereken şey, Spring XML içerisinde o nesneyi tanımlamak, nesnenin referansını bu yapıcı vermektir:
  
  ```xml
  <bean id="db" class="Base.MySQLDAL"/>
  <bean id="EntityManager" class="Base.EntityManager">
      <constructor-arg name="dal" ref="db"/>
  </bean>
  ```

- **!** `<bean>` nesnesinin `ref` özelliğiyle referans olarak verdiğimiz isim, diğer `<bean>` nesnesinin `id` veyâ `name` parametresi olabilir. Yanî yukarıdaki kodun ilk satırını şu şekilde değiştirirsek, kod yine çalışır: `<bean name="db" class="Base.MySQLDAL"/>`

- `id` yalnızca bir münferit değer alabilirken, `name` özelliğiyle birden fazla münferit değer belirtilebilir; belirtilen her değer o nesnenin ismi olur. Ayrıca `name` özelliğine sayısal değerler de verilebilir. `name` özelliği içerisinde birden fazla değer belirtmek için `,`, `;` veyâ ` ` karaketerleri kullanılır:
  
  ```xml
  <bean class="Base.MySQLDAL" name="db, dal, mySQLDB"/>
  ```

- ..

##### Yalın Verileri Hâricî Dosyadan Okuma

- Bu konu sadece kurucu metoda parametre aktarırken değil, diğer bağımlılık zerki çeşitlerinde de ihtiyaç duyulan bir meseledir.

- Kurucu metoda parametre olarak vermek istediğimiz veriler yalın (statik, temel veri tipinde bir veri) olduğunda bu verileri XML dosyasına doğrudan gömmek yerine bir dosyadan alabiliriz. Bunun için `values.properties` isminde veyâ istediğimiz başka isimde bir dosya oluşturup, verilerimizi anahtar - değer çifti olarak oraya yazmalı ve sonra XML dosyasına bu verilerin aktarılması için kod parçası eklemeliyiz. Öncelikle `values.properties` dosyamızın şöyle olduğunu düşünelim:
  
  ```properties
  db.host=localhost
  ```

- Bu değere `applicationContext.xml` dosyası içerisinden erişmek için `applicationContext.xml` dosyasına şu kodu eklemeliyiz:

- ```xml
  <context:property-placeholder location="classpath:values.properties"/>
  <!-- Buradaki 'location' dosyanın konumunu ifâde ediyor,
      'classpath' proje dizinini belirten bir değişken,
      'values.properties' ise dosyamızın ismi -->
  ```

- Böyle yapıldığında ilgili dosyadaki anahtar - değer çiftleri XML dosyasına bir değişken olarak aktarılır. XML içerisinden bu değişkene şu şekilde erişilebilir:
  
  ```xml
  <constructor-arg name="host" value="${db.host}"/>
  ```

- Dilerseniz ilgili parametrenin sırasını `constructor-arg` etiketinin `index` özelliğiyle belirtebilirsiniz. İlk parametrenin sıra numarası `0` olmalıdır.

#### 2) Bağımlılıkları 'setter - injection' Usûlüyle Zerk Etme

- Nesne özelliklerine değerlerin zerk edilmesi için kullanılabilecek bir başka yoldur.

- **Bu zerk işlemi varsayılan olarak nesne oluşturulduktan sonra yapılmaktadır.**

- Bu zerk işleminde ilgili nesnenin **setter** metodu aranmakta ve değer o metoda gönderilerek ilgili özelliğe verinin aktarılması hedeflenmektedir. Bunun için ilgili özelliği XML dosyasında belirtmeliyiz:
  
  ```xml
  <property name="host" value="${db.host}"/>
  ```

- Yukarıdaki kodu `<bean>` etiketi içerisine eklemeliyiz. `name` parametresi özelliğin ismini, `value` parametresi ise özelliğin değerini belirtmektedir.

- **!** Spring, **setter** metodunu varsayılan olarak CamelCase isimlendirme kuralına göre arar. Bu sebeple, yukarıdaki özellik için sınıf içerisinde şu isimde metot olmalıdır:
  
  ```java
  public void setHost(int host){this.host = host;}
  ```

- ..

#### 3) Nesne Özelliklerine (attribute, field) Nesne Aktarılması (field injection)

- Nesnelerin bağımlılıklarını zerketmek için kullanılabilen bir diğer yöntem de nesnelerin alanlarına verinin doğrudan alana erişerek zerk edilmesidir.

- Bunun için ilgili alanın **private** erişim belirteciyle belirtilmesi **sorun değildir**.

- Aslında bu, Spring'in yeni yaklaşımının bir ürünüdür; çünkü burada Java kodu yazıyoruz. Sınıf içerisinde ilgili alanın üzerine `@Autowired` bildirimini eklemeliyiz:
  
  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  public class EntityManager{
      @Autowired
      MySQLDAL dbAccess;
  }
  ```

- Ardından XML kodumuz içerisine (**applicationContext.xml**) Spring bildirimlerinin (anotasyonlarının) taranmasını belirten şu kodu eklemeliyiz:
  
  ```xml
  <context:annotation-config />
  ```

- **!** XML için statik verileri bu şekilde zerk edemeyiz, nesneleri zerk edebiliriz. Bunun için ilerideki `@Autowired` bildirimine bakınız.

> ***NOT :*** **field injection** nesneleri değişmez (**immutable**) olarak oluşturmak açısından tavsiye edilmez.

> ***NOT :*** Nesne özelliklerinin nesne oluşturulduktan sonra kesin olarak atanmış olmasını garanti etmek için **constructor arg injection** usûlünü tercih etmelisiniz.

- ..

#### XML İçerisinde Farklı Tipte Verilerin Tanımlanması

- Zerk etmek istediğimiz veri dizi, liste veyâ harita (`Map`) biçiminde olabilir.

- Liste için `<list></list>` etiketleri kullanılır; bu etiketler içerisinde elemanlar referans `(<ref></ref>`) veyâ değer (`<value></value>`) olarak barındırılabilir; referans elemanlar o elemanın Spring'ten isteneceği anlamına gelir; değer bazlı elemanlar ise XML dosyasında belirtilen değerin kullanılacağı anlamına gelir:
  
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
  
  ```xml
  <entry key="anahtar" value="deger"/>
  ```

- `Properties` sınıfından bir değer eklenebilir:
  
  ```xml
  <property>
      <props>
          <prop key="binDir">../bin</prop>
          <prop key="versionNum">3.21</prop>
      </props>
  </property>
  ```

- ..

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

- Spring XML günümüzde tercih edilmemektedir; bunun sebepleri fazla işgücü gerektirmesi, okunabilirliğinin az olması ve hatâ yapılabilirliğe açık olmasıdır.

- Spring'i XML dosyası üzerinden yapılandırmak çok mâliyyetli bir işlemdir. Hem fazla metîn, hem de fazla işgücü gerektiren bu yapı, değişkenlik için uygun değildir.

- Bu sebeple Spring için yeni bir usûl olan bildirim (notasyon, 'annotation') bazlı yapılandırma eklenmiştir.

- XML'deki `<bean>` etiketi yerine Java'da `@Component` bildirimi (anotasyonu) kullanılır (ayrıca `@Bean` bildirimi de kullanılır; aralarındaki farka ileride değinilecek inşâAllah..).

- Bir alana (field) veyâ bir fonksiyon parametresine bir değerin zerk edilmesi ise `@Value` bildirimiyle yapılır.

- Nesne tanımlamak için sınıfın başına `@Component("beanId")` notasyonu eklenir:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      //.;.
  }
  ```

- Bunu yapmak tek başına kâfî değildir; Spring'in bu bildirimleri taraması gerektiğini belirtmemiz gerekir. Bunun için **applicationContext.xml** dosyası içerisine şu kodları eklemeliyiz:
  
  ```xml
  <context:component-scan base-package="Base"/>
  <!-- 'base-package' özelliğine notasyon taraması yapılacak paketi
          yazmalıyız-->
  ```

- Bir alana (field) statik bir değeri zerk etmek için `@Value` bildirimi kullanılır:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      @Value("${mysqlHost}")
      int host;
      //.;.
  }
  ```

- `@Value` bildirimi yapıcı metodun parametresine veri zerk edilmesi için de kullanılır:
  
  ```java
  package Base;
  
  @Component("db")
  public class MySQLDAL{
      public MySQLDAL(@Value("${mysqlHost}"){/*.;.*/}
  }
  ```

- ..

#### Spring Class-config (Sınıf ile Yapılandırma)

- Nesne tanımlamalarını daha kolaylaşırmak için ve tek bir merkezden idâre etmek için **applicationContext.xml** yapılandırma dosyamızı Java koduyla ifâde etmeliyiz. Spring XML yapılandırma dosyamızın karşılığı olarak bir sınıfı Spring yapılandırma sınıfı olarak atayabiliriz. Bunun için `@Configuration` notasyonu kullanılır:
  
  ```java
  @Configuration
  public class SpringIDARE{
      //.;.
  }
  ```

- Bunu yaptıktan sonra uygulama içerisindeki `ClassPathXmlApplicationContext` tipinden olan 'context' nesnemizi `AnnotationConfigApplicationContext` sınıf örneğiyle değiştirmeliyiz; bu da `ApplicationContext` arayüzünü uygulayan bir sınıftır:
  
  ```java
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.
         annotation.AnnotationConfigApplicationContext;
  ApplicationContext context
      = new AnnotationConfigApplicationContext(SpringIDARE.class);
  // Girdi parametresi olarak yapılandırma sınıfımızı veriyoruz.
  ```

- **applicationContext.xml** yapılandırma dosyasında belirttiğimiz sınıf tarama kodunun notasyon karşılığı şu şekildedir; tüm satırdaki kodlar birbirleriyle aynı anlamdadır; hatâ yapmamak adına son satırdaki yazım biçimi daha uygundur:
  
  ```java
  @ComponentScan("Base")
  @ComponentScan(basePackages={"Base"})
  @ComponentScan(basePackageClasses = {MySQLDAL.class,
                  Base.MsSQLDAL.class})
  ```

- **applicationContext.xml** yapılandırma dosyasında belirttiğimiz statik değerlerin bir dosyadan okunması işleminin bildirim karşılığı ise şu şekildedir:
  
  ```java
  @PropertySource("classpath:values.properties")
  ```

- Her sınıfın üzerine bildirim eklemek yerine, tüm nesne tanımlamalarımızı bir yerde toplayabiliriz. Bu sınıfın üzerine `@Configuration` bildirimi eklemiz gerekiyor:
  
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

> ***NOT :*** Hem **applicationContext.xml** yapılandırma dosyası, hem de notasyonlar kullanıldığında dosyadan değer aktarımı işlemini XML'de yapmak daha doğru olur; çünkü `@PropertySource()` notasyonunu yazdığımızda bu kaynak dosyadaki değerleri XML içerisinde kullanamıyoruz. XML'in Spring işleme sırasında bir önceliği var gibi duruyor.

> ***NOT :*** Birden fazla XML'in olması gibi birden fazla `@Configuration` sınıfınız varsa, `AnnotationConfigApplicationContext` nesnesini parametresiz yapıcı metotla oluşturun, ilgili bağlama yeni yapılandırma sınıflarını `register()` metoduyla ekleyin ve **en son** `refresh()` metodunu çağırın:
> 
> ```java
> AnnotationConfigApplicationContext context = 
>         new AnnotationConfigApplicationContext();
> context.register(SpringIDARE2.class);// Yapılandırma sınıfını ekle
> context.register(SpringIDARE2.class);// Başka yapılandırmayı ekle
> context.refresh();// Bu satırdan sonra yeni 'register' olamaz
> ```

- ..
- ..

#### Çalışma Zamânında Dış Kaynaktan Değer Aktarımına Erişme

- Statik değerlerin dosyadan Spring projesine aktarılma işlemi Spring ile daha kolay bir şekilde yapılabilir.

- Bunun için `org.springframework.core.env.Environment` sınıfından bir nesne oluşturmalıyız. Bu nesnenin üzerine `@Autowired` bildirimini ekleyerek nesnenin otomatik olarak ilklendirilmesi sağlanabilir.

- Ardından `Environment` nesnesinin metotlarını kullanabiliriz:
  
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

## SPRING'TE NESNE ('BEAN') KAPSAMI

- Biz Spring'ten bir sınıf örneği istediğimizde Spring bize istediğimiz sınıfın örneğini döndürüyor; peki, her defasında aynı nesneyi mi döndürüyor?
  Varsayılan olarak, evet; fakat bu değiştirilebilir. Bu ayara **kapsam (scope)** denir.

- Spring'te başlıca altı çeşit kapsam vardır:
  
  1. **singleton (münferid, tekil)** : Her nesneden **sadece bir adet** oluşturulur. Spring'e gelen her talepte aynı nesne döndürülür. Varsayılan kapsamdır.
  
  2. **prototype (örneklem)** : Spring'e gelen her istekte yeni bir nesne oluşturulup, döndürülür.
  
  3. **request (istek)** : '**prototype**' kapsamının Spring web için olan hâli gibidir. Gelen her HTTP isteği için yeni bir nesne döndürülür.
  
  4. **session (oturum)** : Her HTTP oturumunda bir nesne oluşturulur. Misal, bir web uygulamasında `User` isimli, kullanıcı bilgilerini tutan bir Spring nesnemiz olsun. Bu web uygulamasında siteye giriş yapan her kullanıcı için ayrı ayrı sınıf örneği üretilirken bir kullanıcının yaptığı işlemlerden ötürü kullanıcı bilgilerine iki kez erişmek istediği durumda, kullanıcının ikinci isteği için yeni bir nesne üretilmez. Zîrâ bu kapsam çeşidinde, kullanıcı oturum açtığında (tarayıcıda bir oturum ('session') nesnesi oluştuğunda) bir örnek üretilir ve o oturum için yeni bir sınıf örneği üretilmez.
  
  5. **application (uygulama)** : Tüm web uygulaması boyunca bir örnek paylaşımlı olarak kullanılır.
  
  6. **websocket (web soket)** : Her **websocket** oturumu için bir örnek oluşturulur.

> ***NOT :*** Web ile ilgili kapsamları seçebilmeniz için projenize Spring'in web modülünü eklemeniz gerekmektedir.

- Spring'te nesne kapsamı XML ile veyâ bildirim (notasyon) ile belirtilebilir:
  
  ```xml
  <bean id="User" class="com.web.User" scope="session"/>
  ```

- Aşağıdaki Java kodu da aynı işlevi yerine getirir:
  
  ```java
  import org.springframework.stereotype.Component;
  import org.springframework.context.annotation.Scope;
  @Scope("session")
  @Component("user")
  public class User{/*.;.*/}
  ```

> ***NOT :*** Kapsamların isimleri yukarıdaki listede belirtildiği gibi küçük harfle yazılmalıdır.

> ***NOT :*** Kendi özel kapsamınızı yazabileceğiniz gibi, ileri seviye işlemlerde ihtiyaç duyulduğu takdirde, thread boyunca geçerli olan özel kapsamı da kullanabilirsiniz.

- ..

## SPRING'te OTOMATİK ZERK (@Autowired) ve OLASI HATÂLAR

- Spring'te bir sınıfın bir özelliğini veyâ bir fonksiyonun bir parametresini otomatik olarak atayarak sınıf örneği oluşturma işlemini kolaylaştıran bir sistem vardır.

- Bu sistem `@Autowired` bildirimiyle özelliklere veyâ metot parametrelerine uygulanabilir.

- `@Autowired` bildirimi Spring'in 2.5 sürümüyle getirilmiştir.

- `@Autowired` bildirimi nesne alanına, yapıcı metoda, setter metoda veyâ herhangi bir metoda uygulanabilir.

- Bİr örnek vermek gerekirse, bir yapıcı metot parametresinde bir arayüz (`interface`) nesnesi alınıyor; buradaki yapıcı metodun üstüne `@Autowired` bildirimini eklediğimizde Spring,
  
  - bu arayüzü uygulayan sınıfı bulur
  
  - bulduğu o sınıfın bir nesnesini oluşturur
  
  - ve ilgili yapıcı metoda parametre olarak verir.

- Bunun için `@Autowired` bildirimini metodun üstüne eklemeliyiz:
  
  ```java
  public class EntityManager{
      @Autowired
      public EntityManager(INoteDAL dal){/*.;.*/}
  }
  ```

- `@Autowired` bildirimi '**setter-injection**' yapmak için kullanılabilir:
  
  ```java
  @Autowired
  public void setINoteDAL(INoteDAL dal){}
  ```

- **field-injection** yapılırken de kullanılır:
  
  ```java
  public class EntityManager{
      @Autowired
      INoteDAL dal;
      public EntityManager(){}
  }
  ```

- Bâzı durumlarda `@Autowired` bildirimi kifâyet etmez. Eğer sisteminizde söz konusu arayüzü uygulayan birden fazla sınıf varsa ve bu sınıfların her biri Spring tarafından tanınıyorsa uygulama `NoUniqueBeanDefinitionException` hatâsı verir.

#### Birden Fazla Arayüz Uygulayıcının Olduğu Durumu Ele Alma

- Bu sorunu çözmek için `@Primary` ve / veyâ `@Qualifier` bildirimleri kullanılır.

- `@Qualifier` bildirimi bir arayüzü birden fazla uygulayan sınıf olduğunda, hangisinin ilgili alana veyâ metot parametresine zerk edilmesini istediğimizi açıkça belirtmemizi sağlar.

- Misal, `CustomerDal` arayüzünü uygulayan `MysqlCustomerDal` ve `MssqlCustomerDal` sınıflarının olduğunu düşünelim. Bu durumda sınıfın ilgili arayüzünün üstünde hangi sınıfın zerk edilmesini istediğimizi açıkça belirtebiliriz; fakat ilgili nesnenin **bean** isminin yazılması gerektiğine dikkat ediniz (sınıf ismi değil):
  
  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.beans.factory.annotation.Qualifier;
  import org.springframework.stereotype.Component;
  
  @Component("customerService")
  public class CustomerService {
      @Autowired
      @Qualifier("mySQL")
      public CustomerDal dbDal;
  }
  ```

- Eğer `@Autowired` bildirimi eklenmiş her `CustomerDal` tipindeki parametreler için `@Qualifier` bildirimi eklersek program hatâdan kurtulur. Bunun yerine bir sınıfı varsayılan olarak seçmek ve her parametre için `@Qualifier` bildirimi eklemek zorunda kalmamak için `@Primary` bildirimi kullanılır:
  
  ```java
  @Component("msSQL)
  @Primary
  public class MssqlCustomerDal implements CustomerDal{}
  ```

- Hem `@Qualifier` bildirimi, hem de `@Primary` bildirimi kullanıldığında zerk işlemi `@Qualifier` bildirimine göre yapılır.

#### @Autowired Bildiriminin Başka Kullanım Amacı

- `@Autowired` bildiriminin kullanıldığı bir başka durum Spring'in hangi yapıcı metodu seçeceğini belirtmedir. Eğer sınıfın parametresiz kurucu metodu varsa -aksini belirtmediğiniz müddetçe- Spring sınıfın nesnesini oluşturmak için parametresiz yapıcı metodu seçer. Eğer siz parametreli yapıcı metodun seçilmesini istiyorsanız onun üzerine `@Autowired` bildirimi ekleyerek bunu belirtmiş olursunuz.

- Eğer bir sınıfta bir adet yapıcı metot varsa ve bu yapıcı metodun zerk edilebilir (**injectable**) bir bağımlılığı varsa, bu kurucu metodun üstüne `@Autowired` bildiriminin eklenmesine gerek yoktur; Spring ilgili bağımlılığı bulup, o parametreye zerk eder. Bu özellik Spring'in 4.3 sürümüyle sunulmuştur.

- ..

## Diğer

- `@Import` : Bir veyâ daha fazla Spring nesnesini (`@Component` veyâ `@Bean` bildirimiyle süslenmiş) içeri aktarmak için kullanılır. Misal, `@Configuration` sınıfınızın tepesine `@Import(Base.MySQLDAL)` bildirimini eklerseniz, eklediğiniz bu sınıfta bir `@Bean` veyâ `@Component` tanımı varsa bunlar içeri aktarılmış olur.

- ..
