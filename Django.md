# DJANGO

## GENEL BİLGİLER

- Django Python'da web geliştirmek için kullanılan bir üst seviyeli kütüphânedir (framework).

- Django web geliştirme işlerini kolaylaştıran bir kütüphânedir.

- Django ile yönetici paneli otomatik olarak oluşturulur; Java ile 'arka uç' ('back end') geliştirme yaparken birçok kolaylık için Spring Boot kullanıyoruz; bağımlılıklar ekliyoruz. Django'da bunların çoğu kullanıcıdan soyutlaştırılıyor; işler daha kolay hâle geliyor.

- Django projesi uygulamalardan oluşur; bu, proje büyüdüğünde idâre edilebilirliğinin zorlaşmaması açısından iyi bir özelliktir.

- Varsayılan olarak Sqlite - 3 veritabanını kullanır; lâkin bu değiştirilebilir(?)

- Proje ayarları 'settings.py' içerisinde yer alıyor.

- Django kullanıcı belgelerine ulaşmak için ziyâret edin:
  <a>https://docs.djangoproject.com/en/4.2/</a>

- Yeni versiyon çıktığında yukarıdaki bağlantı adresindeki 4.2 yazan yere yeni versiyonu yazabilir veyâ siteyi ziyâret ederek elle versiyon numarası belirtebilirsiniz.

## İLK ADIMLAR

## Django'nun Yüklenmesi

- Django kütüphânesi 'pip' ile kurulabilir. Bunun için komut satırında şu kodu çalıştırmamız gerekiyor:
  `py -m pip install django==5.1.4`

- Python'ın yeni sürümleriyle berâber (3.12 gibi) Python'u çalıştırmak için Windows işletim sisteminde komut satırında `python` yerine `py` yazıyoruz; Linux tabanlı işletim sistemlerinde ise `python3` yerine `python` yazılması söz konusu.

- Django kurulumu yaparken Django'nun uyumlu olduğu Python sürümünün bilgisayarınızda yüklü olmasına dikkat ediniz.

#### Django Projesi Oluşturma

- Komut satırında  şu komut çalıştırılır : `django-admin startproject projeIsmi`

- Proje ismi kısa çizgi ('-') içeremez; ..

#### Django Projesini Çalıştırma

- Django projesini çalıştırmak için şu komutlardan birisi çalıştırılır:
  `django-admin runserver`
  `py manage.py runserver`

- ***NOT :*** Proje oluşturulduktan sonra proje dizini içerisindeki 'manage.py' dosyası bizim için 'django-admin' yerine geçtiğinden 'django-admin' yerine 'python manage.py' yazarak 'django-admin' komutlarını çalıştırabiliriz.

#### Proje Anasayfasını Açma

- Django projesi varsayılan olarak 8000 numaralı port üzerinden yayına alınır.

- Proje çalıştırma kodu yazıldıktan sonra verilen url adresi bir web tarayıcısına yazıldığında proje ana sayfası açılmış olur.

#### Yayını Durdurma

- Projenin çalışmasını sonlandırmak için projenin çalıştırıldığı komut istemcisinde 'CTRL+C' tuş kombinasyonuna basılabilir.

#### Uygulama Ekleme

- Django projesi uygulamalardan oluştuğu için proje içerisine çeşitli uygulamalar eklememiz gerekiyor.

- Django uygulamamıza bir alt uygulama eklemek için şu kodu çalıştırmalıyız:
  `python manage.py startapp uygulamaIsmi`

- Oluşturduğumuz bu uygulamayı projeye tanıtmamız gerekiyor.

- Bunun için yukarıdaki kod çalıştırıldıktan sonra proje dizini içerisindeki proje ismiyle aynı isimde olan dizin (proje ana uygulamasının dizini) içerisindeki 'settings.py' dosyası açılır; dosya içerisindeki `INSTALLED_APPS` listesine uygulama ismi tırnak içerisinde ('str' olarak) eklenir.

#### Django Versiyonunu Sorgulama

- Bunun için `py -m django --version` kodunu komut satırında çalıştırın.

## UYGULAMA MİMARİSİ HAKKINDA

- ..

## TALEPLERİ ELE ALALIM

#### Talep Yönlendirme Noktası (TYN) nı Tanıyalım

- Bir web projesinde en önemli şey gelen talepleri ele almaktır.

- Django'da gelen talepleri ele almak için kolay, kullanışlı ve çok yönlü bir yapı vardır.

