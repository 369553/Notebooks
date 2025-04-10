# REACT

## React Nedir? (Kısaca)

- React, kullanıcılara etkileşimli web sayfaları hâzırlamak için kullanılan, Facebook tarafından geliştirilmiş, MIT lisansıyla sunulan bir Javascript çerçevesidir.

## React Kurulumu

- React'ı kurmak için tavsiye edilen yol, React'ı node.js ile gelen 'npm' (node package manager) üzerinden kurmaktır.

- Bunun için evvelâ node.js'i indirip, kurun.

- Node.js'i indirdikten sonra, React'ı yüklemek için komut satırına `npm install -g create-react-app` komutunu yazmalıyız.

- Buradaki `-g` parametresi "global" anlamına gelmekte olup, react'ı sadece bulunulan dizin için değil; her yerden erişilebilir olarak kurmak için yazılır.

## React Projesi Oluşturma

- Bunun için komut satırında projeyi oluşturmak istediğimiz dizine gelip, `npx create-react-app projeismi` kodunu yazmalıyız; buradaki 'projeismi' yerine kendi proje isminizi yazın.

- React projesi için proje ismi büyük harf içeremez.

## Ortamı Tanıma

- Dizin içerisinde uygulama içinde kullanılacak paketlerin kullanımı gibi ayarları belirlediğimiz "package.json" dosyası vardır.

- Kodlarımız 'src' dizini altındadır.

- Github bağlantısı kurulduğunda hangi dizinlerin dışlanacağını belirtmek için '.gitignore' dosyası vardır.

- Uygulama içerisindeki ana kod dosyalarımız 'src' dizini altındaki 'index.js' ve 'app.js' dosyalarıdır. Bu dosyalarla 'public' dizini altındaki 'index.html' sayfasını kontrol ediyoruz.

- 'index.js' dosyası, 'app.js' dosyası ile belirtilen bileşeni işler ('render' eder); bu sebeple üzerinde en çok oynamamız gereken dosya 'app.js' dosyasıdır.

- Uygulamada kullanmak için yüklediğimiz bağımlılıklar (paketler) 'node_modules' dizini altına eklenir.

#### 'package.json' Dosyasını Tanıma

- En temel yapılandırma dosyasıdır.

- Yapılandırma ve ayarlar JSON formatında, tek bir nesne olarak saklanır; yanî 'package.json' en temelde bir nesne barındırır (yanî dosya başında ve sonunda süslü parantez var).

- Bu nesnenin bâzı özellikleri şöyledir:
  
  - name : Metîn tipinde bir değer tutar, proje ismini bildirir
  
  - version : Uygulama versiyon numarasını metîn tipinde tutar.
  
  - dependencies : Uygulama bağımlılıklarını bir nesne olarak tutar; her bir bağımlılık için bir bağımlılığın ismi ve değer olarak da versiyon numarası belirtilir.
  
  - scripts : Nesne tipindedir. Komutların tek isimle çalıştırılması için kullanılır.

## Uygulamayı Yayına Alma

- Bunun için komut satırına `npm start` komutunu yazmalıyız.

- Bu komut, uygulamayı node.js üzerinde yayına alır.

- Uygulama yayını için varsayılan port 3000'dir.

- Uygulama yayındayken yaptığınız değişiklikleri yayın ortamına aktarmak için tek yapmanız gereken değişiklik yaptığınız dosyayı kaydetmektir.

## TEMEL BİLGİLER

- React "Single Page Application" (SPA) türünde bir uygulamadır.

- Ana mantığı bir 'Component' (bileşen) içerisinde birden fazla bileşenin hiyerarşik olarak tutulduğu bir yapı ile sayfayı idâre etmektir. Bu hiyerarşik düzen ağaç yapısı gibidir.

- Uygulama tek bir ana bileşen içerir ve diğer bileşenler de bu bileşenin içerisindedir.

- Bileşenler arası veri aktarımı veyâ üst bileşen ile alt bileşen arasında veri aktarımı meselesi React için zor meselelerden birisidir. Zîrâ React'ta bir bileşen yalnızca kendi içerisinde bulunduğu bir alt bileşene parametre gönderebilir. Yanî React'te şunlar yoktur:
  
  - Birbirinden bağımsız bileşenler arası veri aktarımı yoktur
  
  - Bir bileşen kendisinden bir üst hiyerarşik sırada bulunan bileşene veri gönderemez ('two-way-binding' (çift yollu aktarım) yoktur)
  
  - Hattâ bir bileşen hiyerarşik sırada kendisinden iki alt sırada bulunan bileşene dahî veri gönderemez (yalnızca bir alt hiyerarşideki bileşene veri gönderebilir).

- Bu menfî durumlara karşın React'ın tercih edilebilir olmasını sağlayan özellikleri de vardır. Bunlardan birisi performanstır. React, bir değişiklik olduğunda sayfanın ilgili yerini değiştirmeyi sağlayan bir yapıya sâhiptir. Böylece hem sayfa yenilenmeden veriler ve bileşenler tazelenir; hem de bütün sayfa değil, değişiklik yapılan yer tazelenerek hız ve performans kazancı sağlanır.

- React içerisinde Javascript kodları ve JSX kodları barındırır. JSX özel HTML ve Javascript karışımı özel bir dildir ve çok kolaydır. Bu dil aynı HTML yazar gibi React bileşeni oluşturmayı sağlayan kolay bir dildir. Bu da React'ın bir diğer güzel yanıdır.

- React yazarken çok kullanılan Bootstrap kütüphânesini kullanmayı kolaylaştırabilmek için bootstrap'i kullanan 'reactstrap' yapısı vardır; fakat bu yapı standart react uygulamasında dâhilî olarak gelmez; eklememiz gerekiyor.

- React'ın en iyi yanlarından birisi performansının yüksek olmasıdır. Bu performans yüksekliğinin en önemli sebeplerinden birisi herhangi bir değişiklik esnasında sayfanın tümünün yeniden çizilmeyip, sadece değişen yerin yeniden çizilmesi özelliğidir. İşte tam da bu özellik sebebiyle React çerçevesi her bir bileşenin birbirinden ayırt edilebileceği bir özelliğinin olmasını istemektedir.

- Bu sebeple bir liste elamanının bir bileşen olması durumunda, React her bir elemanın birbirinden ayrılması için bir 'key' istemektedir. Bunu, sayfayı işlerken ('render' ederken) sayfanın neresinin işlemesi gerektiğini tespit edebilmek için istemektedir. Eğer 'key' belirtilmezse React hatâ verir!

## React Yazmaya Başlarken

- Bileşenler ('Components') birkaç farklı şekilde oluşturulabiliyor:
  
  1. Fonksiyon ile: Geriye JSX döndüren fonksiyonlar aslında bir bileşen döndürür. Bir fonksiyon `return` anahtar kelîmesinden sonra parantez içerisinde JSX kodları döndürüyorsa, bu fonksiyon geriye bir bileşen ('component') döndürüyor demektir.
     
     ```jsx
     function App(){
         return (// Bu parantezle JSX'e özel kodlar başlıyor
             <>// Boş fragment'ı simgeler
             <div>
                 <h2>Bismillâh!..</h2>
             </div>
             </>
         );// JSX'e özel kodlar burada bitiyor
     }
     ```
  
  2. Sınıf ile : Bir Javascript sınıfının bir bileşen olabilmesi için 'Component' sınıfından kalıtım alması gerekmektedir. Ayrıca bu sınıfın da ilgili sayfaya `import` ile dâhil edilmesi gerekmektedir. Sınıf içerisinde JSX kodunu yazarak bileşen oluşturma işlemini `render(){/*....*}` fonksiyonu ile yapıyoruz:
     
     ```jsx
     import React, {Component} from 'react'
     export default class NavBar extends Component{
         render(){
             <div>
                 <h2>Bismillâh</h2>
             </div>
         }
     }
     ```
     
     Yazılan bileşeni 'app.js' içerisinde kullanmak istersek, yazılan bileşeni bir HTML sınıfı gibi kullanıyoruz:
     
     ```jsx
     import React from 'react'
     import NavBar from './NavBar'
      function App(){
          return(
              <NavBar/>
          )
      }
      export default App;
     ```
3. React hooks ile : React'a 16.8. versiyonla dâhil edilen bir özelliktir. ...
- JSX içerisinde yazılan HTML benzerî kodlar HTML bileşenlerini de barındıran React bileşenlerini oluşturur.

- React'ta bir bileşeni göstermek ve gizlemek gibi işlemleri kolayca yapmak için bir boolean Javascript değişkeniyle ve('&&') işlemine tâbî tutmak pratik bir yoldur:
  
  ```jsx
  import React from 'react'
  import NavBar from './NavBar'
   function App(){
      isVisible = true;
       return(
          <>
              <button onClick={()=>{isVisible = !isVisible;}}>
                  Detayları göster / gizle
              </button>
              {isVisible &&
                  <div id="details">...</div>
              }
          </>
       )
   }
   export default App;
  ```

- ..

#### JSX  Hakkında

