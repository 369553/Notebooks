# HIBERNATE

## GENEL BİLGİLER

- Hibernate bir ORM çözümüdür. ORM (Object Relation Map), veritabanındaki tablo satırlarıyla uygulamadaki nesneleri birbirleriyle eşleştiren ve yazılım içerisinde nesnelerdeki değişimleri veritabanına kolayca yansıtabilen, veritabanı sorgusu sonucu gelen satırları uygulamada nesneye otomatik olarak dönüştürebilen ve bu minvalde kolaylıklar sağlayan bir çerçeve türüdür.

- Açık kaynak kodludur.

- Hafiftir.

- LGPL lisansıyla kullanılabilir.

- 4 katmandan oluşur: birincisi, Java uygulama katmanı; ikincisi hibernate kütüphâne katmanı; üçüncüsü arkaplan fonksiyon katmanı ve sonuncusu veritabanı katmanıdır.

- Performansı yüksektir; zîrâ 2 tür önbellekleme özelliği vardır. Birinci seviye önbellekleme varsayılandır.

- Hibernate, 'JPA' (Jakarta / Java Persistence API) standardını uygulayan bir ORM çözümüdür. JPA, farklı ORM teknolojilerinde farklı şekilde yapılan fonksiyon isimlendirmeleri gibi durumların üstesinden gelmek için yapılan bir standarttır. Bu standart sayesinde bir ORM teknolojisinden diğerine geçtiğinizde ORM kullandığınız kodları, çağırdığınız fonksiyon isimlerini değiştirmeniz gerekmiyor.

- Hibernate en çok kullanılan Java ORM çözümlerinden birisidir. İşin açıkçası, bâzı detayları beni boğmaktadır ve fazla gereksiz bir soyutlama olduğunu düşünmekteyim. Veritabanı bağlantısının yapılması, sorgu çekilmesi, nesne ilişkilendirme, otomatik tablo üretme gibi kolaylıkları barındırması hoş; fakat SQL'e benzeyen, fakat SQL olmayan bir HQL (Hibernate Query Language) dilini kullanıyor olması, veritabanı sorgularındaki şartları nesneler olarak sorguya ekleme kullanıcıyı SQL'den tamâmen soyutlamaya çalışan taraflarını hoş bulmuyorum.

- Otomatik tablo üretimi özelliği vardır.

- Sorgu istatistiği ve veritabanı durumu hakkında bilgi sağlar.

## TEMEL YAPITAŞLARI

- **SessionFactory** : Oturum fabrikasıdır. İkinci seviye (ihtiyârî, tercihî olarak ikinci seviye önbellekleme özelliği vardır)

- **Session** : Oturum nesnesi veritabanına sorgu göndermek için kullanılan sargı objesidir.

- **Transaction** : Birden fazla işlemin başarılı şekilde yapıldığının doğrulanması ve işlemlerden biri başarısız olduğunda veritabanının diğer işlemleri de hiç olmamış gibi geriye sarmasının doğrulanması gibi özellikler için kullanılan veritabanı ‘Transaction’ nesnesini oluşturarak işlemin yapılması için desteklenen yapıdır.

- **TransactionFactory** : ‘Transaction’ oluşturmak için kullanılan fabrika desenidir.

## İLK ADIM : YAPILANDIRMA ('Configuration') OLUŞTURMAK

- Veritabanına bağlanmak için öncelikle veritabanı bağlantı bilgileri gibi verileri barındıran bir 'Configuration' nesnesine ihtiyacımız var. Daha sonra bu yapılandırma nesnesinden oturum fabrikası ('SessionFactory') nesnesi üretmeliyiz. Oturum fabrikasından da oturum ('Session') nesnesi üretmeliyiz.

- Bir yapılandırma ('Configuration') nesnesi üretmek için çeşitli yöntemler vardır:
  
  1. **XML yapılandırma dosyasını kullanmak** : Veritabanına bağlanmak için ve Hibernate'i çalıştırmak için  gerekli yapılandırmaları belirttiğimiz dosyanın isminin 'hibernate.cfg.xml' olduğunu düşünelim. Bu dosyayı kullanarak yapılandırma nesnesi üretilebilir:
     
     ```java
     Configuration confs = new Configuration();
     confs.configure("hibernate.cfg.xml");
     ServiceRegistry servReg = new StandardServiceRegistryBuilder().
             applySettings(confs.getProperties()).build();
     SessionFactory sessFactory = confs.buildSessionFactory(servReg);
      // Bir başka yöntem:
      SessionFactory factory = new Configuration().
                              configure("hibernate.cfg.xml").
                              addAnnotatedClass(herhangiSinif.class).
                              buildSessionFactory();
     ```

