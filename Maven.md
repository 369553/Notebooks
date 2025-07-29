# MAVEN

## GENEL BİLGİLER

- Maven, Java için bir paketleme ve derleme organizasyon aracıdır; buna proje idâre aracı da denebilir.

- Açık kaynaklı olarak geliştirilen Maven ile;
  
  - bağımlılıkları tek bir yerden kolayca yönetme,
  
  - projelerinizi farklı ortamlara kolayca taşıma,
  
  - derleme ve test süreçlerini otomatikleştirme,
  
  - proje gereksinimleri, projenizin derleneceği Java sürümü gibi yapılandırmalarınızı kolay anlaşılabilir bir pom.xml dosyasıyla ifâde etme,
  
  - otomatik proje dokümantasyonu oluşturma
  
  gibi işlevleri kolayca gerçekleştirebilirsiniz.

- Bunun yanında Jenkins gibi CI (Continuous Integration (Sürekli Entegrasyon)) araçlarına sorunsuz şekilde entegre olma, ekosistem desteğiyle standart proje şablonlarına kolayca ulaşma, sorun ve destek bulma gibi ek faydaları da vardır.

- Maven, projelerin kolayca derlenmesi, düzenlenmesi gibi işlemleri kolaylaştırmak ve bu işlemleri otomatikleştirmenin önünü açmak için standart bir dosya dizin yapısı sunmaktadır. Bu, geliştirme ortamlarının projeyi tanımasını ve yönetmesini kolaylaştırmaktadır.

- Maven'ın internet adresi şurasıdır: [https://maven.apache.org](https://maven.apache.org)

- Maven'ın en temel yapısı "**pom.xml**" ismiyle tutulan Proje Nesne Modeli (**Project Object Model**) dosyasıdır. Projenin bağımlılıkları, hedef sürümü ve derleme sürümü gibi yapılandırmalar bu dosyayla belirtilmektedir. Bu dosya, insân tarafından okunup, anlaşılabilen bir şekilde XML biçiminde yazılan bir dosyadır.