- JSX kodu içerisinde yorum satır(lar)ı oluşturmak için `{/*` kodu yazılır; yorumu bitirmek için `*/}` kodu yazılır. Eğer Javascript içerisindeysek doğrudan bunları kullanabiliriz : `/*..*/` 

- JSX içerisinde HTML yazabilirsiniz; fakat React'ın hiyerarşik yapısını unutmayın. Bir HTML etiketi içerisine yazdığınız başka bir HTML etiketi, sonra yazılan HTML bileşeninin diğer bileşenin içerisinde olduğunu ifâde eder.

- Kendi tanımladığımız bileşenlerin isimlerinin ilk harfi büyük harf olmalıdır. Bu, HTML elemanlarının JSX elemanlarıyla ayırt edilebilmesi için gereklidir.

- **JSX içerisinde Javascript kodu yazmak için süslü parantezler kullanılır**. Süslü parantez içerisinde sadece bir Javascript kod cümlesi yazılabilir. Süslü parantez içerisinde yeniden JSX kodu yazılabilir; bunun için normal parantez açmak kâfîdir.

## Reactstrap

- Bootstrap kütüphânesinin React bileşenlerine dönüştürülmüş hâlidir.

- Bunun için komut ekranına `npm install reactstrap` yazılabilir.

- Veyâ başka bir yöntem olarak 'package.json' dosyası içerisindeki 'dependencies' kısmına 'reactstrap' versiyon bilgisiyle berâber eklenir  ve bu bağımlılıkların yüklenmesi için komut ekranından npm install komutu çalıştırılır.

- Reactstrap bootstrap'e bağımlıdır; fakat siz reactstrap'i kurduğunuzda 'bootstrap' otomatik olarak yüklenmemektedir; bu sebeple 'bootstrap'i de yüklemeliyiz:
  
  `npm install bootstrap`

- Kütüphâne yüklendikten sonra uygulamanın durdurulup, yeniden yayına alınması gerekebilir.

- Reactstrap'i kullanmak için 'index.js' dosyasına şu kütüphâneyi eklemeliyiz:
  
  ```jsx
  import 'bootstrap/dist/css/bootstrap.min.css';
  ```

- Daha sonra hangi sayfada hangi mimari yapıyı kullanacaksak onu 'reactstrap'ten eklememiz gerekiyor. Reactstrap yapıları bootstrap ile aynı isimdedir; fakat baş harfleri büyüktür:
  
  ```jsx
  import {Container, Row, Col} from 'reactstrap';
  ```

- ..

- 'reactstrap' ile bir kullanım örneği:
  
  ```jsx
  import {Container, Row, Col} from 'reactstrap';
  function App(){
      return(
          <div>
              <Container>
                  <Row>
                      <Col xs="3">Küçük sütun (1/4)</Col>
                      <Col xs="9">Büyük sütun (3/4)</Col>
                  </Row>
              </Container>
          </div>
      )
  }
  ```

## 'PROPS' İLE ALT ELEMANA VERİ TAŞIMA

- React ile üst bileşenden hiyerarşide bir alt kısımda olan bileşene veri taşınabilir.

- Bu, iki kısımdan oluşur. Birincisi üst bileşenden veriyi göndermektir; ikincisi alt bileşen içerisinde gönderilen veriyi almaktır. Üst bileşenden veriyi gönderirken, HTML etiketinin bir özelliğini yazar gibi bunu yapıyoruz. Göndermek istediğimiz verinin ismini özellik ismi gibi yazıyoruz:
  
  ```jsx
  function App(){
      return(
          <>
              <Categories title="Kategoriler"/>
          </>
      );
  }
  ```

- Bunun için öncelikle alt bileşeni bir sınıf ile tanımlamalıyız ve sınıfa 'props' alan bir yapıcı yönteme eklemeliyiz:
  
  ```jsx
  export default class Categories extends Component{
      constructor(props){
          super(props);// Alınan 'props' Component'e gönderiliyor
      }
  }
  ```

- Yapıcı yönteme `super(props);` kodunu eklememizin sebebi JSX içerisinde bunu `this.props` koduyla kullanabilmemiz içindir (çünkü Javascript'te 'this' ifâdesi üst sınıfı olan sınıf için üst sınıfı işâret eder. Bu, Javascript'in özünde sınıf yapısının olmamasından dolayıdır).

- JSX içerisinde gönderilen değere şu şekilde erişebiliriz:
  
  ```jsx
  return(
      <Container>
          <Row>{this.props.title}</Row>
      </Container>
  )
  ```

- JSX içinde Javascript kodu yazabilmek için süslü parantez kullanmamız gerekiyor.

- 'props' yapısıyla üst bileşenden alt bileşene dinleyici için fonksiyon da taşınabilir.

- Tavsiye etmemekle berâber, bileşene gönderilen 'props' değişkenleri şu şekilde de alınabilir:
  
  ```jsx
  export default class Categories extends Component{
      constructor({isim}){
          this.isim = isim;
      }
  }
  ```

- ..

#### 'props' ile Dinleyiciler İçin Fonksiyon Taşıma

- Dinleyiciler için fonksiyon taşıma işlemi 'props'tan farklı değildir; fakat bunu kullanırken yapmamız gereken bir değişiklik var.

- 'props' ile dinleyici fonksiyonunu bir bileşenin 'onClick' gibi bir özelliğine atamak istediğimizi düşünelim. İlk bakışta şöyle bir kod doğru görünebilir:
  
  ```jsx
  export default class Navi extends Component{
      constructor(props){
          super(props);
      }
      state={text : "Başlık"};
      render(){
          return(
              <div>
                  <Button onClick={this.setState({text:"!"})}></Button>
              </div>
          )
      }
  }
  ```

- Bu koddaki sıkıntı, fonksiyonun düğmeye tıklanmadan çalıştırılmasından kaynaklanıyor. Bileşenin durumu düşmeye tıklanmadan değiştiriliyor, React, durumu değişen bileşeni ve alt bileşenlerini yeniden çiziyor, fonksiyon yine çalıştırılıp, bileşenin durumu yeniden değiştiriliyor.

- Dolayısıyla bizim 'onClick' özelliğine fonksiyonun referansını vermemiz gerekiyor. Bunun için yeni bir fonksiyon yazabiliriz; fakat bu fonksiyona parametre gönderemeyeceğimizden dolayı, her yeni parametre için yeni bir fonksiyon yazmamız gerekir. Bu, kabûl edilebilir bir şey olmadığından, isimsiz fonksiyonları kullanmalıyız:
  
  ```jsx
  <Button onClick={()=>this.setState({text:"!"})}></Button>
  ```

- Yukarıdaki kod düğmeye tıklandığında çalışır.

#### Gelen Özelliklerin ('props') Tipini Belirlemek

- Bir bileşene 'props' ile gelen özelliklerin belli bir tipte olduğunu belirtmek istiyorsak 'propTypes' özelliğini kullanmalıyız.

- 'PropTypes' ı kullanabilmek için öncelikle onu dosyamıza eklemeliyiz:
  
  ```jsx
  import PropTypes from 'prop-types';
  ```

- Bileşenimizi sınıf olarak veyâ fonksiyon olarak tanımlamış olabiliriz; bu durum bizim yöntemimizi değiştirmez. Bileşeni tanımladıktan sonra şu şekilde bileşene gelen özelliklerin tipini belirtebiliriz:
  
  ```jsx
  class Navi extends Component{/*...*/}
  Navi.propTypes = {
      text : PropTypes.string,
      pageNumber : PropTypes.number,
      changePage : PropTypes.func,
      listOfContent : PropTypes.array
  }
  ```

- Yukarıdaki gibi gelen özellikler için tip belirtilmesi zorunlu değildir, istenilen özellik için belirtilebilir, istenmezse belirtilmeyebilir.

- Yukarıdaki gibi tip belirtimi yaptıktan sonra bu bileşene yanlış tipte bir özellik ('prop') gönderilirse uygulama yine çalışır; fakat konsola uyarı yazdırır.

- Eğer bir özelliğin birden fazla tipte olması söz konusu ise, bu durumda şöyle bir tip belirtimi yapmalıyız:
  
  ```jsx
  class Navi extends Component{/*...*/}
  Navi.propTypes = {
      text : PropTypes.oneOfType([
          PropTypes.string,
          PropTypes.number,
      ]),
  }
  ```

- İstediğimiz tipteki bir dizi olması belirtimini ise şu şekilde yapabiliriz:
  
  ```jsx
  class Navi extends Component{/*...*/}
  Navi.propTypes = {
      listOfContent : PropTypes.arrayOf(PropTypes.string)
  }
  ```

- ..

#### Bileşene Gelen Özellikler ('props') İçin Varsayılan Değer Atama

- Bunun için bileşen ('Component') tanımlandıktan sonra, `bilesenIsmi.defaultProps = {"ozellikIsmi":varsayilanDeger}` gibi bir tanımlayla bileşene gönderilmeyen değerler için varsayılan bir değerin olması sağlanabilir
  
  ```jsx
  Navi.defaultProps = {
      title : "Varsayılan Başlık",
      pageNumber : 1
  }
  ```

- ..

#### Gelen Özelliğin Zorunlu Olduğunu Belirtmek