```xml
<!--Emsal bir yapılandırma dosyası şöyledir:-->
 <?xml version="1.0" encoding="UTF-8"?>
 <!DOCTYPE hibernate-configuration PUBLIC
         "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
         "http://hibernate.org/dtd/hibernate-configuration-3.0.dtd">
 <hibernate-configuration>
     <session-factory>
         <property name="hibernate.connection.driver_class">
             com.mysql.jdbc.Driver
         </property>
         <property name="hibernate.connection.url">
             jdbc:mysql://localhost:3306/veritabani_ismi
         </property>
         <property name="hibernate.connection.username">
             root
         </property>
         <property name="hibernate.connection.password">
             veritabani_kullanici_sifresi
         </property>
         <property name="hibernate.connection.pool_size">
             1
         </property>
         <property name="hibernate.current_session_context_class">
             thread
         </property>
         <property name="hibernate.show_sql">
             true
         </property>
         <property name="hibernate.dialect">
             org.hibernate.dialect.MySQLDialect
         </property>
     </session-factory>
 </hibernate-configuration>
```

2. Veritabanı yapılandırması Java sınıfıyla da yapılabilir:
   
   ```java
   Configuration confs = new Configuration();
   Properties props = new Properties();
   props.put("hibernate.connection.driver_class", "");
   props.put("hibernate.connection.url", "");
   props.put("hibernate.connection.username", "");
   props.put("hibernate.connection.password", "");
   props.put("hibernate.connection.pool_size", "");
   props.put("hibernate.current_session_context_class", "");
   props.put("hibernate.show_sql", "");
   props.put("hibernate.dialect", "");
   confs.setProperties(props);// Yapılandırmaları ata
   // ServiceRegistry nesnesini oluştur:
   ServiceRegistry servReg = new StandardServiceRegistryBuilder().
           applySettings(confs.getProperties()).build();
   // SessionFactory nesnesini oluştur:
   SessionFactory sessFactory = confs.buildSessionFactory(servReg);
   ```
   
   ..

## BAŞLAMADAN EVVEL

- Hibernate'in bilhassa bağlantı ayarlarını içeren yapılandırma nesnesini oluşturmak için gereken kodu yazdıktan sonra uygulamadaki nesnelerle veritabanı tablolarını eşleştirmek için yapmamız gereken haritalama yapılandırmasını oluşturmaktır.

- Buna 'hibernate-mapping' denmektedir. Bu işlem aynı bağlantı yapılandırmasının oluşturulmasında olduğu gibi XML ile veyâ bildirim ('notasyon')ler ile yapılabilir.

- XML haritalama dosyası oluşturmak daha zahmetlidir. Hibernate'i kullanmanın en iyi yolu bildirimleri kullanmaktır. Ayrıca bildirimlerin kullanılması Spring Boot ile berâber kullanımında kolaylıklar sağlayabilir.

- XML ile haritalamayı öğrenmek için üç sonraki bölüme, bildirimlerle haritalamayı öğrenmek için bir sonraki bölüme bakınız.

- Ayrıca bir sınıfı Hibernate ile bağlamak için sınıfın taşıması gereken özelliklere iki sonraki bölümden bakınız.

#### TEMEL BİLDİRİMLER (NOTASYONLAR)

1. `@Entity` :  Sınıfın tepesine eklenen bu bildirim, ilgili sınıfın bir veritabanı nesnesi olduğuna işâret eder.

2. `@Table` : Sınıfın tepesine eklenen bu bildirim, sınıfın veritabanındaki eşleştiği tabloyla ilgili bilgiler verir. 'name' parametresi sınıfın karşılığındaki veritabanı tablosunun ismini belirtmek için kullanılır.

3. `@Id` : Bir sınıf alanının ('field') tepesine eklenebilen bu bildirim bu alanın veritabanındaki birincil anahtarı ifâde ettiğini ifâde eder. Eğer veritabanındaki tablonuzda birincil anahtar varsa, mutlaka kod içerisinde onu simgeleyen bir özellik de olmalıdır ve bu özelliğin tepesine bu bildirim eklenmelidir. Varsayılan olarak, her sınıf için böyle bir `@Id` bildirimi olmalıdır; hatâ alınır : Veritabanında ilgili satır birincil anahtar olmasa da, @Id bildirimi eklenebilir. Eğer `@Id` bildirimiyle belirtilen bir alan için iki aynı değere sâhip satır varsa, uygulama hatâ vermez!