- Projenin ana uygulama dizininin içerisindeki 'urls.py' dosyası içerisinde bulunan 'urlpatterns' listesi projenin ana uygulamasına gelen taleplerin nasıl yönlendirileceğini belirtiyor. Buna 'talep yönlendirme noktası' diyelim. Örnek TYN:
  
  ```python
  from django.urls import path
  from django.http import HttpResponse
  
  def home():
      return HttpResponse("<h3>Anasayfa</h3>")
  def contact():
      return HttpResponse("<h3>İletişim sayfası</h3>")
  urlpatterns = [
      path('', home),#127.0.0.1:8000/
      path('contact/', contact)#127.0.0.1:8000/contact/
  ]
  ```

- Yukarıdaki kodda gelen taleplerin hangi fonksiyonla eşleştiğini belirten yapı 'urlpatterns' listesidir. Bu listenin elemanları 'path' fonksiyonundan oluşuyor; bu fonksiyon birinci parametre olarak eşleştirilmek istenen url bilgisini, ikinci parametre olarak ise bu bağlantı adresine yapılan isteğe karşılık döndürülecek cevâp bilgisini barındırır.

- Listede ilk parametre uygulama kök dizinini, yanî anasayfayı temsil etmektedir. İkinci parametre ise, anasayfadan sonra eklenen 'contact/' bağlantı adres metninini içeren bağlantı istekleriyle eşleşir. Uygulama ana dizinine gelindiğinde döndürülmek istenen cevâp (Response) 'home' fonksiyonunda tanımlanmıştır.

> ***NOT :*** Django talepleri ele alırken 'urlpatterns' listesi içerisinde sırasıyla uygun olan 'path'e göre ele alır. Dolayısıyla bir url bilgisi birden fazla yönlendirme değeriyle ('path') eşleşiyorsa, bu durumda yönlendirme üstteki 'path' değerine göre yapılır.

#### Cevâpları ('Response') Farklı Fonksiyona Taşıyalım

- 'urls.py' dosyasını sade tutmak ve uygulama düzenleme işlemlerini daha uzmanca bir usûlle ele almak için geri döndürdüğümüz cevâpları 'views.py' içerisine almalı ve ilgili dosyayı `from . import views` diyerek eklemeliyiz:
  
  ```python
  from django.urls import path
  from django.http import HttpResponse
  from . import views
  
  urlpatterns = [
      path('', views.home),#127.0.0.1:8000/
      path('contact/', views.contact)#127.0.0.1:8000/contact/
  ]
  """
  Bu durumda views dosyası şu şekilde olmalı:
  from django.http import HttpResponse
  def home(request):
      return HttpResponse("<h3>Anasayfa</h3>")
  def contact():
      return HttpResponse("<h3>İletişim sayfası</h3>")
  """
  ```

#### Alt Uygulamaya Gelen İstekleri Bırakın Alt Uygulama Ele Alsın

- Gelen bağlantı adresinin işlenmesi işlemini bâzen alt uygulamaya devretmek isteyebiliriz. Misal, bize gelen talebin url adresi '/odeme' şeklinde ise gelen talebi 'odeme' isminde bir uygulamaya yönlendirebiliriz; benzer şekilde gelen talep '/account' şeklinde ise bu talepleri account (veyâ istediğimiz isimde oluşturduğumuz) uygulamasına yönlendirebiliriz. Bunun için yapmamız gereken şey:
  
  1. İlgili alt uygulamayı oluşturmak
  
  2. 'django.urls' sınıfı altındaki 'path' fonksiyonunu kullanarak ana TYN'ye gelen ilgili isteği alt uygulamaya devretmek:

- Emsal kullanım:
  
  ```python
  from django.urls import path, include
  from django.http import HttpResponse
  from . import views
  
  urlpatterns = [
      path('', views.home),#127.0.0.1:8000/
      path('store/', include('store.urls'),#127.0.0.1:8000/store
      path('contact/', views.contact)#127.0.0.1:8000/contact/
  ]
  ```

- Yukarıdaki örnekte uygulamaya '/store' bağlantı adresiyle gelen istekler 'store' ismindeki alt uygulamanın 'urls.py' dosyasına sevk ediliyor. `include` fonksiyonunun ilgili parametreyi metîn tipinde aldığına dikkat ediniz.

#### Bağlantı Adreslerini Dinamik Olarak Ele Alma