- Gelen özelliğin zorunlu olduğunu belirtmek için özelliğin tipini belirttikten sonra `.isRequired` kodunu eklemeliyiz:
  
  ```jsx
  Navi.propTypes = {
      text : PropTypes.string.isRequired
  }
  ```

- Eğer özellik için bir tip kısıtlaması yapmak istemiyorsak, 'any' tipini kullanabiliriz:
  
  ```jsx
  Navi.propTypes = {
      element : PropTypes.any.isRequired
  }
  ```

- Zorunlu olarak belirttiğimiz bir özellik verilmediğinde uygulama yine çalışır; fakat konsola uyarı yazdırır. 

> ***NOT :*** Zorunlu olarak belirtilen bir özellik için varsayılan değer atandığında uygulama uyarı da vermez; çünkü varsayılan değer atandığı için zorunluluk yerine gelmiştir.

- ..

## BİLEŞENLERİN BARINDIRDIĞI DİNAMİK VERİ : STATE

- Bileşenlerin verisini üst bileşenden taşısak da, bu veriler sayfadaki kullanıcı etkileşimleriyle değişebilir. Bu sebeple, bir bileşenin kendine âit bir durum verisi olmalıdır. Bunun için kullanılan yapının ismi 'state'dir.

- Fonksiyonla tanımlanan bir bileşende 'state' olarak tanımlanmayan bir değişkenin değeri değiştiğinde sayfa yeniden işlenmez ('render' edilmez).

- Sınıf ile tanımlanan bir bileşende de yalnızca `state` nesnesi içinde tanımlanan değişkenler, yalnızca `this.setState()` yöntemiyle değiştirildiğinde sayfa yeniden işlenir.

- 'state' nesnesini için yapıcı yöntemde tanımlayabiliriz:
  
  ```jsx
  export default class Categories extends Component{
      constructor(){
          this.state = {selectedCategory : "Yağlar"};
          // Değişken içerisine istenilen değer yazılır
      }
  }
  ```

- 'state' nesnesini sınıf içerisinde de tanımlama özelliği React'e yeni eklenmiş sanırım:
  
  ```jsx
  export default class Categories extends Component{
      this.state = {selectedCategory : "Yağlar"};
  }
  ```

- Aslında yukarıdaki tanımda sınıf içerisinde 'state' isimli bir nesne tanımlıyoruz. React'ı kullanırken kullanmamız gereken 'state' ise dosyamıza eklenmelidir:
  
  ```jsx
  import React, {useState} from 'react';
  ```

- Eklediğimiz bu fonksiyonu bileşen içerisinde kullanırken bâzı şeyleri bilmemiz gerekiyor. Birincisi, her bir durum ('state') tanımını ayrı tanımlayarak 'durum'ların önceki değerlerine kolayca erişebiliriz. Bu, hem önceki duruma dönmede, hem de ekran yenileme işlemlerini performanslı hâle getirmede bize katkı sunuyor.

- useState fonksiyonunu sınıf bileşenlerde ('react class component') kullanamıyorsunuz; fonksiyon bileşenlerde ('react function component') kullanabiliyorsunuz.

- Durumu tanımlarken bir liste tanımlıyoruz, listenin ilk elemanı durum değişkeni, ikinci elemanı ise o durumu değiştirmek için kullanacağımız fonksiyondur. Bunlara istediğimiz ismi verebiliriz; fakat anlaşılırlık açısından 'durum' 'setDurum' tarzındaki isimlendirmeyi tercih etmeliyiz:
  
  ```jsx
  import React, {useState} from 'react';
  function Navi{
      const [title, setTitle] = useState("varsayılanBaşlangıçDeğeri");
      const changeTitle = (title)=>{setTitle(title)};
      return(
          <>
              <h2>{title}</h2>
              <button onClick={()=>changeTitle("Yeni başlık")}>
                  Başlık değiştir
              </button>
          </>
      )
  }
  export default Navi;
  ```

- Bâzen bir durumu bir nesne veyâ bir dizi olarak tanımlayabiliriz. Nesne veyâ dizi tipindeki bir durumun içerisinden sadece seçtiğimiz değerleri değiştirmek isteyip, diğer değerlerini elde tutmak istersek '...durumIsmi' değerini yeni tanımın önüne eklemeliyiz:
  
  ```jsx
  function Navi{
      let [info, setInfo] = useState({ name: "Mehmed",
          surname: "SOLAK" });
      let [certs, setCerts] = useState(["React"]);
      return(
          <>
              <h2>{isim}</h2>
              <button onClick={()=>setInfo({...info, name:"Âkif"})}>
                  İkinci ismi göster
              </button>
              <br></br>
              <h3>Son alınan sertifika : {certs[certs.length - 1]}</h3>
              <button onClick={()=>setCerts([...certs, "Django"])}>
                  Yeni sertifikayı ekle
              </button>
          </>
      )
  }
  export default Navi;
  ```

- İlgili durumun 'setState' yöntemi, önceki durumu girdi olarak alabilir. Bu durumda, önceki durum değerine göre değişiklik yapmak kolaylaşabilir:
  
  ```jsx
  function Navi{
      let [certs, setCerts] = useState(["React"]);
      const addNewCert = (cert)={
          setCerts((prev)=>[...prev, cert)];
      };
      return(
          <>
              <h3>Son alınan sertifika : {certs[certs.length - 1]}</h3>
              <button onClick={()=>addNewCert("Django")}>
                  Yeni sertifikayı ekle
              </button>
          </>
      );
  }
  export default Navi;
  ```

- ..

> ***NOT :*** Bİr bileşenin durumunu değiştirmek istediğinizde, mevcut durum ('state') üzerinde değişiklik yapmak yerine yeni durumu yeni bir nesne olarak atamanız daha iyi olacaktır. Bu durumda, mevcut durum nesnesi aslında değişmemiş, yeni bir durum nesnesi atanmış olduğundan buna 'immutability' (değişmezlik) denmektedir.
> 
> Immutable (değişmez) bileşen durumunun önemi şunlardır:
> 
> 1. Bir bileşenin durumu değiştiğinde o bileşen ve o bileşen içerisindeki tüm alt bileşenler (veyâ sadece değişen kısım) yeniden çizilir ('render' edilir). Yeni bir 'state' nesnesi oluşturduğunuzda mevcut bileşen ile kıyaslaması ve yeniden çiziliecek yerin tespiti daha kolay olabiliyormuş(?)(react tutorial tic tac tao sayfafasından yeniden teyyit et)
> 
> 2. Durum bileşeninin geçmişini tutmak, önceki duruma dönmek; yeniden sonraki duruma dönmek gibi bir hâfıza yapısı daha kolay bir şekilde kurulabilir

- ..

## REACT BİLEŞENLERİNİN YAŞAM DÖNGÜSÜ

- React'ta önce bileşenler yerleşir; ardından bileşenlerin 'render' yöntemleri çalıştırılır.

- Bileşenlerin yaşam döngüsünde üç durum söz konusudur:
  
  1. Bileşen sayfaya yerleştirilir (mount)
  
  2. Bileşenin herhangi bir durumu değişir
  
  3. Bileşen sayfadan kaldırılır (unmount)

#### 1. Bileşen Sayfaya Yerleştirildiğinde

- Bileşen sayfaya yerleştirildiğinde yapmak istediğimiz şeyler olabilir; misal, verileri bir yerden çekip sayfaya aktarmak istiyor olabiliriz.

- Bileşen sayfaya yerleştirildiğinde `componentDidMount()` yöntemi çalıştırılır. Eğer bileşenimiz sınıf bileşeni ise, sınıf içerisine bu yöntemi ekleyip, bileşen yerleştirildiğinde yapmak istediklerimizi bu yöntem içerisinde kodlayabiliriz:
  
  ```jsx
  export default class SubPage extends Component {
      constructor(props){
          super(props);
      }
      state = {
          title: this.props.title
      };
      componentDidMount(){// Bileşen yerleştiğinde bu fonksiyon çağrılır
          this.setState({ title: "Gelen bilgi : " + this.state.title });
      }
      render(){
          return (
              <>
                  <hr />
                  <h1>{this.state.title}</h1>
              </>
          );
      }
  }
  ```

- Eğer fonksiyon bileşeni kullanıyorsak, bu durumda `useEffect()` yöntemini kullanmalıyız. Bunun için bu fonksiyonu sayfaya eklemeliyiz:
  
  `import {useEffect} from 'react';`

- useEffect fonksiyonunun kullanımı biraz karışık gelebilir. "Bileşen yaşam döngüsü"ndeki üç durum için de bu fonksiyonu kullanıyoruz; fakat farklı şekillerde:

- ```jsx
  import {useEffect} from 'react';
  function Navi(){
      useEffect(()=>{console.log("Bileşen sayfaya bağlandı");}, []);
  }
  ```

- ..

#### 2. Bileşen Durumu Değiştiğinde

- Bu anın yakalanması, diğer bileşen yaşam döngüsü anlarında olduğu gibi sınıfla tanımlanan bileşenler (sınıf bileşenleri, 'class components') ve fonksiyonla tanımlanan bileşenler (fonksiyon bileşenleri, 'function components') arasında farklılık gösterir.