4. `@Column` : Sınıf alanlarının veyâ bu alanların erişim yöntemi olan 'getter' yöntemlerinin tepesine eklenebilen bu bildirim, ilgili alanın veritabanındaki ilgili tabloda hangi sütunla eşleşeceğini ifâde etmek için kullanılır.  Sütun ismini 'name' parametresiyle belirtmeliyiz. Eğer veritabanındaki sütunlarla, sınıfın alanlarının (özelliklerinin) isimleri aynı ise bunu yazmamıza gerek yoktur.
   
   Alabileceği diğer parametreler:
   
   - `nullable` : boolean tipinde bir değer alır.
   
   - `unique` : boolean tipinde bir değer alır.

5. `@Transactional` : Yöntem ('method')lerin tepesine eklenebilen bu bildirim veritabanında işlem yaparken hatâlı işlemin önüne geçmeyi, inkâr edilemezlik ve doğrulama veri güvenliği kâidelerini gerçekleştirmeyi sağlayan 'bütüncül işlem' ('transaction') yapısını kolayca uygulamak için kullanılır. Bu bildirimi eklediğimiz işlemin başında bir 'transaction' açılır; eğer yöntem başarıyla sonuçlanırsa bu 'transaction' işlem sonunda veritabanına işlenir ('commit' edilir); eğer yöntem başarıyla sonuçlanmazsa yapılan tüm işlemler güvenli şekilde, hiç yapılmamış gibi geri sarılır ('rollback' edilir). <mark>**!!**</mark> : ÖNEMLİ : Eğer oturum nesnesi `SessionFactory` nesnesinin `getCurrentSession()` yöntemiyle alındıysa, bu bildirim varsayılan olarak işe yaramıyor. Diğer yöntemlerde (`openSession()` ve `createEntityManager().unwrap(Session.class)`) de kaydetme işlemleri için varsayılan olarak işe yaramıyor.

6. `@Access` : Sınıfın tepesine eklenebilen bu bildirim Hibernate çerçevesinin (framework) özelliklere nasıl erişeceğini belirten bir bildirimdir. Verilmesi zorunlu 'value' parametresi vardır. Bu parametreye iki değer verebilirsiniz, ki bu değerler çerçevenin özelliklere erişim tipini simgeleyen birer 'enum' değerlerdir:
   
   1. `AccessType.FIELD` : Eğer Hibernate'in sınıftaki alanları hangi sütunlarla eşleştireceğini çözmek için alanlara ve üzerindeki bildirimlere bakmasını istiyorsak bu 'enum' değerini kullanmalıyız.
   
   2. `AccessType.PROPERTY` : Eğer `@Column` bildirimini sınıftaki alanların 'getter' yönteminin üstüne eklediysek bu 'enum' değerini kullanmalıyız.

7. `@PostLoad` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Bu sınıfın örnekleri veritabanından çekildikten sonra bu bildirimin eklendiği yöntem çalıştırılır.

8. `@PrePersist` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanına kaydetme öncesinde bu bildirimin eklendiği yöntem çalıştırılır.

9. `@PostPersist` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanına kaydetme sonrasında bu bildirimin eklendiği yöntem çalıştırılır.

10. `@PreRemove` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanından silme işlemi öncesinde bu bildirimin eklendiği yöntem çalıştırılır.

11. `@PostRemove` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanından silme işlemi sonrasında bu bildirimin eklendiği yöntem çalıştırılır.

12. `@PreUpdate` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanındaki güncelleme işlemi öncesinde bu bildirimin eklendiği yöntem çalıştırılır.

13. `@PostUpdate` : `@Entity` bildirimini taşıyan sınıf içerisindeki bir yöntemin tepesine eklenebilir. Veritabanındaki güncelleme işlemi sonrasında bu bildirimin eklendiği yöntem çalıştırılır.

14. `@EntityListeners` : Yaşam döngüsü yöntemleri denilen yukarıdaki yöntemleri sınıf içerisine eklenmeyip, başka bir sınıfta tanımlandığı durumlarda kullanılır. Bu durumda bu bildirimin 'value' özelliğine liste olarak ilgili sınıf verilmelidir. **Önemli olan husus şudur ki, ilgili sınıftaki yöntemler bu sınıf örneğini parametre olarak almalıdır**:
    
    ```java
    @Entity
    @Table(name="city")
    @EntityListeners(value = {CityListeners.class})
    public class City{/*.;.*/}
    ```

15. `@` : ..