- Bir kütüphâne uygulaması yazmamız gerektiğini düşünelim. Her kitâp için bir bağlantı adresi olmalı; peki, biz gerçekten her kitâp için ayrı bir bağlantı adresini 'urlpatterns' listesi içerisine ekleyecek miyiz? Yeni bir kitâp eklememiz gerektiğinde ilgili bağlantı adresini liste içerisine eklemek zorunda mıyız? Bu uygulanabilir değil!!

- Bu sorunun çözümü bağlantı adresindeki belli parçaları değişken olarak ele almaktır. Burada gelen url içerisindeki belirlediğimiz noktalardaki metînleri bir değişken olarak alabiliriz. Bunun için değişkenin url içerisindeki yerine küçük büyük işâreti koyup, arasına değişken ismini yazmalıyız. Misal, `<kullaniciAdi>` gibi..
  
  ```python
  from django.urls import path
  from django.http import HttpResponse
  
  def kullaniciBilgisiGetir(request, kullaniciAdi):
      return HttpResponse(f"<h3>{kullaniciAdi} kullanıcı sayfası<h3>")
  urlpatterns = [
     path('<kullaniciAdi>', kullaniciBilgisiGetir)#../<kullaniciAdi>
  ]
  ```

- Yukarıdaki kod uygulama ana url'sinden sonra gelen metni 'kullaniciAdi' isimli bir değişkene atar ve ilk parametre talep, ikinci parametre 'kullaniciAdi' olmak üzere bu iki parametreyi 'kullaniciBilgisiGetir' yöntemine yönlendirir.

> ***NOT :*** Url şemalarını barındıran listede değişken olanlar aşağıya, sâbit olan, öncelikli olan url eşleşme şemaları yukarıya yazılmalıdır. Uygulama içerisinde alt uygulama oluşturmak istediğimiz durumda bu oldukça önemlidir.
> 
> Misal, 'kurslar' uygulamamızın olduğunu ve bu uygulamaya 'kurslar/' bağlantı adresiyle geldiğimizi düşünelim. Bu bağlantı adresinden sonra gelen değeri 'kursIsmi' isminde bir değişken olarak ele aldığımızı düşünelim:
> 
> `urlpatterns = [path('<kursIsmi>', kursDetayGetir)]`
> 
> Ana uygulamaya '../kurslar/mobil-uygulama' adresli bir talep gelirse talep, 'kurslar' uygulamasına yönlendiriliyor. Bu durumda 'kurslar' uygulamasına gelen talebin url adresi 'mobil-uygulama' oluyor. Yukarıdaki şemaya göre buradaki 'mobil-uygulama' değeri 'kursIsmi' ismindeki bir değişkene aktarılıyor, sonra parametreler (talep, kursIsmi) 'kursDetayGetir' fonksiyonuna yönlendiriliyor. Eğer biz, 'kurslar' uygulamasında alt uygulama olarak 'kategori' uygulaması yapmak istesek ve bunun eşleşeceği talep url adresinin `../kurslar/kategori/<kategoriIsmi>` şeklinde olmasını istesek bu durumda kurslar uygulamasının 'urls.py' dosyasındaki 'urlpatterns' listesine şu elemanı eklememiz yeterli olur mu:
> 
> `path('kategori/<kategoriIsmi>)`
> 
> CEVÂP : eğer bu 'path' şemasını liste sonuna eklersek bu durumda 'kurslar' uygulamasına gelen hiçbir talep, 'kategori' uygulamasına yönlendirilmez; çünkü gelen tüm taleplerin url'leri birinci 'path' şeması ile eşleştiğinden, yönlendirme işlemi eşleşen bu ilk şemaya göre yapılır; bu yüzden gelen talep 'kursDetayGetir' fonksiyonuna yönlendirilir. Bu sebeple diğer şemaları kapsayan şemalar listede alt sıraya yazılmalıdır. Eğer elemanları listeye şöyle yazarsak uygulama istediğimiz gibi çalışır:
> 
> ```python
> from django.urls import path
> from django.http import HttpResponse
> """..."""
> urlpatterns = [
> path('kategori/<kategoriIsmi>)#../kurslar/kategori/<kategoriIsmi>
> path('<kursIsmi>', kursDetayGetir)#../kurslar/<kursIsmi>
> ]
> ```
> 
> ..

#### 'path' Şeması İçerisindeki Değişkenlerin Veri Tipini Belirleme