- Fonksiyonla tanımlanan bir bileşenin durumu (veyâ durumunun barındırdığı herhangi bir değişken) değiştiğinde çalıştırmak istediğimiz fonksiyon varsa useEffect fonksiyonuna bir isimsiz fonksiyon vererek bunu sağlayabiliriz. Yapmak istediğimiz şeyler isimsiz fonksiyonun içerisinde yer almalıdır.
  
  ```jsx
  import {useEffect, useState} from 'react';
  function Navi(){
      useEffect(()=>{
          console.log("Bir durum değişikliği saptandı!");
      });
  }
  ```

- Eğer belirli bir durum değişkeni değiştiğinde fonksiyonun çağrılmasını istiyorsak, bu durumda useEffect fonksiyonuna ikinci parametre olarak ilgili durum değişkenini liste içinde vermeliyiz:
  
  ```jsx
  import {useEffect, useState} from 'react';
  function Navi(){
      const [title, setTitle] = useState("Başlık yükleniyor")
      useEffect(()=>{
          console.log("Başlık değişti!");
      }, [title]);
  }
  ```

> ***!NOT :*** useEffect fonksiyonunun ikinci parametresinde verdiğimiz değişkeni, ilk parametreyle verdiğimiz fonksiyon içerisinde değiştiriyorsak, program çıkmaz döngüye girecektir. Çünkü, ikinci parametre ile verilen durum değişkeni her değiştiğinde, ilk parametreyle verilen fonksiyon çalıştırılıyor; ilk fonksiyon içerisinde ilgili değişken değiştirildiğinde fonksiyon yine kendisini çağırdığından uygulama çıkmaz bir döngüye giriyor:
> 
> ```jsx
> function Navi(){
>     const [title, setTitle] = useState("Başlık yükleniyor")
>     useEffect(()=>{
>         console.log("Başlık değişti!");
>         setTitle(title + ".");
>     }, [title]);
> }
> ```
> 
> Yukarıdaki fonksiyon sürekli çalışacağından uygulama çalıştığı sürece 'title' durum değişkeninin sonuna nokta eklenecektir.
> 
> Bu sorunu çözmek için eski durum değerini kullanabiliriz:

- Sınıfla tanımlanan bir bileşenin durumu değiştiğinde çalıştırılmasını istediğimiz kodlar varsa `componentDidUpdate(prevProps, prevState)` fonksiyonunu kullanmalıyız:
  
  ```jsx
  import React, {Component} from 'react';
  export default class Navi extends Component{
      constructor(props){
          super(props);
      }
      state = {
          isVisible: true
      };
      componentDidUpdate(prevProps, prevState){
          console.log("Bileşenin durumu değişti");
      }
      render(){
          return(
              <>
              <button onClick={()=>{isVisible=!isVisible;}}>
                  Detayları göster / gizle
              </button>
              {this.state.isVisible &&
                  <h1>{this.props.details}</h1>
              }
              </>
          )
      }
  }
  ```

- ..

#### 3. Bileşen Sayfadan Kaldırıldığında ('unmount' edildiğinde)

- Fonksiyonla tanımlanan bir bileşen sayfadan kaldırıldığında, bir fonksiyonun çalışmasını istiyorsak bunu `useEffect()` fonksiyonu içerisinde geriye döndürmemiz gerekir:
  
  ```jsx
  function Navi(){
      const [isVisible, setIsVisible] = useState(true);
      useEffect(()=>{
          return ()=>{console.log("Bileşen sayfadan kaldırıldı");}
      });
      return(
          <div>
              {isVisible &&
              <button onClick={setIsVisible(!isVisible);}>
                  Bileşeni göster / gizle
              </button>
          }
          </div>
      )
  }
  ```

- Sınıfla tanımlanan bir bileşen ekrandan kaldırıldığında çalıştırılmasını istediğimiz kodları `componentWillUnmount()` fonksiyonu içerisinde yazmalıyız:
  
  ```jsx
  import React, {Component} from 'react';
  export default class Navi extends Component{
      constructor(props){
          super(props);
      }
      state = {
          isVisible: true
          textOfButton:"";
      };
      componentDidMount(){
          this.state.textOfButton="Detayları gizle"
      }
      componentWillUnmount(){
          this.state.textOfButton = "Detayları göster";
      }
      render(){
          return(
              <>
              <button onClick={()=>{isVisible=!isVisible;}}>
                  Detayları göster / gizle
              </button>
              {this.state.isVisible &&
                  <h1>{this.props.details}</h1>
              }
              </>
          )
      }
  }
  ```

- ..

## React Geliştirici Araçları (react-dev-tools)

- Yüklemek için şu kodu komut ekranında çalıştırabilirsiniz:
  
  `npm install -g react-dev-tools`

## VERİ ÇEKME

- Veri çekme işlemi Javascript içerisinden gelen `fetch()` yöntemiyle yapılabilir.

- Bu yöntemin kullanımı Java'daki Stream gibi peş peşe fonksiyon kullanımını destekler; bu şekilde kullanılabilir:
  
  ```jsx
  import React, {Component} from 'react';
  
  export default class Navi extends Component{
      componentDidMount(){
        fetch("http://localhost:3000/categories")
        .then((response) => response.json())
        .then((data) => this.setState({ categories: data }));
      }
  }
  ```

- Bileşen sayfaya yerleştirildiğinde verileri çekmek için bu ve benzeri kodlar kullanılır.

- `fetch()` fonksiyonuna verinin çekileceği adres girdi olarak verilir.

- Her `then()` yöntemi kendisinden önceki fonksiyonun çıktısını alır.

- Eğer verilerimizin biçimi 'json' ise, json'a çevirmek için `json()` yöntemi kullanılır.

- Verilerin çekilmesi noktasında 'axios' kütüphânesi de kullanılabilir; lüzum yok, çok küçük kolaylıkları var. Misal, JSON verisi çektiğinizde veriyi JSON'a otomatik olarak dönüştürüp, getiriyor. Axios, MIT lisansıyla sunulan açık kaynak bir kütüphânedir.

#### Eşzamânsız (Asenkron) Veri Çekme

- Bir yerden verileri çekme işlemi eşzamânsız (asenkron) bir işlemdir; çünkü verilerin bir HTTP isteğiyle istenmesi ve sonucun elde edilmesi belirsiz bir zamân sonunda bitirilen bir işlemdir ve bu, bağlantı hızına, veri büyüklüğüne bağlı olarak uzun zamân alabilmektedir.

- Veriler çekildikten sonra bir fonksiyonun icrâ edilmesini istiyorsak `fetch()` fonksiyonunun peşine `then()` fonksiyonu ekleyebiliriz; fakat bu ikinci fonksiyon içerisinde de bir veri çekme işlemimiz varsa ve bundan sonra icrâ edilmesini istediğimiz bir fonksiyon varsa bu durumda bunu `then()` içerisinde `fetch()` ve `then()` olarak yine kodlamak durumunda kalıyoruz. Bundan kurtulmak için eşzamânsız bekleme özelliğini kullanabiliriz.

- Eşzamânsız bekleme özelliği bir fonksiyonun icrâsında kullanılacak parametrelerin belli olması için bir verinin gelmesini beklediğimiz durumlarda kullanışlı olabilir.

- Bunun için fonksiyonu eşzamânsız (asenkron) olarak işâretlemeliyiz. Bunun için fonksiyonun başına `async` anahtar kelîmesi yazılır. Daha sonra fonksiyon içerisinde veriyi beklediğimiz satırdaki fonksiyonun başına `await` anahtar kelîmesini yazmalıyız. Böylece, ilgili fonksiyon bitmeden program bir alt satıra geçmeyecektir:
  
  ```jsx
  const getData = async()=>{
      const url = "http://localhost:3000/categories";
      let categories = [];
      await fetch(url).then((res)=>res.json)
      .then((data) => categories=data);
      secondUrl = url + "/" + categories[0]
      const productsInCategories = fetch(secondUrl);
  }
  ```

- Eşzamânsız fonksiyonları kullanırken `try{}catch(){}` kod blokları kullanılabilir.

## REACT YÖNLENDİRME (REACT ROUTER)

#### Giriş ve React 'Route' Bileşeni

- Yönlendirme, web sitelerinde çok kullanılan bir özelliktir.

- React yönlendirme için 'react-router-dom' isimli bir kütüphâne sunmaktadır.

- React, mobil uygulamalar için de kullanılabilir olduğu için 'react-router' React ile berâber gelmemektedir.

- Kütüphâneyi 'package.json' dosyası içerisindeki 'dependencies' listesine eklemek veyâ `npm install react-router-dom` komutunu proje dizinimizde açtığımız komut satırında çalıştırmak kâfîdir

- React Router ile ilgili bilmemiz gereken ilk şey gelen bağlantı adresine göre kullanıcıya hangi React bileşenlerini göstermemiz gerektiğini seçen sistemdir. Bunun için 'Route' bileşeni kullanılır.

- `<Routes></Routes>` içerisinde `<Route></Route>` şeklinde yönlendirmeler bulunur ve bu yönlendirmeler `<BrowserRouter></BrowserRouter>` etiketleri arasında bulunur:

- Yönlendirme, sayfanın değişken olduğu kısımlara konularak diğer kısımların tüm sayfalarda geçerli olması sağlanabilir.

- Emsal bir yönlendirme:
  
  ```jsx
  import React, {Component} from 'react';
  import {BrowserRouter, Routes, Route} from 'react-router-dom';
  
  export default class App extends Component{
      render(){
      return(
          <BrowserRouter>
              <Routes>
                  <Route index element={<Home/}></Route>
                  <Route path="home" element={<Home/}></Route>
                  <Route path="articles" element={<Articles/}></Route>
                  <Route path="contact" element={<Contact/}></Route>
                  <Route path="articles" element={<Home/}></Route>
              <Routes>
          </BrowserRouter>
      )}
  }
  ```

- 'path' özelliği karşılık gelen bağlantı adresini belirtmek için kullanılır.

- 'element' özelliği ise ilgili 'path' değerine karşılık gelen bileşeni belirtmek içindir.

- 'element' yerine 'component' özelliğini de kullanabilirsiniz.

- 'index' özelliği varsayılan sayfa olduğunu belirtmek içindir. Yanî;
  index = path("/")

- İstenilirse, `<BrowserRouter></BrowserRouter>` etiketleri 'index.js' dosyasındaki `<App/>` ifâdesini çerveleyecek şekilde yazılabilir. Bu durumda yönlendirmeyi sayfa içinde şu şekilde kullanabiliriz:
  
  ```jsx
  import React, {Component} from 'react';
  import {Switch, Routes, Route} from 'react-router-dom';
  
  export default class App extends Component{
      render(){
      return(
           <Routes>
              <Route index element={<Home/}></Route>
              <Route path="home" element={<Home/}></Route>
              <Route path="articles" element={<Articles/}></Route>
              <Route path="contact" element={<Contact/}></Route>
              <Route path="articles" element={<Home/}></Route>
          <Routes>
      )}
  }
  ```

- Her iki şekilde de gelen bağlantı adresine göre yönlendirme işlemi yukarıdan aşağıya doğru ilk eşleşen `<Route>` bileşenini uygulayacak şekilde çalışır.

- Bir alt bağlantı adresi yakalandıktan sonra, bağlantı adresimiz yeniden dallanıyorsa bu durumda o dalları yakalanan `<Route>` içerisinde yazmalıyız:
  
  ```jsx
  <Routes>
      <Route path="articles" element={<Articles/}>
          <Route path="" element={<ArticleDetails/}></Route>
      </Route>
  <Routes>
  ```

- Yönlendirme yaparken olası bir hatâlı yazımdan ötürü bir link eşleşmesi gereken `<Route/>` bileşeninden önce olan başka bir `<Route/>` bileşeniyle eşleşebilir. Bunun önüne geçmek için 'exact' özelliğini kullanabiliriz:
  
  ```jsx
  <Routes>
      <Route exact path="articles" element={<Articles/>}></Route>
          <Route path="articles/details" element={<ArticleDetails/>}>
      </Route>
  <Routes>
  ```

- Yukarıdaki yönlendirme sistemine sâhip bir uygulamaya 'articles/details' adresi geldiğinde ikinci yönlendirme çalıştırılır; eğer ilk `<Route/>` bileşenine 'exact' özelliğini vermeseydik ilk yönlendirme çalışırdı (?).

- Gelen bağlantıyı parametrelendirmek için (bağlantıyı bölerek, parametreye atamak için) ilgili yere iki nokta işâretinden sonra parametre ismi yazılır:
  
  ```jsx
  <Routes>
      <Route exact path="articles/:id" element={<Articles/>}/>
  </Routes>
  ```

- Yukarıdaki bağlantı yönlendirmesine sâhip uygulamaya 'articles/1' bağlantı adresiyle bir istek gelirse `<Articles/>` bileşeni içerisinde bu parametre 'id' ismiyle alınabilir

> ***NOT :*** React Router 5. versiyonda `<Route/>` bileşeninin 'element' anahtar kelîmesi yerine 'component' anahtar kelîmesini kullanmalıyız ve yalnızca bileşen ismini yazmalıyız:
> 
>  `<Route exact path="articles/:id" component={Articles}/>`

- React Router 5. versiyonda sayfa bulunamaması durumunu kontrol altına almak için en alta 'path' özelliğine bir değer atamadığımız bir `<Route/>` koymalıyız:
  
  ```jsx
  <Routes>
      <Route exact path="articles/:id" component={ArticleDetails}/>
      <Route exact path="reports/:id" component={ReporDetails}/>
      <Route component={NotFound}/>
  </Routes>
  ```

- Yukarıdaki koddaki son yönlendirme bileşeninin React Router 6. versiyondaki karşılığı şudur:
  
  ```jsx
  <Route path="*" element={<NotFound/>}/>
  ```

- ..

#### React 'Link' Bileşeni ve 'useNavigate' Fonksiyonu

- React'ta sayfa yönlendirmek için React `<Link/>` bileşenini veyâ `useNavigate()` fonksiyonunu kullanabiliriz. `useNavigate()` fonksiyonu, fonksiyonla tanımlanmış bileşenlerde kullanılabilir.

- React, 'Tek Sayfa Uygulaması' (SPA (Single Page Application)) olduğundan yönlendirmelerde sayfanın yenilenmesi durumunda bileşenlerin durumları ('states') ve bileşenlere daha önce gönderilmiş olan özellikler ('props') kaybolur. Bunun olmaması için React Router da sayfayı yenilemeden yönlendirme işlemi yapar. Bu, kullanıcı deneyimini ve performansını da arttırmaktadır.

- Sayfa yönlendirme linki oluşturmak için yine 'react-router-dom' altındaki `Link` bileşeni kullanılabiliriz. Gitmek istediğimiz adresi belirtmek için 'to' özelliğini kullanın:
  
  ```jsx
  <Link to="/">Anasayfa</Link>
  ```

- Bir başka yöntem de `useNavigate()` fonksiyonunu kullanmaktır:
  
  ```jsx
  import 'useNavigate' from 'react-router-dom';
  
  function App{
      const navigate = useNavigate();
      return(
          <button onClick={()=>{navigate("/");}}></button>
      );
  }
  export default App;
  ```

- `useNavigate()` kullanarak sayfalar arasında sıra tâkibi yapabiliriz. Misal, `useNavigate(-1);` fonksiyonu sizi önceki sayfaya götürür.

> ***NOT :*** Eğer sayfanın yenilenerek yönlendirilmesini istiyorsak, HTML'de bulunan `<a/>` etiketini kullanabiliriz.

- Link ile veri gönderme de React Router 5. versiyon ile React Router 6. versiyon arasında fark göstermektedir.
  Bu işlemin React Router 6. versiyonda nasıl yapıldığını öğrenmek için ilk koda bakınız; bu kodun React Router 5. versiyondaki karşılığını görmek için ise bir alttakine bakınız:
  
  ```jsx
  <Link to"articles" state={{articleReview : 17}}></Link>
  {/*Yukarıdaki kodun React Router 5. versiyondaki karşılığı şudur:*/}
  <Link to={{pathname:"articles", state:{articleReview : 17}}}></Link>
  ```

> ***NOT :*** Buradaki 'state' isminin özel bir anlamı yok; değiştirilebilir.

- ..

#### Gelen Adres Bilgisini Ele Geçirmek

- React Router'un fonksiyonla tanımlanmış bileşenleri için gelen adres bilgisini almak oldukça kolaydır.

- Bunun için `useParams()` fonksiyonu kullanılır. Fonksiyon parametreleri bir nesne biçiminde, anahtar - değer çifti şeklinde döndürür. Bunun için fonksiyonu sayfaya ekleyin ve fonksiyonu fonksiyonla tanımlanmış bileşenin başında çağırın:
  
  ```jsx
  import {useParams} from 'react-router-dom';
  
  function App(){
      const params = useParams();
      console.log(params);
  }
  ```

- Sınıfla tanımlanmış bileşenlerde bağlantı adresindeki parametreyi almak da zor değildir. Bunun için 'react-router-dom' altındaki `withRouter(sinifBilesenIsmi)` fonksiyonu sınıfla tanımlanan bileşenin altında çalıştırılmalı. Böyle yaptığımızda ilgili parametreler bileşene 'props' ile gönderilir. Gönderilen parametreleri alabilmek için `this.props.match.params` nesnesini kullanın.
  
  ```jsx
  import React, {Component} from 'react';
  import {Switch, Routes, Route} from 'react-router';
  
  class Articles extends Component{
      constructor(props){
          super(props);
      }
      writeParams = ()=>{console.log(this.props.params);};
      render(){
      return(
          <>
              <button onClick={()=>writeParams();}>Parametreleri göster
              </button>
          </>
      )}
  }
  export default Articles;
  withRouter(Articles);
  ```