> ***NOT*** : Yaşam döngüsü yöntemleri olarak isimlendirilen yöntemler (`@PreUpdate` , `@PostUpdate` , `@PostLoad` gibi) her eleman için çalıştırılır. Misal, tablodan dört satır çekerek uygulamaya dört nesne aktardıysanız, `@PostLoad` yöntemi dört kez çalışır; tabi her bir nesne için çalışır.
> 
> ***NOT - 2*** : Yaşam döngüsü yöntemleri için eklenen dinleyiciler başka bir sınıfta tanımlanıyorsa o sınıfta tanımlandıklarında parametre olarak ilgili nesneyi almalıdırlar ve 'void' tipinde olmalıdırlar.:
> 
> ```java
> public class CityListeners{
>     @PostLoad
>     public void afterFetching(City city){// Başka parametre alamaz
>         System.out.println("'City' kayıtları başarıyla çekildi");
>     }
> }
> ```

## ‘PERSISTENT’ (KALICI) SINIF

- Hibernate'in bir sınıfı veritabanı ile eşleştirmesi için sınıfın taşıması gereken bâzı kurallar vardır:
  
  1. Sınııfın parametresiz yapıcı fonksiyonu olmalı.
  
  2. Nesneyi diğerlerinden ayıran münferid bir değer barındıran bir özellik taşıması, misal ‘id’ özelliği olabilir.
  
  3. Erişim yöntemleri (‘getter’ ve ‘setter’) içermeli.
  
  4. ‘final’ olmayan sınıf tercih edilmeli(?)

## KALICI SINIF İÇİN HARİTALAMA DOSYASI OLUŞTURMA

- Bu dosyanın ismi yaygın kullanıma göre  ‘className.hbm.xml’ olabilir.

- Bu dosya birçok haritalama bileşeni içerir:
  
  1. `<hibernate-mapping>` : İçerisinde tüm haritalanmış bileşenleri barındıran kapsayıcı bileşendir
  
  2. `<class>` : Kalıcı sınıfı simgeler
  
  3. `<id>` : Sınıfın alt bileşenidir. Sınıf örneklerinin birbirinden ayırt edilmesini sağlayan ve tabloda birincil anahtara karşılık gelen özellik bu etiketle belirtilir. Hangi özelliğin tablodaki birincil anahtar olmasını istiyorsak o özelliğin ismini nu etikete ‘name’ özelliğiyle vermeliyiz.
     
     ```xml
     <id name="identityNumber">
         <!-- ...-->
     </id>
     ```
  
  4. `<generator>` : ‘id’ nin alt bileşenidir. Tabloda birincil anahtarı üretmek için kullanılır
  
  5. `<property>` : Sınıfın özelliğini ifâde eder; sınıfın alt bileşenidir.
     
     Emsal bir haritalama dosyası:
     
     ```xml
     <?xml version=1.0 encoding="UTF-8"?>
     ...(hibernate ilgili kod)
     <hibernate-mapping>
         <class name="schoolAutomation.Student"
         table="StudentTableNameOnDatabase">
             <id name="schoolNumber">
                 <generator class="assigned"></generator>
             </id>
             <property name="name"></property>
             <property name="surname"></property>
         </class>
     </hibernate-mapping>
     ```

- Haritalamadaki en önemli detaylardan birisi `<id>` etiketidir. Bu etiketle sınıfın birincil anahtarı belirtilirken, bu etiket içerisindeki `<generator>` etiketi ile bu birincil anahtarın üretilmesiyle alâkalı bir yapılandırma ayarı belirtilir. `<id>` etiketiyle belirtilen bir özellik `<property>` etiketiyle yeniden belirtilmez.

## SORGU DİLİ : HQL (Hibernate Query Language)

- SQL'in nesne yönelimli hâli gibidir.

- Sorgu cümlesi nesnesi oluşturmak için oturum (‘Session’) arayüzünün `createQuery()` yöntemi kullanılır.

- Oturum nesnesini elde etmek için oturum fabrikasının `getCurrentSession()` yöntemini veyâ `openSession()` yöntemini veyâ  `createEntityManager().unwrap(Session.class)` yöntemini kullanabiliriz. `getCurrentSession()` yöntemini kullandığımızda `@Transactional` bildirimi hiç çalışmıyor; diğerlerinde de commit edilmiyor (değişiklik yaptığımızda veritabanına kaydedilmiyor). Transaction işlemini kendimiz başlatıp, sonlandırdığımızda sorun olmuyor.

- **<mark>! DİKKAT</mark>** : Sorgu yapmadan evvel oturumun durumunu aktif hâle getirmek için oturumun `beginTransaction()` yöntemini çağırmalıyız!