- Uygulamanıza gelen taleplerin adresinde gelen değerleri doğrudan değişkene atamak yerine uygun veri tipinde olanları atamayı tercih edebiliriz. Misal, makâleleri sunduğumuz bir web sitesi yapmak istiyoruz ve bu web sitesinde makâle bilgilerinin döndürüldüğü bir 'makale' uygulaması hâzırlamak istiyoruz. Uygulama gelen makâlenin ismine göre veyâ makâle numarasına göre makâle bilgisini cevâp olarak döndürsün istediğimizde 'makale' uygulamasının urls.py dosyasındaki 'urlpatterns' listesini şu şekilde yapılandırmalıyız:
  
  ```python
  urlpatterns = [
      path('int:<makaleNo>', numarayaGoreMakaleGetir),
      path('str:<makaleIsmi>', ismeGoreMakaleGetir),
  ]
  ```

- **!** Eğer burada sondaki 'path' şemasını listede öne alırsak, bu durumda gelen talebin adresi ne olursa olsun, gelen talep 'ismeGoreMakaleGetir' yöntemine yönlendirilir; zîrâ tüm veri tipleri metne dönüştürülebilir ve ilk şema eşleştiğinden alttaki şemaya bakılmaz. **Bu sebeple bir 'path' şemasını kapsayan 'path' şeması dâimâ alta yazılmalıdır.**

#### Talep Yönlendirme

- Gelen talepleri ele alırken her talebe karşılık bir cevâp döndürmek yerine, bâzen talebi yönlendirmemiz gerekebilir. Bu yönlendirme işleminde talebin url adresi değiştirilebilir.

- Bilhassa uygulamamızın başka yerlere gidip, geri dönmesi gibi durumlarda uygulamanın gittiği yerde talebin adresinin değiştirilerek yönlendirilmesi büyük önem arz etmektedir.

- Bu işlem için `django.http` modülü altındaki `HttpResponseRedirect` fonksiyonunu eklemeliyiz. Bu fonksiyonu kısa şekilde yazmak için ise `django.shortcuts` içerisindeki `redirect` fonksiyonunu uygulamaya eklemeliyiz. Bunu eklediğimizde `from django.http import HttpResponseRedirect` kodunu silebiliriz:
  `redirect('uygulamaIsmi/...')`

- Yukarıdaki kodda `redirect` yöntemine verilen parametre talebin parametresidir; fakat burada ana uygulama adresi hâriç url adresinin tamâmını yazmalısınız. Yukarıdaki örnek üzerinden gidersek, makâle numarası olarak gelen değeri makale ismi olarak yönlendirmek istediğimizde cevâp döndürmek istediğimiz yere şu kodu yazmalıyız:
  
  ```python
  isim = makaleIsminiGetir(makaleNo)
  redirect('/makale/' + isim)
  ```

- ..

#### Yanlış Bağlantı Adresiyle Gelen Talebi Değerlendirme

- Uygulamaya yanlış bir talep geldiğinde kullanıcıya hatâ mesajı göstermek için `django.http` modülü içerisindeki `HttpResponseNotFound` fonksiyonunu kullanabiliriz. Fonksiyona verilen metîn türündeki girdi kullanıcıya gösterilir, bi iznillâh:
  `return HttpResponseNotFound("Gelen talep tanınamadı")`
  Kullanıcıya '404' hatâ koduyla 'Gelen talep tanınamadı' hatâ mesajı döndürülür.

#### 'path' Şemalarını İsimlendirme

- Bilhassa gelen talebi yönlendirirken url bilgisini elle yazmak hatâya açık bir yapıdadır. Bunun yerine isimlendirme ile url'yi oluşturabiliriz; bunun için öncelikle yönlendirmek istediğimiz 'path' şemasına isim vermeliyiz:
  
  ```python
  path('str:<makaleIsmi>', ismeGoreMakaleGetir, name='ismeGoreMakale')
  ```

- Ardından `django.urls` modülünden `reverse` fonksiyonunu eklemeliyiz. Bu fonksiyon yönlendirilmek istenen 'path' şemasına verilen girdilere göre url adresi oluşturmak için kullanılır. Buradaki parametreler ('args' parametresine dizi olarak verilir) ilgili path şeması içerisindeki değişkenlere denk düşürülür; sırasıyla yazmak önemli (?). Makâle numarasını makâle ismine yönlendirmek için gerekli url adresini şu kodlarla üretebiliriz:
  
  ```python
  isim = makaleIsminiGetir(makaleNo)
  hedefUrl = reverse('ismeGoreMakale', args=[isim])
  redirect(hedefUrl)
  ```