- React Router v5'te bağlantı adresindeki soru işâretinden sonra gelen parametreler 'arama' parametresi olarak geçmektedir. Bunların hâricinde ve uygulama ana dizini hâricinde kalan adrese ulaşmak için yukarıdaki yöntemi kullandıktan sonra gelen `this.props.location.pathname` metnini kullanabilirsiniz. Öte yandan 'arama' şeklinde ifâde edilen kısmı almak için `this.props.location.search` metnini kullanabilirsiniz.

> ***NOT :*** Yukarıdaki kodda kullanılan 'withRouter' React Router v6 ile kitâplıktan çıkarıldığından ötürü 'withRouter' fonksiyonu en son React Router v5 ile çalışmaktadır. Bunun için proje dizininde komut satırı açarak şu kodu çalıştırın:
> 
> `npm install -s react-router-dom@5`
> 
> Fakat React Router 5. versiyonu kullandığınızda, `<Routes/>` bileşenini bulamazsınız; bunun yerine `<Switch>` bileşenini kullanınız.
> 
> Bir başka uyuşmazlık da React Router 5. versiyonunda, `<Route/>` tanımlarken 'element' özelliği yerine 'component' özelliğini kullanmalı ve eşitliğin karşı tarafına sadece bileşenin ismini süslü parantez içerisinde yazmalısınız. Aşağıdaki React Router 5. versiyon için geçerli olan kodun karşılığı bir altındadır
> 
> ```jsx
> <Switch>
>     <Route exact path="articles/:id" component={Articles}/>
> </Switch>
> // Yukarıdaki kodun React Router v6'daki karşılığı:
> <Routes>
>     <Route exact path="articles/:id" element={<Articles/>}/>
> </Routes>
> ```

- ..

#### Gönderilen Veriyi İlgili Bileşende Ele Geçirmek

- `<Link>` ile veyâ `useNavigate` ile gönderilen veriyi ele geçirmek konusu sınıfla tanımlanan bileşenler ileve fonksiyonla tanımlanan bileşenler arasında farklık göstermektedir.

- Fonksiyonla tanımlanan bileşenler için 'react-router-dom' altındaki 'useLocation' 'hook' fonksiyonu kullanılmalıdır:
  
  ```jsx
  import {useLocation} from 'react-router-dom';
  function Article(){
      const data = useLocation();
      return(
          <>
              <h3><pre>{JSON.stringify(data)}</pre></h3>
          </>
      );
  }
  export default Article;
  ```

- Sınıfla tanımlanan bileşenlerde bu verinin ele geçirilmesi için aynı bağlantı adresi bilgisinin ele geçirilmesinde olduğu gibidir. İlgili veri sınıf içerisinde aldığımız 'props' nesnesinin altındaki 'location' nesnesi içerisindedir.

## İŞLEME ('RENDER') OPTİMİZASYONU ve REACT MEMO

- React'te bir bileşendeki herhangi bir değişkenin değeri değiştiğinde bileşen yeniden işlenmez ('render' edilmez). Fonksiyonla tanımlanmış bileşenlerdeki değişkenlerin yalnızca `useState()` ile tanımlananları değiştiğinde sayfa yeniden işlenir; sınıf ile tanımlanan bileşenlerdeki değişkenlerin yalnızca 'state' nesnesi içinde olanlar yalnızca `setState()` yöntemiyle değiştirildiğinde sayfa yeniden işlenir.

- Bir bileşenin durumu değiştiğinde sayfa ve o sayfa altındaki tüm bileşenler yeniden işlenir. Bu, pek çok kez istenmeyen bir durum olabilir. Misal, bir haber sitesi için yukarıdaki yeni gelen haberleri gösteren sayının değişmesi, bütün sayfanın yeniden işlenmesine sebep olduğundan çok verimsiz bir iş yapılmış olur.

- Bunun önüne geçebilmek için, alt bileşenleri dışarı çıkartırken `React.memo()` bileşeniyle sarmalamalıyız (parametre olarak vermeliyiz):
  
  ```jsx
  import React, {Component} from 'react';
  
  class Article extends Component{/*...*/}
  export default React.memo(Article);
  ```

- Sayfaya eklediğimiz bileşeni `React.memo` bileşeniyle sarmaladığımızda, herhangi bir durum değişikliğinde `React.memo` ile sarmalanan bileşenin değişip, değişmediği kontrol edilir ve sadece değiştiğinde o bileşen yeniden işlenir.

- Yukarıdaki yöntemi uyguladığımızda tüm performans sorunları çözülmüyor. Bir bileşenin bir durumu değişse ve değişen bu durum değişkeni alt bileşene gönderilmişse alt bileşenin ekran görüntüsünü değiştirmese bile alt bileşen yeniden işlenir ('render' edilir). Hattâ içteki bu bileşen bu durum değişkenini hiç kullanmasa bile alt durum yeniden işlenir.

- `React.memo` bileşeni ile nesneyi sarmaladığımızda **fonksiyon ile tanımlanan bileşenler için** devâm eden bir başka sorun ise şudur: Eğer bileşenin alt bileşene gönderilen parametresi nesne tipinde ise, bu durumda bu nesne hiçbir yerde değişmese, alt bileşene gönderilmeyen bir durum değişkeni değişse bile alt bileşen yeniden işlenir. Bunun sebebi ise, alt bileşene gönderilen 'props' ile mevcut değişkenlerin karşılaştırılması sonucunda bir değişiklik olduğu saptanır; çünkü alt bileşene gönderilen değişkenin tipi nesne olduğundan ve nesne yeniden oluşturulduğunda referansı değiştiğinden ötürü React alt bileşene gönderilen 'props' parametresinin değiştiği algılar. Eğer bu değişken referans tipli değil de, değer tipli bir değişken olsaydı (string, number gibi) alt bileşenin yeniden çizilmesini önlemek için alt bileşenin `React.memo` ile sarmalanarak dışarı aktarılması kâfî gelirdi.

- Yukarıdaki bahsedilen sorunun yalnızca fonksiyonla tanımlanan bileşenler için geçerli olduğuna dikkat edelim.

- Bu sorunun birkaç çözümü vardır. En basit hâliyle, nesne tanımını sayfa içerisinde, fakat fonksiyon dışarısında yaparsak, bu durumda mevcut sayfa yeniden işlendiğinde (fonksiyon yeniden çalıştırıldığında) nesnenin referansı değişmeyeceğinden ve alt bileşen `React.memo` ile sarmalandığından alt bileşen yeniden çizilmez.

- Eğer bu nesneyi fonksiyon içinde tanımlamamız gerekiyorsa, bu durumda `useMemo` isimli 'hook' yapısını kullanmalıyız; ilgili fonksiyonu bu fonksiyon içerisinde, birinci parametre olan fonksiyonun içinde geri döndürmeliyiz:
  
  ```jsx
  import {useMemo} from 'react';
  function App(){
      const articleInfo = useMemo(
          ()=>{
              return {
                  articleName : "Uygur zulmü",
                  pageNumber : "11",
              };
          }, []
      );
      return(
          <>
              {/*...*/}
              <Article articleInfo={articleInfo}>
          </>
      );
  }
  ```

- Bu 'hook'un kullanımı da `useEffect` 'hook'una benzemektedir. `useMemo()` fonksiyonunun dizi şeklindeki ikinci parametresini vermezseniz alt bileşen yine çizilir.

- Fonksiyonla tanımlanan bileşenlerdeki benzer bir diğer sorun ise referans tipli olan bir başka değişken olan fonksiyonun alt bileşene gönderilmesi ve mevcut sayfa yeniden çizildiğinde alt bileşenin görüntüsü değişmemesine rağmen yeniden çizilmesi. Bu sorunun oluştuğu bir ortam aşağıdaki gibidir:
  
  ```jsx
  import {useState} from 'react';
  function App(){
      const [clickedNumber, setClicked] = useState(2);
      const articleInfo = ()=>{/*...*/};
      return(
          <>
              <h3>Tıklanma sayısı : {clickedNumber}</h3>
              <br/>
              <button onClick={()=>{setClicked((prev)=>{prev+1;});}}>
                  Tıklanma sayısını arttır
              </button>
              <Article articleInfo={articleInfo}>
          </>
      );
  }
  ```

- Yukarıdaki bileşende düğmeye tıkladığınızda alt bileşene giden fonksiyon tipli değişkenin referansı değiştiğinden ötürü alt bileşen yeniden çizilir. Bu sorunun çözümü ise şudur:
  
  ```jsx
  import {useState, useCallback} from 'react';
  function App(){
      const [clickedNumber, setClicked] = useState(2);
      const articleInfo = useCallback(()=>{/*...*/}, []};
      return(
          <>
              <h3>Tıklanma sayısı : {clickedNumber}</h3>
              <br/>
              <button onClick={()=>{setClicked((prev)=>{prev+1;});}}>
                  Tıklanma sayısını arttır
              </button>
              <Article articleInfo={articleInfo}>
          </>
      );
  }
  ```