- Sınıflar tablolarla eşleştiğinden, tablo sütunlarının tümünü çektiğimizde, ilgili sınıf örneğini oluşturmak için gereken verileri elde etmiş oluyoruz. Verileri doğrudan nesneye atanmış olarak almak istediğimizde `createQuery()` yöntemine ikinci parametre olarak ilgili sınıfı vermeliyiz:
  
  ```java
  String sql = "from City";// 'from sinif_ismi'
  Transaction act = session.beginTransaction();
  List<City> cities = session.createQuery(sql, City.class).
                      getResultList();
  act.commit();
  ```

- HQL'in SQL'den farklı yanlarının bir kısmı şöyledir:
  
  1. `SELECT` deyimini kullanmıyorsunuz.
  
  2. Veriyi çekeceğiniz tablonun ismini değil; tablonun uygulamada eşleştiği sınıfın ismini yazıyorsunuz.

- Eğer saf SQL yazılmak isteniyorsa oturumun `createNativeQuery(String sql)` yöntemi kullanılır.

- Sorgu sonucunda dönen veri setinde tekrar eden değerlerin bir kez olması isteniyorsa sorgu sonucu dönen veri setinin `uniqueResult()` yöntemi kullanılır.

- Sorgu nesnesinin birçok yöntemi vardır. Bâzıları:
  
  1. `int executeUpdate()` : JDBC'de `executeUpdate` yöntemi olduğunu dikkate alırsak, onu çalıştırdığını tahmîn edebiliriz. Veri güncellemeyle ilgili deyim yazdıysak, bunu çalıştırmak için kullanırız.
  
  2. `List list()` : Veriyi liste olarak getirir
  
  3. `Query setFirstResult(int rowNo)` : Tablodaki verilerin herhangi satırdan başlayarak döndürülmesini istiyorsak, burada bu belirtilebilir.
  
  4. `Query setMaxResult(int rowNo)` : Eğer tablo verilerinin sadece belli bir satır aralığını istiyorsak, bu aralığın üst sınırını belirtmek için bu yöntemi kullanabiliriz.
  
  5. `Query setParameter(int position, Object value)` : Sorgu cümlesindeki yerine konmamış parametreyi sorgu cümlesindeki sıra numarasını belirterek yerine koymak için kullanılır. Sorgu cümlesine isimlendirilmiş parametre şu şekilde konur:
     
     `SELECT * FROM Student WHERE name:=name;`
     
     Buradaki "=:" işleci isimlendirilmiş parametre koymak içindir; bu işleçten sonra yazılan kelime değeri belirtilmemiş parametrenin ismidir. Bu isim `setParameter(String name, Object value)` yöntemini kullanmak için gereklidir.
  
  6. `Query setParameter(String name, Object value)` : Sorgu cümlesindeki yerine konmamış parametreyi sorgu cümlesindeki isim belirterek yerine koymak için kullanılır.

- ..

#### HCQL (Hibernate Conditional Query Language)

- Sorguyu belli bir şarta göre çekmek için kullanılıyor.

- Aslında saf SQL sorgusundaki "WHERE" şartıyla belirtilebilen şeyleri ayrı nesneler üzerinden oluşturma temeline dayanıyor.

- Şartları `Criteria` arayüzü simgeliyor.

- Şart ifâde eden `Criteria` arayüzünü sağlayan bir örnek oluşturmak için oturumun (`Session`) `createCriteria(Class entityClass)` yöntemi kullanılıyordu; bu yöntemin girdi parametresi verilerin çekileceği tablonun uygulamadaki karşılığı olan sınıftır. Hibernate 5 sürümünün bir güncellemesinde bu yöntem kaldırıldı. Bunun yerine oturumun `getCriteriaBuilder()` yöntemi kullanılıyor. Dolayısıyla aşağıdaki yöntemler yerine dört sonraki konudaki yöntemlere bakınız. 

- Criteria sınıfının sık kullanılan bâzı yöntemleri şöyle:
  
  1. `public Criteria addCriteria(Criterion c)` : Kısıt eklemek için kullanılır
  
  2. `public Criteria addOrder(Order o)` : Sıralama belirtmek için kullanılır
  
  3. `public Criteria setFirstResult(int firstResult)` : İlk kaç satırın çekileceğini belirtmek için kullanılır
  
  4. `public Criteria setMaxResult(int totalResult)` : En fazla kaç satır çekileceğini belirtmek için kullanılır.
  
  5. `public List list()` : Şartları ekledikten sonra sonucu çekmek için kullanılır.
  
  6. `public Criteria setProjection(Projection projection)` : 

- ..

#### "RESTRICTIONS" SINIFI

- Kısıt eklemek için bu sınıf kullanılır.

- Fonksiyonları statiktir; oturum üzerinden oluşturulan "Criteria" nesnesinin "add()" yöntemi içerisinde kullanılabilir.