- ..

## HTML SAYFALARI DÖNDÜRME

- Bir web sunucusu gelen isteğe göre geriye html sayfası döndürür ve tarayıcı da bunu görüntüler.

- Django'da HTML sayfalarını döndürmek için yapmamız gereken HTML dosyasının ismini `render` fonksiyonuna vermek ve bunun çıktısını geri döndürmek..
  Bunun için şu kod satırını dosyanın en üstüne eklemeliyiz:
  `from django.shortcuts import render`

- HTML dosyasını verirken sadece dosya ismini vermek istiyorsak bu durumda, bu dosyayı uygulama dizini içerisinde 'templates' dizini içerisine atmalıyız. Misal, proje dizinimiz (`django.conf.settings.BASE_DIR` ile proje dizinini öğrenebilirsiniz) ABC ise ve uygulama ismimiz 'laptops' ise, 'ABC/laptops/templates/' dizini içerisine atılan 'herhangiSayfa.html' isimli dosyayı uygulama içerisinde 'herhangiSayfa.html' olarak çağırabiliriz.

- Bunu yaptığımızda Django, aranan dosyayı evvelâ uygulama 'templates' dizini içerisinde arar; orada bulamazsa diğer uygulamaların 'templates' dizini altında arar. **Bu, varsayılan olarak böyledir; lâkin bu ayar değiştirilebilir**. Bu ayarı değiştirmek için proje dizinindeki 'settings.py' dosyasındaki 'TEMPLATES' listesi içerisinde bulunan sözlüğün 'APP_DIRS' anahtarına karşılık gelen değeri 'False' yapmalıyız:
  
  ```python
  TEMPLATES = [
      {
          #...
          APP_DIRS : False
      }
  ]
  # Bu ayar yapıldığında dosya diğer dizinlerde aranmaz
  ```

- ..

## VERİTABANI - NESNE İLİŞKİSİYLE VERİTABANI MODELLERİNİ ELE ALMAK (DJANGO DÂHİLÎ ORM ÇÖZÜMÜ)

- Django veritabanındaki verilerle yazılım içerisindeki nesneleri eşleyen ve nesne üzerine değişiklik yapıldığında bunu veritabanına kolayca kaydetmeyi sağlayan; veritabanı işlemlerini kolaylaştıran bir ORM (Object Relation Map) çözümü sunuyor.

#### 'models.Model' Nesneleriyle Veritabanı - Nesne İlişkisi Kurma

- Oluşturduğumuz nesneleri veritabanı üzerine eşlemek için kullanılan sınıf `models` sınıfıdır. Bu sınıf `django.db` modülü içerisindedir. Oluşturmak istediğimiz tabloları nesne olarak tanımlıyoruz; ancak bu nesneler `models.Model` sınıfının alt sınıfı olmak zorunda.

- Misal üzerinden gidelim, inşâAllâh..

- Ürünleri tutan bir web uygulamamız olsun. Her ürünün id, name, price, description, startDate ve satışta olup, olmadığını belirtmek için isActive özelliği olsun. Bunun için ilgili sınıfı şöyle tanımlamalıyız:
  
  ```python
  from django.db import models
  class Product(models.Model):
      name = models.CharField(max_length=40)
      price = models.DecimalField()
      description = models.(TextField)
      startDate = models.DateField()
      isActive = models.BooleanField()
  ```

- Yukarıdaki koda göre tabloya yeni satır eklenirken tüm alanların boş olmaması zorunludur; yanî sütunlar 'NOT NULL' özelliktedir. Bunun böyle olmaması için alanı oluştururken `null=True` parametresini vermeliyiz.

- ..

#### Veritabanı Kodlarını İşletmek İçin Kullanılan Bir Sınıf : Migration

- Yazdığımız nesne ve özellikleri veritabanına tablo olarak işletmek için `Migration` sınıfı kullanılır. Bu bir nevi sorguları saran bir çerçevedir. Modelde yapılan değişikliklerin veritabanına yansıtılması çoğu zamân otomatik olacak şekilde tasarlanmış, diye belirtiliyor; fakat en başta bunun ne olduğunu ve nasıl kullanıldığını öğrenmemiz gerekiyor.

- Bu yapı ile veritabanı tablo yapısındaki değişiklikleri kontrollü şekilde yapabiliyoruz. Eğer yaptığımız son değişikliği geri almak istiyorsak, bunun için birçok sql kodu yazmak yerine bunu buradan yapabiliyormuşuz. `Migrations` modülü bâzı komutlar barındırıyor. Bu komutlar, model - veritabanı eşlemesi için kullanılıyor.