> ***NOT :*** Yukarıdaki kodun yetersiz çözüm olduğu bir durum vardır; o da şudur: Eğer 'articleInfo' fonksiyonu içerisinde bir durum güncellemesi yapıyorsanız ve durumu değiştirme fonksiyonunu kullanırken ('setClicked' gibi) durum değişkenini doğrudan kullanıyorsanız, durum değişkeni her seferinde değiştiğinden fonksiyonun referansı da her seferinde değişir ve alt bileşen yeniden çizilir. Bu sorunun oluşmaması için durum güncelleme fonksiyonunda durum değişkenini doğrudan kullanmayın; eğer bu değişkenin değerine ihtiyacınız varsa aynı fonksiyona girdi olarak verilen eski durum değerini kullanın. Misal,
> `setClicked(clicked+1);` yerine
> `setClicked((prev)=>{prev+1;});`  fonksiyonunu kullanın.

- ..

## REACT'TA KAPSAMLI DURUM (STATE) YÖNETİMİ

- Daha evvel de değinildiği üzere React'ta şu kısıtlar vardır:
  
  1. Bir bileşenden aynı ağaç rotası üzerinde olmayan başka bir bileşene veri taşıyamazsınız
  
  2. Bir bileşenden, onu kapsayan üst bileşenlere veri taşıyamazsınız
  
  3. Ağaç hiyerarşisinde kendisinden iki aşağıda olan alt bileşene doğrudan veri taşıyamazsınız

- React'ta yalnızca bir alt bileşene, yanî bileşenin içindeki bileşene (birinci seviye için) veri taşıyabilirsiniz. Misal, 'Anasayfa' bileşeninizden 'Anasayfa'da gösterilen 'Bildirimler' bileşenine veri taşıyabilirsiniz, fakat 'Bildirimler' bileşeninin içinde yer alan 'Bildirim' bileşenine veri taşıyamazsınız.

- Bu sebeple React'ta durum yönetimi için çeşitli kitâplıklar ve araçlar kullanılmaktadır; bu sorunun çözümü için React içerisinde de bir kütüphâne var. 

- ..

#### Context API

- Context, bağlam demektir. Birden fazla bileşenden aynı duruma erişmek için kullanılan, React içerisinde dâhilî olarak gelen Context API, bize bir bileşenden tüm alt bileşenlere veri gönderebilmeyi sağlayan bir kütüphânedir.

- En basit ifâdeyle, bir bileşeni bir 'Provider' ile sarmalayıp, tüm alt bileşenlerin o bileşendeki veriye erişmesini sağlayan bir yapı sağlıyor.

- Bunun için 'react' içerisinden gelen 'createContext' yapısını kullanmamız gerekiyor. Genel durum bilgilerini ifâde eden bu bağlam bilgilerini ayrı dosyada tanımlamamız daha iyi olur; öncelikle bağlam bilgisi ayrı bir dosyada tanımlayıp, dışarı aktarılım:
  
  ```jsx
  import {createContext} from 'react';
  
  const GuiContext = createContext("dark");
  {/*'dark' varsayılan değerdir, istenilirse burası boş bırakılabilir*/}
  export default GuiContext;
  ```

- Daha sonra bu bağlam bileşenini uygulamamıza ekleyelim ve uygulamamız içerisindeki bileşenleri bu bağlam bileşeninin elemanı olan sağlayıcıyla ('Provider') şu şekilde sarmalayalım:
  
  ```jsx
  import GuiContext from '../contexts/GuiContext';
  import React, {Component} from 'react';
  export default class App extends Component{
      render(){
          return(
              <div>
                  <GuiContext.Provider value="lightblue">
                      <Navi/>
                      <Home/>
                  </GuiContext.Provider>
              </div>
          );
      }
  }
  ```

- `<Navi/>` ve `<Home/>` bileşenlerinin içerisinde bu bağlam bilgisine nasıl erişiriz?

- Eğer bu bileşenler fonksiyonla tanımlanmış bileşenler ise `useContext()` 'hook' fonksiyonu kullanarak bunlara erişilebilir. Bunun için ilgili bağlam bilgisini tanımladığımız dosyayı da sayfaya eklemeliyiz:
  
  ```jsx
  import {useContext} from 'react';
  import GuiContext from '../contexts/GuiContext';
  function Navi(){
      const guiData = useContext(GuiContext);
      console.log(guiData);
      return({/*...*/});
  }
  ```

- Eğer bu alt bileşenler sınıfla tanımlanan bileşenler ise, ilgili bağlam bilgisine şu şekilde erişilir:
  
  ```jsx
  import React, {Component} from 'react';
  import GuiContext from '../contexts/GuiContext';
  class Home extends Component{
      static contextType = GuiContext;
      componentDidMount(){
          console.log(this.context);
      }
      render(){return({/**/});}
  }
  export default Home;
  ```

- Yanî sınıf içerisine en başa static `contextType = GuiContext;` kodunu eklediğimizde sınıf içerisinden `this.context` bağlam bilgisine erişebiliriz.

- Birden fazla bağlam bilgisi eklendiğinde ise fonksiyonla tanımlanan bileşenlerde bunları almak çok kolaydır:
  
  ```jsx
  import GuiContext from "../contexts/GuiContext";
  import LanguageContext from "../contexts/LanguageContext";
  import {useContext} from 'react';
  
  function App(){
      const guiContext = useContext(GuiContext);
      const langContext = useContext(LanguageContext);
  }
  ```

- Fakat sınıfla tanımlanan bileşenlerde birden fazla durum bilgisini almak çok daha karmaşıktır. İki şekilde değerlendirebiliriz. Eğer bu bağlam bilgilerine `render()` fonksiyonu içerisinde ihtiyaç duyuyorsanız şu kodlama örüntüsüyle bunlara erişebilirsiniz (bağlam dosyalarını `import` ile eklemeyi unutmayın):
  
  ```jsx
  render(){
      return(
          <>
              <LanguageContext.Consumer>
              {(languageContext) => (
                  <GuiContext.Consumer>
                  {(guiContext) =>
                      (<h3> guiContext= {guiContext}
                      languageContext={languageContext}
                      </h3>)}
                  </GuiContext.Consumer>
              )}        
             </LanguageContext.Consumer>
          </>
      )
  }
  ```

- Aslında her bir bağlam için `<ContextFirst.Consumer>` etiketi açıyoruz ve bunları iç içe koyuyoruz. Etiket açıldığında bir Javascript fonksiyonu yazıyor gibi davranıp, ilgili bağlamı girdi olarak alıyoruz.

- Eğer birden fazla bağlam bilgisine sınıf içerisinde ihtiyacımız varsa, bu durumda uygulamamız gereken yöntem biraz daha karmaşıktır. En öz hâliyle bir fonksiyon oluşturup, bileşeni bu fonksiyona verip, dışarı aktarmak gerekir. Böylece sınıf içerisinden ilgili bağlam bilgilerine ulaşılabilir. Kodlama örüntüsü şöyledir (kod çalışıyor, ama istenen sonuç alınmıyor, kontrol edilecek):
  
  ```jsx
  import GuiContext from "../contexts/GuiContext";
  import LanguageContext from "../contexts/LanguageContext";
  import React, {Component} from 'react';
  export const withContextBag = (Component)=>(
      (props)=>{
          <LanguageContext.Consumer>
          {(lang)=>
              <GuiContext.Consumer>
              {(gui)=>
                  <Component lang={lang} gui = {gui}{...props}/>
              }
              </GuiContext.Consumer>
          }
          </LanguageContext.Consumer>
      }  
  );
  class Home extends Component{
      constructor(props){
          super(props);
      }
  }
  export default withContextBag(Home);
  ```

- Ezcümle Context API fonksiyon tanımlanan bileşenler için uygundur. Context API kullanımını iyileştirmek için bağlam bilgilerimiz bağlamı tanımladığımız dosyaya alınabiliriz! Fakat dikkat etmemiz gereken şeyler var. Öncelikle yeni bağlam tanım dosyamıza bakalım:
  
  ```jsx
  import {createContext, useState} from 'react';
  const GuiContext = createContext();
  export const GuiContextProvider = ({children})=>{
      const [guiColor, setGuiColor] = useState("dark");
      const values = {
          guiColor,
          setGuiColor
      };
      return(
          <GuiContext.Provider value={values}>{children}
          </GuiContext.Provider>
      );
  };
  export default GuiContext;
  ```

- Bu örüntüyle tanımladığımız bağlamı kod içerisinde rahat bir şekilde kullanabiliriz:
  
  ```jsx
  import {GuiContextProvider} from "../contexts/GuiContext";
  
  function App(){
      const data = useContext(GuiContext);
      console.log(data);
      return(
          <>
              <GuiContextProvider>
                  <h3>Görünüm rengi : {data.guiColor}</h3>
                  <button onClick={()=>data.setGuiColor("light")}>
                      Görünüm rengini değiştir
                  </button>
              </GuiContextProvider>
          </>
      );
  }
  export default App;
  ```

- Bağlam tanımında yaptığımız değişiklikle `<GuiContext.Provider>` içerisinde yer alan alt bileşenleri alıp, `GuiContextProvider` olarak paketleyip, dışarı aktardık. Buradaki isim bize bağlı bir şey; başka isim de seçilebilir. `GuiContextProvider` bileşeninin süslü parantez içinde olduğuna dikkat ediniz. Bunun sebebi onu `export default` olarak dışarıya çıkarmıyor oluşumuzdur, bunun sebebi de sayfada yalnızca bir tâne nesneyi `default` anahtar kelîmesiyle dışarı çıkarabiliyor oluşumuzdur.