- Maven **pom.xml** dosyasındaki bağımlılıklara bakar ve bu bağımlılıkları yerel Maven deposunda arar; eğer bu bağımlılıkları yerel Maven deposunda bulamazsa uzak Maven deposundan ([https://repo.maven.apache.org/maven2/](https://repo.maven.apache.org/maven2/)) indirir. İndirilen bu JAR dosyaları yerel Maven deposunda saklanır; böylece her defasında uzak sunucuya gidilmez.

- Projeye bağımlılık eklemek için Maven depo tarayıcısını ziyâret etmeli ve oradaki ilgili kodu **pom.xml** dosyasına eklemeliyiz.

- Maven hafif ve etkili bir proje yönetim aracıdır. Maven'dan daha hafif sayılabilecek; fakat bu özellik ve esneklikleri sunmayan **Apache ANT** aracı vardır. Maven aracının muadili sayılabilecek ve kullanımı yaygın olan bir diğer araç ise **Gradle**'dır.

> ***NOT :*** Defterde hangi ayarların ne anlama geldiği belirtilmektedir; fakat bu, her ayarı elle belirtmeniz gerektiği anlamına gelmemektedir. Maven komutları, Maven eklentileri pek çok yapılandırma ayarını sizin yerinize yapmaktadır.

- Yazar : Mehmet Akif SOLAK

### MAVEN NASIL KURULUR

- Maven'ı kullanabilmek için bilgisayarımıza kurmalı ve işletim sistemi dosya yoluna eklemeliyiz.

- Bunun için [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi) adresini ziyâret ediniz.

- Buradan Maven'ın işletim sisteminiz için olan ikili (binary) biçimindeki hâlini indiriniz.

- İndirdiğiniz arşiv dosyasını çıkartınız ve herhangi uygun bir yere taşınız.

- Ardından bu dizin içerisinde bulunan **bin** dizininin dosya yolunu işletim sisteminizin **path** ortam değişkenine ekleyiniz; bu sayede Maven'ı programın dosya yolunu vermeden kullanabilirsiniz.

- Ayrıca IntelliJ IDEA gibi profesyonel geliştirme ortamları kullanıyorsanız ve Maven'ı tekrardan kurmanıza gerek yok; dilerseniz Ayarlar kısmından Maven'ın adresini alıp, dosya yolunu sistem **path** değişkenine ekleyerek geliştirme ortamıyla gelen Maven'ı başka yerlerden de kullanabilirsiniz.

- Maven bağımlılıkları indirdikçe diskinizde yer kaplanacağından -farklı versiyonları gerekmedikçe- sisteminizde bir tâne Maven bulundurmanız yer israfını önler.

### YAPILANDIRMA DOSYASI (pom.xml) GENEL YAPISI

- XML formatındaki bu belge, projeyle ilgili bağımlılıkların, yapılandırmaların, kaynak ve hedef dizinlerin, kaynak ve hedef Java sürümünün belirtildiği bir dosyadır.

- Aşağıdaki kod örnek **pom.xml** dosyasını ve etiketlerin anlamlarını göstermektedir: 
  
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project><!--Projeyle ilgili tüm bilgiler bu etiket altında olmalı-->
      <modelVersion>4.0.0</modelVersion><!-- Bu versiyon 4.0.0 olmalı-->
      <groupId>com.alanAdim</groupId><!--paket veyâ alan adı-->
      <artifactId>ilk-uygulamam</artifactId><!--Proje ismi-->
      <version>1.0.0</version><!--Uygulama versiyon no -->
      <name>UygulamaGorunurIsmim</name><!--uygulama ismi-->
      <description>Bu uygulama hakkında açıklama</description>
      <properties><!-- Kullanılan değişkenler buraya yazılır-->
          <java.version>1.8</java.version><!--Spring Java belirtimi-->
      </properties>
      <dependencies><!--Bağımlılıklar, bu etiket altında olmalı-->
      </dependencies>
      <build><!-- Proje derlenme ayarları buraya yazılır-->
      </build>
  </project>
  ```

- Ana projenin **pom.xml** yapılandırma dosyası proje kök dizininde bulunur. Alt uygulamaların **pom.xml** dosyaları da kendi kök dizinlerinde bulunur. Bu alt uygulamaların ana uygulamanın altında olduğunu belirtmek için alt uygulamaların **pom.xml** dosyaları içerisinde `<parent>` etiketi şu şekilde kullanılır:
  
  ```xml
  <project>
      <modelVersion>4.0.0</modelVersion>
      <parent><!-- Bu etiketin altında proje ana bilgisi belirtilir -->
          <modelVersion>4.0.0</modelVersion>
          <groupId>com.alanAdim</groupId>
          <artifactId>ilk-uygulamam</artifactId>
      </parent>
      <version>1.25.3</version>
      <dependencies><!-- ... --></dependencies>
  </project>
  ```

> ***NOT :*** Eğer ana uygulamamızın sürüm (version) bilgisinin tüm alt uygulamalar için de aynı olmasını istiyorsak, alt uygulamaların **pom.xml** dosyası içerisinde sürüm numarası belirtmemeliyiz.

> ***NOT :*** Eğer ana uygulamamızın **pom.xml** dosyası ve dizini henüz belli değilse, alt uygulama içerisinde ana uygulamanın bilgisini yazarken `<relativePath>` etiketi kullanmalıyız.

> ***NOT :*** `<modelVersion>` etiketi Maven POM modelinin sürümünü belirtir.

> ***NOT :*** XML versiyon ve şema bilgisini dosyada belirtmek için şu özellikleri **pom.xml** dosyasının başındaki `<project>` etiketi için belirtebilirsiniz:
> 
> `xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
> xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"`

- Yukarıdaki **pom.xml** dosyasındaki tüm etiketlerin kullanılmasına gerek olmadığı gibi, daha fazlası da kullanılabilir.

- Kullanılabilecek diğer etiketlerin bâzıları şunlardır:
  
  - `<packaging>` : Projenin paketlenme biçimini ('jar' veyâ 'war') belirtir.
  
  - `<url>` : Projenın adresini belirtmek için kullanılır.
  
  - `<plugins>` : Proje üzerinde çalıştırılmak istenen eklentiler bu etiket altında, her biri ayrı ayrı `<plugin>` etiketi olacak şekilde eklenir. Eklentiler test, yayına alma adımları gibi farklı amaçlar oluşturulan ve birer komut biçiminde çalıştırılan yapılardır.
  
  - `<repositories>` : Uzak sunucu adresi belirtmek için kullanılır. Bu uzak sunucu deposu bağımlılıkların indirilmesi sırasında taranır; eğer merkezî depoda olmayan, fakat adresini bildiğiniz bir paket varsa bunu bu etiket altında `repository` etiketiyle bildirebilirsiniz.
  
  - `<distributionManagement>` : Proje dağıtım idâresi kurmak için kullanılır.
  
  - `<scm>` : Kaynak kontrol idâresi anlamına gelen 'source control management' yapısı için ayarların tutulduğu kısımdır.
  
  - `<issueManagement>` : Projeyle ilgili sorunların idâre edilmesi için kullanılır.
  
  - `<ciManagement>` : Devamlı entegrasyon sistemi kurmak için kullanılır.
  
  - `<mailingLists>` : Projeyle ilgili olarak 'commit'ler için, kullanıcılar için, geliştiriciler için, duyurular için ve daha fazlası için birer e-posta listesi belirtilebilir.
  
  - `<developers>` : Projenin geliştiricilerini belirtmek için kullanılır.
  
  - `<contributors>` : Projeye destek verenleri belirtmek için kullanılır.
  
  - `<licenses>` : Projeyle ilgili lisanslar bu etiket altında belirtilir.
  
  - `<modules>` : Projenin paketleri (modülleri) bu etiket altında belirtilir.
  
  - `<profiles>` : Bir derleme profili oluşturmak için kullanılır.

- Spring için gerekli Java sürümü yukarıdaki gibi `<properties>` altındaki `<java.version>` etiketiyle bildirilir; Maven için derleme için kaynak ve hedef sürümü belirtimi ise şu şekilde yapılır:
  
  ```xml
  <properties>
      <maven.compiler.source>1.8</maven.compiler.source>
      <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  ```

- **pom.xml** dosyası içerisinde dosya içerisindeki başka bir değer -JQuery'de olduğu gibi- kullanılabilir:
  
  ```xml
  <properties>
      <java.version>1.8</java.version>
      <maven.compiler.source>${java.version}</maven.compiler.source>
      <maven.compiler.target>${java.version}</maven.compiler.target>
  </properties>
  ```

> ***NOT :*** Bilindiği üzere projenin hangi sürüm için derlendiği bilgisiyle, hangi sürüm kodunun derlendiği bilgisi birbirinden farklıdır. `<maven.compiler.source>` etiketi kaynak kodun hangi Java sürümünde yazıldığı bilgisini belirtirken, `<maven.compiler.target>` etiketi ise derlenen paketin hangi Java sürümünde çalıştırılmak için derleneceği bilgisidir. Eğer kaynak kodunuz daha yeni bir sürümde yazılmışsa ve yeni gelen bir özelliği kullanmışsanız, kodu alt sürüm için derleyemezsiniz.

> ***NOT :*** Java 9'dan sonraki sürümler için `<maven.compiler.release>` etiketini kullanmak v e hedeflediğimiz Java sürümünü bu etiketle belirtmek daha iyi bir yaklaşımdır. Çünkü, eski usûlde çapraz derleme için `-bootclasspath` parametresi vermemiz gerekiyor; fakat yeni yaklaşımda derleyici, çapraz derleme için otomatik olarak yapılandırılıyor.

- **pom.xml** dosyası içerisinde `<properties>` altında değişken tanımlayarak bunları tüm **pom.xml** dosyasında kullanabilirsiniz. Misal:
  
  ```xml
  <properties>
      <spring.version>6.2.7</spring.version>
  </properties>
  ```

- Bunu bu şekilde ayarladıktan sonra bağımlılıklar kısmında bunu kullanabiliriz; Böylece Spring bağımlılığının sürüm numarası tek yerden kontrol edilebilir:
  
  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>${spring.version}</version>
      </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-core</artifactId>
          <version>${spring.version}</version>
      </dependency>
  </dependencies>
  ```

- Kodlarınızın "UTF8" karakter kodlamasına göre kodlanması için `<property>` belirtebilirsiniz:
  
  ```xml
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  ```

- Misal, eklentinin sürüm numarasını projenin sürüm numarasıyla aynı yapmak için `<version>` etiketi değerine `${project.parent.version}` yazılır.

### BAĞIMLILIKLARI EKLEME

- Bağımlılıkları eklemek için ilgili bağımlılığı ifâde eden bâzı bilgileri bilmemiz gerekmektedir.

- Bunun için Maven depo tarayıcısını ziyâret etmeli ve oradaki ilgili kodu **pom.xml** dosyasına eklemeliyiz.

- Resmî Maven deposu tarayıcısını ([https://central.sonatype.com/](https://central.sonatype.com/)) ziyâret edebiliriz; fakat kullanım kolaylığı açısında [https://mvnrepository.com/](https://mvnrepository.com/) adresi daha uygundur. Bu adres de bağımlılıkların resmî Maven deposundan çekilmesi için gereken XML kodunu sağlar; fakat arayüzü daha kullanışlıdır.

- Yapılandırmalar `<dependencies>` etiketi altındadır ve şu biçimdedir:
  
  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
  </dependency>
  ```

- `<optional>true</optional>` etiketi bağımlılığın zorunlu olmadığı durumları ifâde etmek için kullanılır. Misal, tüm veritabanları için çalışmasını istediğiniz bir uygulama yazıyorsanız, tüm veritabanlarının JDBC bağlantı arayüzlerini bağımlılık olarak **pom.xml** dosyasına eklemelisiniz; fakat uygulama çalışırken sadece bir veritabanıyla çalıştığı durumda, diğer bağımlılıkların uygulamaya gereksiz yere eklenmesini önlemek için her bir bağımlılığa bu kodu eklemeniz doğru olur.

- **!!!** Maven projesinde bilmemiz gereken en önemli şeylerden birisi de hâricî JAR dosyalarının projeye nasıl ekleneceğidir. Hâricî JAR dosyasını bir bağımlılık olarak tanıtarak projeye ekleyebilirsiniz:
  
  ```xml
  <dependency>
      <groupId>UygulamaPaketIsmi</groupId>
      <artifactId>hariciJar</artifactId>
      <scope>system</scope>
      <version>1.0</version>
      <systemPath>src\lib\hariciJar.jar</systemPath>
      <!-- Yukarıdaki parametre JAR dosyasının adresidir -->
  </dependency>
  ```

- `<scope>` etiketi kapsam durumunu belirtir; alabileceği bâzı değerler şunlardır:
  
  - `compile` : Varsayılan kapsam değeridir. Bu, ilgili bağımlılığın derlenirken yüklenmesi anlamı taşır.
  
  - `runtime` : İlgili bağımlılığa çalışma zamânında ihtiyaç duyulması anlamı taşır. Misal, JDBC sürücü arayüzleri için `runtime` kapsam değeri belirtilir.
  
  - `test` : İlgili bağımlılığa yalnızca test aşamasında ihtiyaç duyulduğu belirtilir.
  
  - `provided` : Bu, ilgili bağımlılığın uygulamanın uygulama çalışma zamânında JDK tarafından veyâ uygulamanın çalışacağı konteyner tarafından sağlanacağını belirtmek için kullanılır.
  
  - `import` : Eğer `<dependency>` etiketinin `<type>` etiketi "pom" ise bu kapsam seçilir. 
  
  - `system` : `provided` parametresine benzerdir; fakat ilgili bağımlılığın sistemdeki adresini tam olarak işâret etmemizi gerektirir.

- İndirilen paketler (bağımlılıklar) `$HOME/.m2/repository` adresinde saklanmaktadır.

- Eğer merkezî Maven deposunda istediğiniz bağımlılık yoksa, Maven'ın ilâve taramasını istediğiniz depoları `<repositories>` altında belirtiniz.

### MAVEN PROJELERİNİN GENEL DOSYA - DİZİN YAPISI

- Aşağıdaki örneklerde proje kök dizini `/` ile ifâde edilmektedir.

- `/pom.xml` : Uygulama POM dosyası.

- `/LICENSE.txt` : Lisans bilgisi dosyası

- `/README.txt` : Proje tanıtım dosyası

- `NOTICE.txt` : Hâricî (3rd party) kütüphânelerle ilgili uyarılar

- `/src` : Kaynakların bulunduğu dizin

- `/src/main/java` : Kaynak kod dosyalarının bulunduğu dizin

- `/src/main/test` : Test kod dosyalarının bulunduğu dizin

- `/src/main/webapp` : Eğer uygulama Web uygulaması ise dosyaları burada yer alır.

- `/src/main/resources` : Java sınıf yolu kaynakları

- `/src/test/resources` : Birim test için kaynakların bulunduğu dizin

- `/target` : Hedef çıktılar buraya yerleştirilir.

- `/target/classes` : Derleme sonucu oluşan '.class' dosyalar burada yer alır.

- `/target/test/test-classes` : Derlenen test sınıfları burada bulunur.

### MAVEN KOMUTLARI

- Yaptığımız tüm bu yapılandırmalardan sonra, derleme, testleri çalıştırma gibi işlemleri komutlarla yapabiliriz.

- Maven komutları Super POM isimli dosyadaki eklentileri (plugins) kullanarak işlem yapar. Bu işlem aşama anlamına gelen 'phase' kelîmesiyle tanımlanır.

- Komutların genel yapısı şu şekildedir:
  
  ```shell
  mvn [options] [<goal(s)>] [<phase(s)>]
  ```

- Başlıca Maven komutları şu şekildedir:
  
  - `mvn compile` : Dosyaları derler; fakat işlem akışında kendisine kadar olan kodları da çalıştırır.
  
  - `mvn clean` : Derlenmiş dosyaları temizler; yanî **target** dizinini siler.
  
  - `mvn test` : Birim test dosyalarını derler ve birim testleri çalıştırır.
  
  - `mvn package` : Projeyi paketler; 
  
  - `mvn site` : Proje dokümantasyonu oluşturur.
  
  - `mvn deploy` : Projeyi uzak sunucuya göndermek için kullanılır; fakat kendisine kadar olan tüm süreci de çalıştırır.
  
  - `mvn validate` : Pek bir şey yapmaz; projenin doğruluğunu kontrol eder.
  
  - `mvn verify` : Paket doğruluğunu kontrol eder; fakat kendisine kadar olan tüm süreci de çalıştırır.
  
  - `mvn install` : Projeyi derler ve yerel depoya yükler; fakat kendisine kadar olan tüm süreci de çalıştırır.
  
  - `mvn archetype` : Hâzır şablonlarla proje oluşturmak için kullanılır. 
  
  - `mvn eclipse:eclipse` : Eclipse projesi oluşturur.

- Temel komutlar yukarıdaki gibidir. Sık kullanılan örüntülerden bâzıları ise şöyledir:
  
  - `mvn dependency tree` : Proje için bağımlılık ağacı oluştur
  
  - `mvn dependency analyze` : Bağımlılıkların kullanılıp, kullanılmadıklarını analiz eder(?)
  
  - `mvn -help` : Yardım dokümantasyonunu gösterir
  
  - `mvn archetype:generate` : Örnek bir  Maven projesi oluşturur.
  
  - `mvn clean package` : Derlenmiş dosyaları temizler ve süreci paketleme işlemi de dâhil olacak şekilde paketleme işlemine kadar çalıştırır.
  
  - `mvn clean install` : Derlenmiş dosyaları temizler ve tüm süreci çalıştırır (deploy hâriç).
  
  - `mvn dependency:copy-dependencies` : Uzak depodaki bağımlılıkları yerel depoya kopyalar.

- Maven komutlarını kullanırken bilmemiz gereken bâzı parametreler vardır. Bu parametreler komut kelîmesinden önce arada boşluk olacak biçimde yazılır:
  
  - `-D` : Bir değişken tanımlamak için kullanılır. Misal, proje oluştururken proje ismini tanımlamak için `-DArtifactId=proje-ismi` yazılır.
  
  - `-P` : Bir derleme profili belirtmek için kullanılır. Peşine profil ismi belirtilmeli.
  
  - `-V` : İşleme başlanmadan evvel Maven sürüm numarasını gösterir.
  
  - `-X` : Maven komutunu hatâ ayıklama modunda çalıştırır.
  
  - `-e` : İşlem yapılırken oluşan hatâları görmek için kullanılır.
  
  - `-T` : İşlemin birden fazla thread ile yapılması için kullanılır, peşine bir boşluk koyup, istenilen iplik (thread) sayısı yazılmalıdır. Bu, çok paket barındıran projelerde derleme performansını arttırmak için kullanışlı bir parametredir.
  
  - `-q` : İşlemi sessiz modda çalıştırır; yalnızca hatâ ve test durumları gösterilir.
  
  - `-f` : İşlemi başka bir **pom.xml** dosyasıyla yapmaya zorlamak için kullanılır. Peşine bir boşluk koyup, ilgili POM dosyasının adresi verilmelidir.
  
  - `-o` : Maven komutunu çevrimdışı modda çalıştırır.

- ..

### Maven İşlem Adımları

- Maven işlem adımları kendisine kadar olan işlem adımlarını koşmaktadır; fakat tekraren yapılması gerekmeyen işlemleri tekrar çalıştırmaz.

- `validate` : Projenin doğruluğunu kontrol eder.

- `compile` : Projeyi derler.

- `test` : Birim testleri çalıştırır

- `package` : Projeyi paketler.

- `integration-test` : Birleştirme testlerini koşar.

- `verify` : Paket doğruluğunu kontrol eder.

- `install` : Paketi yerel Maven deposuna yükler.

- `deploy` : Projeyi uzak sunucuya gönderir.

- Komut çalıştırmak için `mvn`'den sonra bir boşluk bırakarak ilgili işlemi yazmalısınız.

- Birden fazla işlemin peş peşe yapılmasını istiyorsanız `mvn clean install` gibi peş peşe yazabilirsiniz; fakat son adımı yazmak önceki tüm adımları kapsadığından bu şekildeki bir kod çalıştırma şekline pek ihtiyaç duyulmaz; fakat Maven derleme işleminin tekrar etmemesine gerek duymuyorsa o işlemi çalıştırmayacaktır; bu sebeple işlemi sıfırdan yapmak için `mvn clean install` kodunu kullanabilirsiniz.

> ***NOT :*** Bu sürecin müşahhas bir parçasını çalıştırmak istersek şu biçimde çalıştırabiliriz: `mvn compiler:compile` -> Sadece derler
> Tabi, buraya verebileceğimiz işlemlerin sayısı sınırlıdır. Buna göre şu komutları çalıştırabiliriz:
> `mvn compiler:compile`, `mvn compiler:help`, `mvn compiler:testCompile`

- ..

#### Proje Oluşturma

- Bunun için `mvn archetype` komutu kullanılır.

- `mvn archetype:generate` ile hâzır şablonda bir Java projesi oluşturulur. Bunun için şablon ismi `archetypeArtifactId` parametresiyle verilmelidir. Aşağıdaki kod standart bir Java projesi oluşturmaktadır:
  `mvn archetype:generate -DgroupId=paketIsmi -DartifactId=ProjeIsmi -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

- Hâzır şablonların isimleri için bakınız : [https://maven.apache.org/archetypes/](https://maven.apache.org/archetypes/)

- Bâzı hâzır şablonlar şöyledir:
  
  - `maven-archetype-quickstart` : Standart, yalın bir Java projesi oluşturur.
  
  - `maven-archetype-j2ee-simple` : Basit bir J2EE uygulaması oluşturur.
  
  - `maven-archetype-plugin` : Örnek bir Maven eklentisi (plugin) oluşturur.
  
  - `maven-archetype-webapp` : Örnek bir web uygulaması oluşturur.

- `interactiveMode=true` parametresi proje oluşturulurken gerekli parametrelerin kullanıcıya sorulmasını sağlar. Eğer vermeniz gereken tüm parametreleri verdiğinizden emînseniz ve / veyâ komutu bir "CI/CD pipeline" süreci içerisinde kullanacaksanız interaktif modu kapalı konuma getiriniz.

- ..

### EKLENTİLER (PLUGINS)

- Eklentiler, birden fazla işlemin bir arada yapılmasını sağlayan, yanî işlemleri otomatize etmeyi sağlayan yapılardır.

- Derleme eklentisi için basit bir eklenti oluşturulabilir:
  
  ```xml
  <build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
    <!-- Maven Java'yı bulamazsa şu iki satır eklenebilir: -->
                <fork>true</fork>
                <executable>C:\Java\jdk1.8.0\bin\javac.exe</executable>
            </configuration>
        </plugin>
    </plugins>
  </build>
  ```

- Maven'da iki tip eklenti vardır:
  
  1. **build** : Derleme işlemi esnasında çalışan eklentilerdir. Misal, `clean`, `install`..
  
  2. **reporting** : Dokümantasyon 

- Bir eklentinin ne anlama geldiğini öğrenmek için şu kodu çalıştırabiliriz:
  `mvn PLUGIN_NAME:help`

- ..

### DERLEME PROFİLİ

- Derleme profili, derleme işleminin hangi kaynak sürümden, hangi hedef sürüm doğru yapıldığını, testlerin yapılıp, yapılmayacağını ve daha başka yapılandırmları içeren ve tek bir isimle çağrılabilen bir yapılandırılmış derleme seçeneğidir.

- Basit olarak şu yapıdadır:
  
  ```xml
  <profile>
      <id>profilIsmi</id><!-- Derleme profilinin ismi -->
      <properties><!-- Derlemeyle ilgili ayarlar burada belirtilmeli -->
          <maven.test.skip>true</maven.test.skip>
      </properties>
  </profile>
  ```

- Maven kodunu aktif hâle getirip, çalıştırmak için kodu çalıştırırken `-P` parametresi kullanılabilir: `mvn package -P profilIsmi `

- Profilin her zamân aktif olması isteniyorsa, bu durum **pom.xml**'de belirtilebilir:
  
  ```xml
  <profile>
      <id>profilIsmi</id><!-- Derleme profilinin ismi -->
      <properties><!-- Derlemeyle ilgili ayarlar burada belirtilmeli -->
          <maven.test.skip>true</maven.test.skip>
      </properties>
      <activation>
          <activeByDefault>true</activeByDefault>
      </activation>
  </profile>
  ```

- Yukarıdaki gibi yapıldığında,`-P` parametresiyle profil ismi belirtmeye gerek yoktur; fakat başka bir profili kullanmak isterseniz `-P` parametresiyle belirtmeniz kâfî..

- Apache'nin kılavuzda belirttiği şu örnek Windows için Windows kitâplığını, Linux için Linux kitâplığını kullanan iki profilin otomatik olarak aktifleştirilmesini gösteriyor (düzeltilmesi lazım):
  
  ```xml
  <profiles>
    <profile>
      <id>release-profile</id>
      <activation>
        <os>
          <family>windows</family>
        </os>
      </activation>
      <dependencies>
        <dependency>
          <groupId>swt</groupId>
          <artifactId>swt-win32</artifactId>
          <version>3.2.1</version>
        </dependency>
      </dependencies>
      <build>
        <filters>
          <filter>src/main/filters/releaseVersion.properties</filter>
        </filters>
      </build>
    </profile>
    <profile>
      <id>unix</id>
      <activation>
        <os>
          <family>unix</family>
        </os>
      </activation>
      <dependencies>
        <dependency>
          <groupId>swt</groupId>
          <artifactId>swt-linux-gtk</artifactId>
          <version>3.1.1</version>
        </dependency>
      </dependencies>
      <build>
        <filters>
          <filter>src/main/filters/demoVersion.properties</filter>
        </filters>
      </build>
    </profile>
  </profiles>
  ```

- ..

### BİRDEN FAZLA JAR ÇIKTISINI TEK DAĞITIMLA SUNMA

- ..

### BİRDEN FAZLA PROJEYİ İDÂRE ETME

- Maven'da birden fazla projeyi idâre etmek için önce ana POM dosyasını oluşturmalı ve bu dosyaya `<packaging>pom</packaging>` kodunu eklemeliyiz.

- Ardından her bir alt projenin POM dosyalarını oluşturmalıyız.

- Ardından ana POM dosyasını açmalı ve ona ilgili alt projeleri tanıtmalıyız:
  
  ```xml
  <modules><!-- Alt projeleri artifactId'leri ile tanıtıyoruz: -->
      <module>altProjeArtifactId</module>
      <module>altProje2ArtifactId</module>
  </modules>
  ```

- Ardından her alt projenin POM dosyasına ana projeyi `parent` olarak tanıtmalıyız:
  
  ```xml
  <parent>
      <artifactId>anaProjeArtifactId</artifactId>
      <groupId>anaProjeGroupId</groupId>
      <version>anaProjeSurumBilgisi</version>
  </parent>
  ```

- Birden fazla projeyle çalışırken alt projelerin bağımlılıklarını `<dependencyManagement>` etiketi altında belirtmeliyiz. Alt POM dosyasında versiyon numarasını belirtmediğimiz bağımlılıkların sürüm numarası ana POM dosyasından alınır.

- Ana POM dosyasında alt projelere aktarılmasını istemediğimiz bağımlılıkları şu şekilde belirtebiliriz (bunlar `<dependencyManagement>` altında olmalıdır:
  
  ```xml
  <exclusions>
      <exclusion>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context<artifactId>
      </exclusion>
  <exclusions>
  ```

- ..