- 'Migration' komutları:
  
  1. `migrate` : Uygulama içerisinde `django.db.models.Model` sınıfıyla tanımlanan, yanî veritabanında oluşturulması istenen bir nesne varsa, bunu veritabanına uygulamak için bu komut kullanılır. Bu komutu, 'django.shell' ortamında kullanabiliriz, uygulama içerisinde de kullanılabilir; uygulama tarafından bir kod yürütmek yerine doğrudan, sunucu bilgisayarında yerel olarak bu kodu çalıştırmak için `py manage.py migrate` kodu komut ekranında çalıştırılmalıdır.
     
     ***NOT*** : Python kabuk modundan çıkmak için `quit()` komutu çalıştırılır.
  
  2. `makemigrations` : Bu komut, uygulama içerisinde yeni yaptığımız model değişiklikleri için 'Migration' oluşturur. Bu 'Migration' uygulama ana dizini altındaki 'migrations' dizini içerisinde yer alır.
  
  3. `showmigrations` : ..

- ..

#### Yeni Kayıt Ekleme

- Yeni kayıt ekleme işlemi web uygulamasında formlar üzerinden veyâ arkaplanda çalıştırılan bir kod ile yapılabilir; fakat sunucu bilgisayarda yerel olarak yeni kayıt eklemek için python kabuk modunda 'manage.py' dosyasını çalıştıralım:
  `python manage.py shell`

- Daha sonra 'uygulamaIsmi.models' örüntüsüyle eşleşen dizindeki 'Model'i ekleyelim. Misal, 'ticaret' uygulaması içerisinde 'Product' isminde bir modelimiz varsa, `from ticaret.models import Product`  kodunu yazarak ilgili sınıfı ekleyelim.

- Bu kodu çalıştırdıktan sonra 'Product' sınıfından yeni bir değişken (nesne) oluşturalım.

- Oluşturulan nesne üzerinden çağırılan 'save()' yöntemiyle veritabanına kayıt ekleyebiliriz.

- Bir başka kayıt ekleme yöntemi ise ilgili 'Model'in 'objects' özelliğinin 'create' yöntemini kullanmaktır:
  `Product.object.create(...)`

- Yukarıdaki kodda üç nokta ile belirtilen yere oluşturulmak istenen 'Product' nesnesinin parametreleri verilir. Eğer bu şekilde nesneyi oluşturursak, bu durumda `save` yöntemini çalıştırmaya gerek kalmaz.

#### 'Field' Alanının Özellikleri