- Basit şekilde bir alandaki değer için büyüktür, küçüktür, büyük eşittir, küçük eşittir, eşit değildir, arasındadır (SQL'deki "BETWEEN" işleci) ve şuna benzerdir (SQL'deki "LIKE" işleci) kısıtlarını eklemek için kullanılır.

- "Restrictions" sınıfının statik fonksiyonları:
  
  1. `public static SimpleExpression lt (String propertyName, Object value)` : Verilen özelliğin, verilen değerden küçük olduğu şartını belirtmek için kullanılır.
  
  2. `public static SimpleExpression le (String propertyName, Object value)` : Verilen özelliğin verilen değerden küçük eşit olduğu şartını belirtmek için kullanılır.
  
  3. `public static SimpleExpression gt (String propertyName, Object value)` : Verilen özelliğin verilen değerden büyük olduğu şartını belirtmek için kullanılır.
  
  4. `public static SimpleExpression ge (String propertyName, Object value)` : Verilen özelliğin verilen değerden büyük eşit olduğu şartını belirtmek için kullanılır.
  
  5. `public static SimpleExpression ne (String propertyName, Object value)` : Verilen özelliğin verilen değere eşit olmadığı şartını belirtmek için kullanıır.
  
  6. `public static SimpleExpression eq (String propertyName, Object value)` : Verilen özelliğin verilen değere eşit olduğu şartını belirtmek için kullanıır.
  
  7. `public static SimpleExpression between (String propertyName, Object min, Object max)` : Verilen özelliğin verilen iki değer arasında olduğu şartını belirtmek için kullanılır. Bu, SQL'deki 'BETWEEN' işleci olarak düşünülebilir.
  
  8. `public static SimpleExpression like (String propertyName, Object value)` : SQL'deki 'LIKE' işlecini ifâde eder. Verilen özelliğin verilen değere benzediği şartını belirtmek için kullanılır. Buradaki bu benzerlik, SQL'deki joker karakter denilen ön tanımlı karakterlerden oluşan bir değerdir. Bilindiği üzere SQL'de `'%ak'` ifâdesi 'ak' ile başlayanları ifâde etmektedir, LIKE işleci bu tür (`%`) ön tanımlı karakterlerle kullanılır.

- ..

## ORDER nesnesi

- `Restrictions` sınıfıyla kısıtların belirlenmesi için; bu sınıf ise sıralamanın belirlenmesi içindir.

- Fonksiyonları statiktir.

- "Criteria" nesnesinin `addOrder()` yöntemi sorguya sıralama şartı eklemek içindir.

- Statik fonksiyonları:
  
  1. `public static Order asc(String propertyName)` : Artan sırada sıralama yapmayı belirten Order nesnesi döndürür. Hangi sütuna göre sıralama yapılması isteniyorsa parametre olarak verilir
  
  2. `public static Order desc(String propertyName)` : Azalan sırada sıralama yapmayı belirten `Order` nesnesi döndürür. Hangi sütuna göre sıralama yapılması isteniyorsa parametre olarak verilir

- ..

## "Projection" NESNESİ

- Sorgudan çekilecek sütunları sınırlandırmak için kullanılır.

- Statik `property()` fonksiyonuna sütun ismi verilerek, sorgudan yalnızca o sütunun çekilmesinin istendiği belirtilir.

- Bunu kullanmak için ise "Criteria" nesnesinin `setProject()` yöntemi kullanılır:

- Misal, aşağıdaki sorgu sadece "schoolNumber" sütunu verisini çeker:
  
  ```java
  crtr.setProject(Projections.property("schoolNumber"));
  crtr.list();
  ```

- ..

#### HCQL (Hibernate Conditional Query Language) YENİ YÖNTEM

- Yeni yöntemde öncelikle oturumun `getCriteriaBuilder()` yöntemini kullanarak bir 'CriteriaBuilder' nesnesi oluşturuluyor.

- Ardından bu 'CriteriaBuilder' nesnesinin '`createQuery(Class<T>)`' yöntemi kullanılıyor; buna parametre olarak kısıtın ekleneceği sorgudaki veri çekilen tablonun eşleştiği sınıf verilir. Bu yöntem geriye `CriteriaQuery<T>` tipinde HCQL sorgu nesnesi döndürür:
  
  ```java
  SessionFactory factory = new Configuration().
                          configure("hibernate.cfg.xml").
                          addAnnotatedClass(herhangiSinif.class).
                          buildSessionFactory();
  Session session = factory.getCurrentSession();
  session.beginTransaction();// 'Transaction' başlatılmazsa hatâ verir
  CriteriaBuilder crtrBui = session.getCriteriaBuilder();
  CriteriaQuery<City> crtrQuery = crtrBui.createQuery(City.class);
  // Şartlar CriteriaBuilder ve CriteriaQuery nesneleriyle yapılır..
  ```