#### Durum İdâre Aracı :  Redux

- Redux durumları tek bir yerden idâre etmek için kullanılan bir kütüphânedir.

- Redux React'a özgü bir kütüphâne değildir; React içerisinde Redux'u rahatça kullanmak için 'react-redux' isimli bir paket daha vardır.

- Bir bileşen durum bilgisi almak istediği zamân Redux'un 'Store' olarak isimlendirdiği yerden bunu kendi bileşeninin 'props' girdisine bağlanmış olarak alabilir.

- Redux'u eklemek için proje dizininde komut satırında `npm install redux` komutunu çalıştırın. Ardından `npm install react-redux` komutunu çalıştırın.

- Redux'taki yapıların açıklaması:
  
  1. 'actionTypes' dosyası bizim eylemlerimizin isimlerini tanımladığımız yer.
  
  2. Her bir durum değişken için, o değişkeni değiştiren eylemleri tanımladığımız birer 'action' dosyası olmalıdır: 'likedActions.js', 'postActions.js' gibi... Bu dosya içerisinde her eylem için eylemin tipini ve eylemin parametresini girdi olarak verdiğimiz bir fonksiyon oluşturuyoruz; bu fonksiyonu da bir fonksiyona eşitliyoruz (daha açıklayıcı yaz).
  
  3. Her bir eylem için o eylemler geldiğinde durum değişkeni üzerinde gerekli değişikliği yapacak birer 'reducer' olmalıdır. 'reducer' yapısı gelen eyleme bakarak değişiklik yapıyor. Yanî durum üzerinde esas değişiklik yapılan yer burasıdır.
  
  4. Tüm 'reducer' yapılarını bir yerde toplamak ve kolay erişmek için 'combineReducers' yapısı vardır. Düzenli olması açısından bunu 'reducers' dizini içinde 'index.js' dosyasında yapmalıyız.
  
  5. 'reducer' yapılarını tutan, duru

- ..

- Daha düzgün bir proje yapısı için proje dizininde 'redux' dizini oluşturun; bu dizin altında 'actions', 'reducers' dizinlerini oluşturun. 'actions' dizini altında 'actionTypes.js' dosyası oluşturun. Bu dosya eylem isimlerini elle yazarak hatâ yapmak yerine buradan seçerek daha düzgün şekilde yapılandırmak içindir; yanî 'actionTypes' dosyası yalnızca eylemlerin isimlerini yine eylem ismi ile aynu isimde değişken olarak saklayan bir dosyadır (eylem ismi ile aynı isimde olmak zorunda değil; fakat böyle olması çok iyidir). Emsal bir 'actionTypes.js' dosyası şu şekildedir:
  
  ```js
  export const INCREASE_LIKED = "INCREASE_LIKED";
  export const DECREASE_LIKED = "DECREASE_LIKED";
  ```

- Daha sonra hangi aksiyon hangi durum değişkeni için ise bunun için bir dosya oluşturuyoruz. Yukarıdaki eylemler için 'likedActions.js' ismiyle oluşturabiliriz. Emsal bir aksiyon dosyası şöyledir:
  
  ```js
  import * as actionTypes from 'actionTypes';
  
  export const increaseLiked = () =>({
      type : actionTypes.INCREASE_LIKED,
      payload : 1
  })
  
  export const increaseLiked = ()=>({
      type : actionTypes.DECREASE_LIKED,
      payload : 1
  })
  ```

- Yukarıda tanımladığımız 'increaseLiked' değişkeni bir fonksiyondur. O fonksiyonun değeri de bir fonksiyondur. Yanî fonksiyon içerisinde fonksiyon olmuş oluyor. Bu iç fonksiyonun parametresi bir nesnedir. Bu nesne içerisinde eylemin tipi belirtilir, eylemin durum üzerindeki değişikliğini belirtmek için eylemin değeri veyâ başka deyişle eylemi çalıştırırken verilen parametre belirtilir (örnekte 'payload' özelliği bunu ifâde ediyor).

- 'reducers' dizini altında bu eylemleri kontrol eden, uygulayan bir 'reducer' (eylem uygulayıcısı) tanımlayalım. Emsal bir dosya şu şekildedir:
  
  ```js
  import * as actionTypes from 'actionTypes';
  /*durumun başlangıç değeri sıfırdır*/
  const likedReducer = (state=0, action)=>{
      switc(action.type){
          case actionTypes.INCREASE_LIKED:
              return (newState = state + action.payload);
          case actionTypes.DECREASE_LIKED:
              return (newState = state - action.payload);
          default state;/*Eğer eylem için bir şey yapılmayacaksa
                          mevcut durum değişkenini olduğu gibi döndür*/
      }
  };
  export default likedReducer;
  ```

- 'reducer' yapısı gelen eyleme göre, durumu geri döndürür. Bu fonksiyonda ('reducer'da) gelen eyleme göre işlem yapılacağı için 'switch-case' yapısı kullanmak uygundur.

> ***NOT :*** 'reducer' fonksiyonunda mevcut durum değişkenini değiştirip döndürmedik; çünkü mevcut durum değişkeninin referansının değişmesi Javascript immutability açısından daha uygun görülmüştür. Böylece durum değişkeninin önceki versiyonlarını depolayarak geçmişi hâtırlayan bir yapı inşâ edebiliriz. Ayrıca ilginç şekilde bunun performansı iyileştirebileceği söyleniyor.

- Tüm 'reducer' fonksiyonlarımızı birleştirmek için 'reducers' dizini altında 'index.js' dosyası oluşturalım. Emsal bir dosya şu şekildedir:
  
  ```js
  import {combineReducers} from 'redux';
  import likedReducer from './likedReducer';
  
  const reducers = combineReducers({
      likedReducer : likedReducer
      /*Yukarıdaki satırı kısaca likedReducer şeklinde de yazabilirdik*/
  });
  ```

- Öncelikle 'reducers' dizini altında 'configureStore' isimli bir mağaza oluşturalım. Bu, durumların depolandığı ve React uygulamasına aktarıldığı yerdir. İçeriği şöyledir:
  
  ```jsx
  import {createStore} from 'redux';
  import reducers from './index';
  
  export default function configureStore(){
      return createStore(reducers);
  }
  ```

- Redux'ı React uygulamamıza entegre etmek için bâzı kodlar yazmamız gerekiyor. Öncelikle ana uygulama dosyamız olan 'App.js' dosyasında uygulamamızı 'Provider' bileşeniyle sarmalayalım, ardından tüm durum değişkenlerimize erişmek için kullanacağımız mağazamızı oluşturalım ve mağazamızı bu sağlayıcı bileşene 'props' olarak verelim:
  
  ```jsx
  import {Provider} from 'react-redux';
  import configureStore from './redux/configureStore';
  /*...*/
      const store = configureStore();
      reactDOM.render(<Provider store = {store}><App/></Provider>,
              document.getElementById('root'));
  /*...*/
  ```

- Mağazamızı kullanmak istediğimiz sınıfta 'react-redux'tan gelen 'connect' yöntemini kullanmalıyız:
  
  ```jsx
  import {connect} from 'react-redux';
  import React, {Component};
  class Likes extends Component{
      render(){
          return(
              <h3>Beğeni sayısı : {this.props.likes}</h3>
          );
      }
  }
  function mapStateToProps(state){
      return {likes : state.likedReducer};
  }
  export default connect(mapStateToProps)(Likes);
  ```

- Bir eylemi bir bileşene bağlamak için şu kodlar yazılır:
  
  ```jsx
  import {increaseLiked} from '../redux/actions/likedActions';
  import React, {Component};
  class LikeButton extends Component{
      render(){
          return(
              <button onClick={(event)=>{
                  this.props.dispatch(increaseLiked()}>
                  Beğen
              </button>
          );
      }
  }
  
  function mapDispatchToProps(dispatch){
      return {actions:bindActionCreators(increaseLiked, dispatch)}
  }
  export default connect(mapDispatchToProps)()
  ```

- ..

## YEREL DEPOLAMA ve VERİTABANI

#### Kolay ve Basit Depolama :  Tarayıcı Üzerinde Yerel Depolama

- Kullanıcının tercihleri gibi bilgiler sayfa yenilense bile kaybolmamalıdır. Misal, kullanıcı websitesine her girdiğinde  web sitesinin görünüm rengini veyâ dilini veyâ başka özelleştirilebilir bir ayarı belirleme zahmetini çekmemelidir. Bunun için kullanabileceğimiz en basit ve en kolay yöntemlerden birisi bu bilgiyi tarayıcının yerel depolamasına yazmaktır.

- Tarayıcının yerel depolamasına bilgi yazmak ve buradan bilgi okumak kolaydır. Bunun için bir ekleme işlemine gerek yoktur. Yazmak istediğimiz değerleri anahtar - değer çifti olarak yazıyoruz. İlk satır yazma işlemi, ikinci satır ise okuma işlemidir:
  
  ```jsx
  localStorage.setItem("anahtar", nesne);
  ```

- ..