- Bir 'Field' oluştururken verebileceğimiz parametrelerdir. Bunlar 'Field' alanının özellikleridir:
  
  1. **null (Field.null)** : Bu parametre alanın 'NULL' veri barındırıp, barındıramayacağını belirtmek için kullanılır. Varsayılan değeri `False`'tur. Eğer bu parametre `True` yapılmazsa, veri tabanına kayıt eklenirken eklenen kaydın o alanı mutlaka veri içeriyor olmalıdır. Metîn bazlı alanlar ('CharField', 'TextField') için 'null=False' vermekten kaçınmak gerekir. Django boş metni veritabanına gönderirken 'NULL' olarak göndermediğinden yine de hatâ alınmayabilir; fakat bunun da bir istisnası vardır; bir alanın `blank` parametresi `True` ise ve o alan için `unique` parametresi `True` ise bu durumda, boş metîn değeri yalnızca bir kaydın söz konusu alanına atanabileceğinden hatâ alınabilir.
  
  2. **blank (Field.blank)** : Django'da nesnelere göre otomatik form oluşturma gibi işimizi kolaylaştırıcı yapılar / hizmetler vardır. Otomatik form oluşturulduğunda form doğrulaması yapılırken alanın boş olarak geçilememesini istiyorsak modelin o özelliğini oluştururken `blank=False` yazarak bunu belirtmeliyiz.
  
  3. **db_column (Field.db_column)** : Alanın veritabanındaki sütun ismidir. Bu verilmediğinde özelliğin ismi, veritabanındaki sütunun ismi olarak atanır. Eğer bir nesnenin bir özelliğinin uygulama içerisindeki ismi ile, o alanın veritabanı tablosundaki karşılığı olan sütunun isminin farklı olması isteniyorsa bu parametreye istenen sütun ismi verilmelidir.
  
  4. **db_comment (Field.db_comment)** : Sütunun veritabanındaki yorumudur (açıklamasıdır). Doğrudan veritabanına bakıldığında hangi sütunun ne verisi barındırdığını anlamak için tablodaki hangi sütunun ne anlama geldiğini belirtmek isâbetli olur.
  
  5. **db_default (Field.db_default)** : Django'nun 5. versiyonu ile gelen bir özelliktir. Bu parametreye sütun için varsayılan bir değer verebiliriz. Misal, veritabanındaki 'Kullanici' tablosuna yeni kayıt eklediğimizde 'kayit_tarihi' alanının otomatik olarak o anki zamânı barındırması için şu kodu yazabiliriz:
     
     ```python
     from django.db import models
     class Kullanici(models.Model):
         kayit_tarihi = models.DateTimeField(db_default=Now())
     ```
  
  6. `db_index (Field.db_index)` : Eğer bu alan için `True` değeri verilirse veritabanında o alan için 'index' oluşturulur. Veritabanında indeks o alana göre verilerin sıralı bir hâlinin barındırılması demektir. Bu, sürekli sorgu yapılan alanlar için kullanılan bir özelliktir. Misal, kullanıcı ismi için bir indeks oluşturduğunuzda veritabanında o alandaki veriler alfabetik olarak sıralı bir şekilde saklanan bir yapı barındırır. Nasıl alfabetik olarak sıralanmış bir rehberde bir ismi bulmak çok daha kolaysa veritabanında da bu, o alan için daha az maliyetle sorgu yapabilmeyi sağlar.
  
  7. **primary_key (Field.primary_key)** : Veritabanındaki birincil anahtar olmasını istediğimiz sütun için `primary_key` parametresini `True` olarak vermeliyiz.
  
  8. **unique (Field.unique)** : Bir alanın değerinin münferid (tekil) olmasını istiyorsak o alanı oluştururken `unique` parametresini `True` olarak vermeliyiz.
  
  9. ..

- ..

#### Veritabanından Kayıt Sorgulama

- Oluşturduğumuz `Model`'in `objects` özelliği bize `manager` sınıfından bir nesne döndürüyor. Bu nesne üzerinden sorgulamalarımızı yapabiliriz.

##### 1. Tüm kayıtları çekme

Tüm kayıtları çekmek `manager` değişkeninin `all()` yöntemini kullanabiliriz:

```python
tumUrunler = Product.objects.all()
```

- Yukarıdaki kod `QuerySet` sınıfından bir nesne döndürür. Bu nesne içerisinde kayıtları barındırır.

##### 2. Belirli kayıtları çekme

- Bunun için yine 'manager' nesnesi üzerinden bir yöntemi çağırmalıyız. Bu yöntemin ismi `filter(**kwargs)`'dır. Yönteme hangi sütun için hangi değer olmasını istediğimizi belirterek sorgu yazabiliriz. Veritabanı tablosundaki sütunları birer parametre gibi vererek sorgu yazabiliriz. Misal:
  
  ```python
  Product.objects.filter(name="Samsung S23")
  ```

- Yukarıdaki kod 'Product' tablosundaki 'name' alanı 'Samsung S23' olan kayıtları getiriyor.

##### 3. Belirli kayıtların dışındaki kayıtları seçme

- Bunun için de `exclude(**kwargs)` yöntemi kullanılır. Kullanımı `filter()` ile aynıdır. Bu yöntemde verilen değerlerin eşleşmediği tüm kayıtlar getirilir. Misal, aşağıdaki kod, isim alanı "Samsung S23" olmayan tüm kayıtları getirir:
  
  ```python
  Product.objects.exclude(name="Samsung S23")
  ```

##### Tek bir kaydı sorgulama

- Tek bir kaydı getirmenin kolay bir yolu `get(**kwargs)` yöntemini kullanmaktır:
  
  ```python
  Product.objects.get(pk=1)
  ```

- Yukarıdaki kod birincil anahtar ('primary key' ('pk')) değeri 1 olan kaydı getirir. İstenildiği takdirde `pk` yerine herhangi bir sütun ismi parametre olarak verilebilir.

- Bu yöntemin diğerinden farkı bu yöntemle tek bir kaydın gelmesidir. `filter()` yöntemiyle birden fazla kayıt gelebilir; bu sebeple gelen nesneler liste ile sarmalanarak geri döndürülür; bu yöntem ise her zamân (?) tek bir kaydı geriye döndürür.