- 'WHERE' şartı eklemek için 'CriteriaQuery' nesnesinin `where()` yöntemi çağrılır. Bu yönteme verilen şart 'Predicate' tipinde olmalıdır. Bu şart da 'CriteriaBuilder' nesnesi üzerinden yapılır; fakat 'CriteriaBuilder' nesnesi üzerinden bir şart yazabilmek için öncelikle bir sütunu seçmeliyiz. Bunun için de sorgunun ham hâlindeki yapıyı simgeleyen 'Root' nesnesini kullanmalıyız. Bu nesnenin `get()` yöntemiyle bir sütun seçilebilir; bu yöntem geriye 'Expression' tipinde bir değer döndürür. Bu değer 'CriteriaBuilder' nesnesi üzerinden şart yazarken kullanılır. 'Root' tipindeki nesneyi almak için 'CriteriaQuery' nesnesinin `from(sinif_ismi.class)` yöntemi kullanılır. Yazdığımız şartı uygulamak için 'CriteriaQuery' nesnesinin `select()` yöntemine bu şartı verebiliriz; görüldüğü üzere uğraştırıcı ve çoğu kez işe yaramaz bir şey! Bunun yerine şartı sql cümlesiyle vermek çoğu kez daha iyidir!
  
  ```java
  Root<City> root = crtrBui.from(City.class);
  // Plaka kodu 34'ten büyük olma şartını 'Predicate' olarak getir:
  Predicate condition = crtrBui.ge(root.get("plateCode"), 34);
  // Şartlı sorgu nesnemizin 'where' yöntemine ilgili şartı ver:
  crtrQuery.select(root).where(condition);
  // Şartlı sorguyu oturumun 'createQuery' yöntemi aracılığıyla oluştur:
  List<City> cities = session.createQuery(crtrQuery).getResultList();
  ```

- CriteriaBuilder şart yöntemleri:
  
  1. ..

- ..

#### 'CriteriaUpdate' ve 'CriteriaDelete'

- Bu sınıfların kullanımı da diğer Criteria sınıfının kullanımı gibidir. Emsal kullanım:
  
  ```java
  SessionFactory factory = new Configuration().
                          configure("hibernate.cfg.xml").
                          addAnnotatedClass(herhangiSinif.class).
                          buildSessionFactory();
  Session session = factory.getCurrentSession();
  session.beginTransaction();// 'Transaction' başlatılmazsa hatâ verir
  CriteriaBuilder crtrBui = session.getCriteriaBuilder();
  CriteriaUpdate<City> crtrUpdate = 
              crtrBui.createCriteriaUpdate(City.class);
  Root<City> root = crtrUpdate.from(City.class);
  crtrUpdate.set("name", "İstanbul");
  crtrUpdate.where(crtrBui.equal(root.get("name"), "Istanbul");
  session.createQuery(crtrUpdate).executeUpdate();
  ```

- ..

## İSİMLENDİRİLMİŞ SORGULAR (NAMED QUERY)

- Sık kullanılan sorgular veyâ uzun sorgular isimlendirilerek hatâlı sorgulamanın önüne geçilebilir. Hibernate'de bu yapıya 'named query' (isimlendirilmiş sorgu) denmektedir.

- İki şekilde isimlendirilmiş sorgu tanımlanabilir:
  
  1. Bildirim (notasyon, annotation) ile : Tek isimlendirilmiş sorgu tanımlamak için `@NamedQuery()`, birden fazla isimlendirilmiş sorgu tanımlamak için `@NamedQueries()` bildirimi kullanılır. Eğer sorgu dili HQL değil, SQL ise `@NamedNativeQuery` bildirimi eklenir.
     
     Örnek tanımlamalar : 
     
     ```java
     @NamedNativeQueries(
     {    
         @NamedNativeQuery(
             name="ogrNo çek",
             query="SELECT schoolNumber from Students WHERE name=:"
         )
     })
     ```
  
  2. Haritalama dosyası (mapping file) ile : ...

## JPA META-MODEL

- JPA API'lerinden birisiyle çalışılıyorsa (misal, Criteria API), JPA meta-modelin kullanılması tavsiye ediliyor.

- Bunu kullanabilmek için projemize dâhil etmemiz gereken bir kütüphâne var. Maven kullanıyorsak, şu bağımlılığı 'pom.xml' dosyasına eklemeliyiz:
  
  ```xml
  <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-jpamodelgen</artifactId>
  </dependency>
  ```

- Bu kütüphâne sayesinde yukarıdaki kodlardaki `root.get("plateCode")` yerine `root.get(City_.plateCode)` kodu yazılabilir. Bu, alanların yanlış yazılmasının önüne geçmek, arama yaparken hızlıca istenileni bulmak ve yazım yaparken IDE'nin tamâmlama - tavsiye gibi özelliklerini kullanmak için iyi bir yol olabilir.

## DETAYLAR

#### Saf SQL Sorguları İçin Sorgu Sonucu ile Nesne Özelliğini İlişkilendirme

- `@SqlResultSetMapping` bildirimiyle yazılan bir saf SQL sorgusundan gelen sonuç `Object` yerine ilgili sınıf tipinden alınabilir. Bu, pek çok zorunlu parametresi olan uzun bir bildirim, emsal tanımlama:
  
  ```java
  @SqlResultSetMapping(
      name="CityMapping",// Haritalama ismi, sorgu çekerken lazım.
      entities = @EntityResult(
          entityClass = City.class,
          fields = {
              @FieldResult(name="id", column="id"),
              @FieldResult(name="plateCode", column="plateCode"),
              @FieldResult(name="name", column="name")
          }// name = alan ismi        column = tablo sütun ismi
      )
  )
  public class City{
      public int id;
      public int plateCode;
      public String name;
  }
  ```

- Bu tanımlamadan sonra ilgili haritalama şu şekilde kullanılmalı:
  
  ```java
  
  ```

- ..

## SORGU ÇEKME YÖNTEMİ ('FetchType')

- Hibernate bir alana bir değeri eşleştirmek istediğinde bunun için veritabanına sorgu yollar. Fakat varsayılan olarak, bir nesnenin tüm alanları için tüm alanlar çekilir ve uygulamaya aktarılır.

- Eğer sınıfın bir alanı özel bir sınıf ise ve bu sınıf veritabanındaki başka bir tabloyla eşleşiyorsa Hibernate bu durumda gereken diğer sorgulamaları da yapar. Bu durum, sınıfın yüklenmesi işleminin yavaş olmasına sebebiyyet verebilir.

- Yukarıda anlatılan bu veri çekme biçimi 'EAGER' (hevesli) veri çekme işlemidir ve varsayılan olarak bu böyledir.

- Diğer bir veri çekme biçimi ise 'LAZY' (tembel) veri çekme biçimidir. Bu veri çekme biçiminde, Hibernate, siz o alanı kullanana kadar ilgili alana veritabanındaki değeri zerk etmez.

- Eğer bir sınıftan bir nesne üretilirken, o sınıfın başka tabloyla eşleşen alanına hemen ihtiyaç duymuyorsak, bu durumda 'LAZY' (tembel) veri çekme biçimi kullanılabilir.

- Emsal kullanım:
  
  ```java
  ..
  ```

- ..

## TAVSİYELER

- Sorguları isimlendirilmiş sorgu olarak yazın

- jpa.modelgen kullanılması tavsiye ediliyor

- Alan bazlı bildirimi seçin; böyle yaptığınızda, Hibernate ilgili alana değeri zerk etmek için temel Java kütüphânesi olan `java.lang.reflect` kütüphânesini kullanır.

- İsimlendirilmiş sorguların isimlerini sınıf içerisinde `static final` olarak tanımlayın; hatâdan kaçınmak için bu, iyi bir yöntemdir.

- Sorguları çekerken Tuple biçiminde çekilmesinin daha iyi olacağı belirtiliyor; Tuple biçiminde çektiğiniz sorgu sonuca, hem indis numarasıyla, hem de alan ismiyle erişebiliyormuşsunuz.

- Parametreleri sorgu içerisine yerleştirirken ('parameter binding') bunu isimlendirilmiş parametre kullanarak yapın; bu, parametre sırasını yazarken hatâ yapmanıza engel olması açısından ve okunabilirlik açısından daha isâbetlidir.

- Veritabanında yapılması daha verimli olan işleri veritabanına yaptırın. Misal, bir sorgu sonucu gelen verinin adedini hesaplamak yerine bunu veritabanı 'aggregate' fonksiyonlarıyla yapabilirsiniz. Bu, yapılan işleme göre performansı ciddî derecede etkiler.

## HIBERNATE ile VERİTABANINA EKLEME - GÜNCELLEME - SİLME

- `CriteriaUpdate` ve `CriteriaDelete` sınıflarıyla güncelleme ve silme yapılabilir; fakat nesnede yapılan değişiklikleri veritabanına aktarmak çok daha kolaydır. Bunun için oturumun `save()` yöntemine ilgili nesne vermek kâfîdir.