##### Daha özelleştirilebilir sorgulama

- Veritabanında bir alan üzerinde sorgu yapılırken büyüktür, küçüktür gibi işleçler kullanılabiliyor. Burada tüm işlemleri yöntemlerle yazdığımızdan bunun için de bize bir yapı sağlanmış olmasını bekliyoruz.

- Filtreleme işlemleri için `filter` yöntemi kullanılıyor.  Bu sebeple filtreleme işlemleri için parametreler sunulması gerekiyor.

- İlgili için alan isminden sonra işleçler yazılarak ilgili alan üzerinde 'büyüktür', 'küçüktür' gibi sorgulamalar yapılabilir.
  
  ###### filter yöntemi parametreleri:
  
  1. `__lte` : 'less than equal' (küçük eşittir) ifâdesinin kısaltılmış hâlidir. Bu parametre kullanıldığında alandaki değeri verilen değerden daha düşük olan kayıtlar getirilir.
     `Product.objects.filter(price__lte = 3000)`
     Yukarıdaki kod 'Product' tablosundaki kayıtlar içerisinden 'price' alanı 3000 değerinden küçük olan kayıtlarla eşleşir, o kayıtları geri döndürür.
     
     ***NOT :*** Târih alanında `__lte` gibi işleçler kullanılırken değer 'yyyy-aa-gg' (?) şeklinde yazılmalıdır. Misal:
     `Product.objects.filter(startDate__lte = '2012-01-02')`
     Yukarıdaki kod 'startDate' alanı 2 Ocak 2012'den daha önceki bir zamân değeri olan kayıtlarla eşleşir, o kayıtları döndürür.
  
  2. `__gte` : Kullanım biçimi `__lte` ile aynıdır; 'greater than equal' (büyük eşittir).
  
  3. `__gt` : 'greater than' (büyüktür) işleci
  
  4. `__lt` : 'less than' (küçüktür) işleci
  
  5. `__exact` : İlgili alan değeri verilen değer ile aynı ise, o kayıt getirilir.
  
  6. `__iexact` : Yukarıdaki ile aynıdır; sadece büyük küçük harf duyarsız şekilde sorgu işlemi yapar. 'ignore' anlamındaki 'i' takısı bunu ifâde etmektedir.
  
  7. `__contains` : Verilen sütun için verilen değeri barındıran kayıtlar getirilir
  
  8. `__icontains` : Büyük küçük harf duyarsız şekilde verilen değeri barındıran kayıtlar getirilir.
  
  9. `__startswith` : Verilen değerle başlayan kayıtlar getirilir; eğer bu işlemi büyük küçük harf duyarsız şekilde yapmak istiyorsak, bu durumda `__istartswith` işlecini kullanmalıyız
  
  10. `__endswith` : Verilen değerle biten metîn kayıtlarını çekmek için kullanılır; büyük küçük harf duyarsızlığı için `__iendswith` işlecini kullanmalıyız.
  
  11. ..
  
  ###### Birden fazla koşulu mantıksal bağlaçlarla berâber kullanmak
  
  `filter` yöntemine parametre olarak verdiğimiz her bir koşul birbirine 'Ve' bağlacıyla bağlanmış bir sorgu olarak oluşturulur. Yanî verilen koşulların tamâmını sağlayan kayıtlar döndürülür. Bâzı durumlarda göreceli sorgu yazılmak istenebilir. Bu durumda sorgu cümlesini değiştirmeye yarayan sınıfı eklemeliyiz:
  `from django.db.models import Q`
  Bahsi geçen sınıf `Q` sınıfıdır. `Q` sınıfı içerisinde sorgunun parçaları yazılır ve daha sonra bu parçalar ',' ('ve') veyâ '|' ('veyâ') işleciyle birbirine bağlanır. Bu `Q` değişkenleri `filter` yöntemi içerisinde yazılır.
  Misal, fiyatı '3000'den küçük olan veyâ isim alanında 'Samsung' metnini barındıran ürünleri getirmek istiyorsak şöyle bir kod yazmalıyız:
  `Product.objects.filter(Q(name__contains("Samsung") | Q(price__lt=3000)))`
  Eğer bu kayıtlar içerisinden 'isActive' alanı `True` olan kayıtları getirmek isteseydik en son yazdığımız `Q` ifâdesinden sonra `, isActive=True` yazmalıydık.

- ..

- 
