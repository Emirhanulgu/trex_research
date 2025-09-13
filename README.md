# trex_research
## 1. Modern Yazılım Geliştirme Pratikleri🤷‍♂️

<details>
<summary><strong>Git nedir? GitHub nedir?<strong></summary>

* Git, yazılım geliştirmede kod değişikliklerini kaydeden ve yöneten bir versiyon kontrol sistemidir.  
* Kod üzerinde yapılan her değişiklik bir sürüm olarak saklanır.  
* Aynı proje üzerinde birden fazla kişinin çakışmadan çalışmasına olanak sağlar.  
* Geçmişte yapılan değişikliklere geri dönüp bakılabilir.  

---

* GitHub ise Git altyapısını kullanarak projelerin internet üzerinde tutulduğu bulut tabanlı bir platformdur.  
* Ekip çalışmasını kolaylaştırmak için issue (sorun takibi), pull request (kod katkısı), GitHub Actions (otomasyon) gibi araçlar sunar.  
* Açık kaynak projelerin paylaşımı için en çok kullanılan platformlardan biridir.  

</details>

<details>
<summary><strong>Temel Git komutları: init, clone, add, commit, push, pull, branch, merge<strong></summary>

* `git init` → Yeni bir Git deposu başlatır. ***Örnek*** = `O klasörde .git adında gizli bir klasör oluşur → bu klasör Git’in tüm geçmişi, ayarları ve sürüm kontrol bilgilerini saklar.`
* `git clone` → Var olan bir depoyu bilgisayarına indirir. ***Örnek*** = https://github.com/kullanici/proje.git 
* `git add` → Dosyaları commit için hazırlar.***Örnek*** = `git add index.html`
* `git commit` → Yapılan değişiklikleri kaydeder. ***Örnek*** = `git commit -m "Ana sayfa güncellendi`
* `git push` → Kaydedilen değişiklikleri uzak depoya gönderir. ***Örnek*** = `git push origin main`
* `git pull` → Uzak depodaki son değişiklikleri indirir. ***Örnek*** = `git pull origin main`
* `git branch` → Yeni bir dal (branch) oluşturur. ***Örnek*** = `git branch yeni-ozellik`
* `git merge` → Farklı dalları birleştirir. ***Örnek*** = `git merge yeni-ozellik`

</details>

<details>
<summary><strong>Merge conflict nedir? Nasıl Çözülür?<strong></summary>
  <br>
 Merge conflict, Git’te iki farklı dalda (branch) aynı dosyanın aynı kısmında farklı değişiklikler yapılınca ortaya çıkan çakışmadır.

Git, hangi değişikliğin geçerli olacağına otomatik karar veremez.

Bu yüzden kullanıcıya sorar: “Hangi değişikliği istiyorsun?”

Kısaca:

“İki kişi aynı yerde farklı şeyler yazdı, Git karıştı, sen karar ver!”
<br>

---

 <br>
 Merge Conflict Nasıl Çözülür?

1.Çatışan dosyayı açmak: Git, hangi dosyada çatışma olduğunu gösterir.

2.Değişiklikleri incelemek: Hangi değişikliğin kalacağını veya iki değişikliği birleştirip bir çözüm oluşturacağını seçersin.

3.Değişikliği kaydetmek ve bildir: Çatışmayı çözdükten sonra Git’e bu dosyanın artık hazır olduğunu bildirmek için commit yapılır.

---

</details>


<details>
<summary>CI/CD Nedir? AzureDevOps, GitHub Actions ile pipeline örnekleri</summary>
   <br>
CI/CD, yazılım geliştirme sürecinde otomasyon ve sürekli teslim sağlayan bir yaklaşımdır. İngilizce açılımı:

 <br>

***CI (Continuous Integration) → Sürekli Entegrasyon***

***CD (Continuous Delivery / Continuous Deployment) → Sürekli Teslim / Sürekli Yayın***

Kısaca, yazılımın daha hızlı, güvenli ve hatasız geliştirilmesini sağlayan yöntemdir.
<br>
<br>

---

***CI – Continuous Integration (Sürekli Entegrasyon)***

Geliştiriciler, yaptıkları değişiklikleri sıklıkla ortak koda (main branch) entegre eder.

Her entegrasyon otomatik olarak test edilir, böylece hatalar erken yakalanır.

Amaç: Kodun her zaman çalışır durumda olmasını sağlamak.

Örnek:
Birden fazla kişi aynı projede çalışıyor. Herkes kendi değişikliklerini sık sık ana koda ekliyor ve sistem otomatik olarak test ediyor. Böylece büyük bir hata oluşmadan önlem alınabiliyor.
<br>
<br>


---

***CD – Continuous Delivery / Deployment (Sürekli Teslim / Yayın)***

Continuous Delivery (Sürekli Teslim): Kod değişiklikleri testlerden geçtikten sonra her an yayına alınabilir hâle getirilir. Ama yayın manuel olabilir.

Continuous Deployment (Sürekli Yayın): Kod değişiklikleri testleri geçtikten sonra otomatik olarak canlıya çıkar.

Örnek:
Testleri geçen bir özellik, insan müdahalesi olmadan direkt kullanıcıya sunulabilir.
<br>
<br>

---

***CI/CD’nin Avantajları***

1.Hızlı geri bildirim: Hatalar erken bulunur.

2.Daha güvenli kod: Testler sürekli çalışır.

3.Hızlı teslim: Yeni özellikler ve düzeltmeler kullanıcıya çabuk ulaşır.

4.İnsan hatasını azaltır: Otomasyon sayesinde manuel hatalar azalır.
<br>


---


📌**Azure DevOps Pipeline Örneği**
 ```
name: Python CI/CD

# 1. Tetikleyici (Trigger)
on:
  push:
    branches: [ main ]       # main branch’e push olunca tetiklenir
  pull_request:
    branches: [ main ]       # Pull request açıldığında da tetiklenir

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest    # 2. Hangi işletim sistemi üzerinde çalışacak

    steps:
    # 3. Repo kodunu çek
    - uses: actions/checkout@v3
      name: Step 1: Checkout code
      # Ne yapıyor: Repository’deki kodu pipeline ortamına kopyalar

    # 4. Python kurulumu
    - name: Step 2: Setup Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'
      # Ne yapıyor: Pipeline ortamına Python 3.x kurar

    # 5. Bağımlılıkları yükleme
    - name: Step 3: Install dependencies
      run: pip install -r requirements.txt
      # Ne yapıyor: Projenin çalışması için gerekli kütüphaneleri yükler

    # 6. Testleri çalıştır
    - name: Step 4: Run tests
      run: pytest
      # Ne yapıyor: Kodun düzgün çalışıp çalışmadığını kontrol etmek için testleri çalıştırır (CI adımı)

    # 7. Deploy
    - name: Step 5: Deploy to server
      run: |
        scp -r ./app user@server:/var/www/app
        ssh user@server 'systemctl restart app'
      # Ne yapıyor: Testler başarılıysa kodu uzak sunucuya kopyalar ve uygulamayı restart eder (CD adımı)

```

🔑 Açıklama

* trigger → `Pipeline’ın hangi branch için çalışacağını belirler.`

* pool → `Build ajanını seçer (Linux, Windows veya macOS).`

* UseDotNet@2 → `İstenilen .NET SDK sürümünü indirir.`

* dotnet restore / build / test → `CI aşamaları.`

* dotnet publish → `Deploy edilebilir paket üretir.`

* PublishBuildArtifacts → `Bu paketi artifact olarak kaydeder, release pipeline’da kullanılabilir.`

---

📌**GitHub Actions Pipeline Örneği**
```
name: .NET CI/CD

on:
  push:
    branches: [ "main" ]   # main branch'e push olunca çalışır
  pull_request:
    branches: [ "main" ]   # PR açılınca da çalışır

jobs:
  build:
    runs-on: ubuntu-latest   # Çalışacağı ortam

    steps:
    - name: Checkout code
      uses: actions/checkout@v4   # Repo kodlarını indirir

    - name: Setup .NET
      uses: actions/setup-dotnet@v4
      with:
        dotnet-version: '8.0.x'   # .NET versiyonu

    - name: Restore dependencies
      run: dotnet restore

    - name: Build
      run: dotnet build --configuration Release --no-restore

    - name: Test
      run: dotnet test --no-build --verbosity normal

    - name: Publish
      run: dotnet publish -c Release -o ./publish

```

🔑 Açıklama

* on → `Pipeline’ın hangi durumlarda çalışacağını belirler (ör. push, pull request).`

* runs-on → `Build ortamı (ubuntu-latest, windows-latest, vs.).`

* actions/checkout → `GitHub reposundan kodları indirir.`

* actions/setup-dotnet → `İstediğin .NET SDK sürümünü kurar.`

* dotnet restore / build / test / publish → `CI/CD aşamaları.`
</details>


 <details>     
 
 <summary>Ek Maddeler</summary>
 
<br>  

**SDLC Aşamaları (Yazılım Geliştirme Yaşam Döngüsü)**

**Planlama (Planning)**

* Projenin amacı, kapsamı ve hedefleri belirlenir.

* Zaman, maliyet ve kaynak planlaması yapılır.

**Gereksinim Analizi (Requirement Analysis)**

* Kullanıcı ihtiyaçları toplanır.

* Fonksiyonel (ne yapacak) ve fonksiyonel olmayan (performans, güvenlik vb.) gereksinimler netleştirilir.

**Tasarım (Design)**

* Sistem mimarisi, veri tabanı ve arayüz tasarımı yapılır.

* Yüksek seviye (mimari) ve düşük seviye (detaylı) tasarım hazırlanır.

**Geliştirme (Implementation / Development)**

* Kodlama aşaması başlar.

* Takım üyeleri belirlenen tasarıma göre yazılımı geliştirir.

**Test (Testing / Verification)**

* Yazılım hatalara karşı test edilir.

* Birim testleri, entegrasyon testleri, sistem testleri ve kullanıcı kabul testleri yapılır.

**Dağıtım (Deployment)**

* Yazılım canlı ortama alınır.

* Kullanıcıların erişimine açılır.

**Bakım (Maintenance / Support)**

* Hatalar düzeltilir, güncellemeler yapılır.

* Yeni ihtiyaçlara göre sistem geliştirilir.
  
**Metodolojiler** Ⓜ️

Agile → Esnek, hızlı geri bildirim.

Scrum → Sprint (2-4 hafta), roller (PO, SM, Dev Team).

Kanban → İş akışı panosu (To Do → Doing → Done).


 </details>

 ## 2. .Net Ekosistemi🌁
 <details>

<summary><strong>.NET nedir? Tarihçesi amacı,neden kullanılır?<strong></summary>



**.NET Nedir?**

.NET, Microsoft tarafından geliştirilen, farklı platformlarda (Windows, Linux, macOS) çalışan uygulama geliştirme platformudur.

Web, masaüstü, mobil, oyun, IoT ve bulut uygulamaları geliştirmek için kullanılabilir.

C#, F#, VB.NET gibi dilleri destekler.

İçinde CLR (Common Language Runtime) adlı bir çalışma zamanı bulunur → bu sayede kodlar güvenli, hızlı ve yönetilebilir şekilde çalışır.

<hr>

**Tarihçesi**

2002: İlk kez .NET Framework 1.0 yayımlandı. Sadece Windows üzerinde çalışıyordu.

2016: Microsoft, .NET Core’u çıkardı → açık kaynak ve cross-platform oldu.

2020: .NET 5 yayımlandı → Framework ve Core birleşti. Artık sadece “.NET” olarak adlandırılıyor.

Günümüz: En güncel sürüm .NET 8 (LTS), performans ve platform desteği çok gelişmiş durumda.

<hr>

**Amacı**

Yazılım geliştirmeyi kolaylaştırmak,

Farklı cihaz ve platformlarda ortak bir yapı sağlamak,

Performanslı, güvenli ve ölçeklenebilir uygulamalar geliştirmeyi mümkün kılmak.

<hr>

**Neden Kullanılır?**

 Çapraz platform: Windows, Linux, macOS’ta çalışır.<br>
 Çok amaçlı: Web (ASP.NET), masaüstü (WPF, WinForms), mobil (.NET MAUI, Xamarin), oyun (Unity), bulut (Azure) gibi birçok alanda kullanılabilir.<br>
 Açık kaynak ve güçlü topluluk desteği var.<br>
 Yüksek performans ve güvenlik sağlar.<br>
 Düzenli olarak güncellenir, Microsoft ve açık kaynak topluluk tarafından desteklenir.<br>
</details>

  <details>

<summary><strong>.NET Framework, .NET Core ve .NET 7/8+ farkları<strong></summary>

<img width="1793" height="980" alt="3103b3d4-4683-4e3c-9dbf-8854276eac22" src="https://github.com/user-attachments/assets/610d3e75-a682-4eb4-bb24-608392d070f5" />
</details>
<details>

<summary><strong>Senkron Ve Asenkron Programlama<strong></summary>

<br>

## 💻Senkron Programlama Nedir:
- Senkron programlama, işlemlerin ardışık olarak yürütüldüğü programlama modelidir. Bir görev tamamlanmadan diğerine geçilmez; bu nedenle işlem sırası nettir ancak uzun süren işlemler tüm süreci yavaşlatabilir.



## Günlük Hayattan Benzetmeler:

- Sırada beklemek → Kasada bir müşteri işini bitirmeden diğerine geçilmez.

- Telefon görüşmesi → Karşı taraf konuşmayı bitirmeden sen konuşamazsın.


## 💻Senkron Python Örneği:
```
print("Dosya okunuyor...")
data = open("veri.txt").read()   # Bu işlem bitene kadar beklenir
print("Dosya okundu:", data)
```
## Artı/Eksi Yönleri:

- Kod Akışı Basittir. Takip etmesi kolaydır.
- Uzun süren işlemler(dosya okuma API çağrısı tüm süreci bloke eder).

<hr>

## 👨‍💻Asenkron Programlama Nedir:

- Asenkron programlama, işlemlerin eşzamanlı olarak yürütülmesine izin veren bir modeldir. Bir görev tamamlanana kadar diğerleri beklemek zorunda değildir; uzun süren işlemler arka planda devam ederken program diğer işlere geçebilir.

## Günlük Hayattan Benzetmeler

- Restoranda sipariş vermek → Garson siparişini alır, mutfağa iletir ve senin yemeğini beklemeden başka müşterilerle ilgilenir.

- Mesajlaşma uygulaması → Mesaj gönderilirken internet yavaş olsa bile uygulama donmaz, sen başka mesajlar yazabilirsin.


## 👨‍💻Asenkron Python Örneği:
```
import asyncio

async def islem():
    print("İşlem başladı...")
    await asyncio.sleep(2)   # 2 saniyelik bekleme (bloklamaz)
    print("İşlem bitti!")

async def main():
    await asyncio.gather(islem(), islem())  # İki işlem paralel yürür

asyncio.run(main())
```


## C#’ta Arrow Function (=>) İfadesi:

- C#’ta => ifadesi lambda expression (lambda ifadeleri) için kullanılır.


**1.Kısa Fonksiyon Yazımı**
- Normal metod tanımlarına göre çok daha kısa ve okunabilir fonksiyonlar yazmayı sağlar.
- Örn:
 ```
- Func<int, int> kare = x => x * x;
```


**2.Anonim Fonksiyonlar**
  - İsmi olmayan, tek satırlık fonksiyonlar oluşturmak için kullanılır.
  - Event, delegate veya LINQ işlemlerinde sık kullanılır.

**3.LINQ Sorgularında Kullanımı**
  - Veri filtreleme, sıralama, seçim işlemlerinde pratik yazım sağlar.
  - Örn:
```
var ciftSayilar = sayilar.Where(x => x % 2 == 0);
```
  
**4.Expression-bodied Members (C# 6.0 ve sonrası)**

  - Property, metod veya constructor’larda tek satırlık gövde tanımı yapılabilir.
  - Örn:
```
public string Name { get; set; }
public override string ToString() => $"Name: {Name}";
```

**5.Okunabilirlik ve Modern Syntax**

  - Kodun daha az satırla yazılmasını ve daha temiz görünmesini sağlar.
  - Geleneksel anonim metod yazımına kıyasla daha derli toplu bir alternatiftir.
</details>

## 3.Backend Geliştirme Temelleri🅱️

<details>
<summary><strong>Backend Nedir? Frontend İle Farkları<strong></summary>
  
<br>

**Backend Nedir?**
  - Backend, bir uygulamanın arka planda çalışan kısmıdır. Kullanıcının doğrudan görmediği, ama uygulamanın çalışmasını sağlayan veritabanı yönetimi, iş mantığı, API geliştirme, kimlik doğrulama gibi süreçleri içerir.

**Örnek:**
  - Bir e-ticaret sitesinde ürün siparişi verdiğinde, siparişin veritabanına kaydedilmesi, stok kontrolü yapılması ve ödeme işlemlerinin gerçekleşmesi backend tarafından yönetilir.


<hr>

**Frontend Nedir?**
  - Frontend, kullanıcının doğrudan etkileşimde bulunduğu kısımdır. Web sayfasının tasarımı, butonlar, formlar, yazılar, görseller ve kullanıcı deneyimi (UI/UX) frontend tarafından sağlanır.


 **Örnek:**
  - Aynı e-ticaret sitesinde ürünlerin listelenmesi, sepet butonu, ödeme formu ve sipariş onay ekranı frontend’in işidir.

**🔄 Backend ve Frontend Farkları**

| Özellik            | Frontend                                   | Backend                                  |
|--------------------|--------------------------------------------|------------------------------------------|
| Kullanıcı ile İlişki | Doğrudan kullanıcının gördüğü arayüz      | Kullanıcının görmediği iş mantığı         |
| Teknolojiler       | HTML, CSS, JavaScript, React, Angular      | C#, Java, Python, Node.js, SQL            |
| Görev              | Görsellik, kullanıcı etkileşimi            | Veri işleme, API, güvenlik, mantık        |
| Örnek              | “Sepete Ekle” butonunun görünümü           | “Sepete Ekle” isteğinin veritabanına kaydı |

</details>

<details>
<summary><strong>Web Sunucusu Nedir? Apı Nedir? Apı Türleri<strong></summary>

<br>

## Web Sunucusu Nedir?
  - Web sunucusu, internet üzerinden gelen HTTP/HTTPS isteklerini alan ve bu isteklere karşılık web sayfaları veya veri gönderen bir yazılım veya donanımdır.


**Kısaca:**

   - Tarayıcı (frontend) bir istekte bulunur.
   - Web sunucusu (backend) isteği alır.
   - İlgili dosyayı veya veriyi tarayıcıya geri gönderir.

**Örnekler:**

  - Apache, Nginx, Microsoft IIS
  - Node.js ile yazılmış Express sunucusu

**Önemli Noktalar:**
  - Web sunucuları sadece statik dosya gönderebilir (HTML, CSS, JS) veya dinamik içerik üretebilir (PHP, Node.js, Python).
  - Backend ile birlikte çalışarak veri tabanından veri çekip kullanıcıya sunabilir.
  - Güvenlik, performans ve erişilebilirlik açısından kritik rol oynar.

<hr>

## API Nedir?
  - API (Application Programming Interface / Uygulama Programlama Arayüzü), iki yazılımın birbiriyle iletişim kurmasını sağlayan bir köprüdür.


**Kısaca:**

   - Bir uygulama başka bir uygulamadan veri almak veya işlem yapmak isterse API kullanır.
   - API, hangi verilerin alınabileceğini, hangi işlemlerin yapılabileceğini standart bir şekilde belirtir.


**Örnekler:**

  - Twitter API → Tweet atma, okuma işlemleri
  - Google Maps API → Harita ve konum verisi alma
  - REST API → Web üzerinden veri alışverişi (JSON formatında)

**Önemli Noktalar:**
  - API, genellikle web sunucuları üzerinden çalışır.
  - Frontend ve backend arasındaki iletişimi sağlar.
  - Modern yazılım geliştirmede veri paylaşımı ve entegrasyon için çok önemlidir.

## API Türleri

1. **REST API**  
   - HTTP protokolü üzerinden çalışır.  
   - JSON veya XML ile veri gönderir/alır.  
   - Basit ve yaygın olarak kullanılır.  

2. **SOAP API**  
   - XML tabanlıdır.  
   - Daha katı kurallar ve güvenlik özellikleri vardır.  
   - Kurumsal sistemlerde sık kullanılır.  

3. **GraphQL API**  
   - Tek bir endpoint üzerinden ihtiyacınız olan veriyi seçerek almanızı sağlar.  
   - Daha esnek ve veri israfını önler.  

4. **WebSocket API**  
   - Sürekli bağlantı sağlar, gerçek zamanlı veri iletimi için kullanılır.  
   - Örn: Chat uygulamaları, canlı bildirimler.
  

## HTTP Nedir?

**HTTP (HyperText Transfer Protocol / HiperMetin Transfer Protokolü)**, web tarayıcıları ile web sunucuları arasında **veri alışverişini sağlayan protokoldür**.  
Kısaca, biz tarayıcıda bir siteyi açtığımızda veya bir API isteği gönderdiğimizde, bu iletişim HTTP üzerinden gerçekleşir.  

### Temel Özellikleri:
- **İsteğe Dayalı (Request-Response) Yapı:**  
  Tarayıcı veya başka bir istemci, sunucuya bir istekte bulunur (request). Sunucu da buna karşılık bir yanıt (response) döner.  
- **Stateless (Durumsuz) Protokol:**  
  Her HTTP isteği bağımsızdır. Sunucu, önceki istekleri hatırlamaz. Durum bilgisi gerekiyorsa, genellikle **çerez (cookie) veya token** kullanılır.  
- **Metin Tabanlıdır:**  
  HTTP mesajları kolay okunabilir metin formatındadır, bu da debug ve geliştirmeyi kolaylaştırır.


 ### HTTP Metodları:
HTTP ile hangi işlemi yapmak istediğimizi belirten bazı temel metodlar vardır:  
- **GET:** Sunucudan veri almak için kullanılır.  
- **POST:** Sunucuya veri göndermek için kullanılır.  
- **PUT:** Sunucudaki mevcut veriyi güncellemek için kullanılır.  
- **DELETE:** Sunucudaki veriyi silmek için kullanılır.  
- **PATCH:** Verinin sadece belirli bir kısmını güncellemek için kullanılır.



```http
# GET - Tüm kullanıcıları al
GET /users HTTP/1.1
Host: www.ornekapi.com

# POST - Yeni kullanıcı ekle
POST /users HTTP/1.1
Host: www.ornekapi.com
Content-Type: application/json

{
  "username": "emir",
  "age": 16
}

# PUT - Mevcut kullanıcıyı tamamen güncelle
PUT /users/2 HTTP/1.1
Host: www.ornekapi.com
Content-Type: application/json

{
  "username": "emir_ulgu",
  "age": 17
}

# PATCH - Kullanıcının sadece bir alanını güncelle
PATCH /users/2 HTTP/1.1
Host: www.ornekapi.com
Content-Type: application/json

{
  "age": 17
}

# DELETE - Kullanıcıyı sil
DELETE /users/2 HTTP/1.1
Host: www.ornekapi.com
```
</details>


<details>
<summary><strong>Restful servislerin çalışma mantığı<strong></summary>

## Restful Nedir
- RESTful, internet üzerinden veri alışverişi yapan servislerin bir standart ve düzeni
- Web siteleri veya uygulamalar veri almak/veri göndermek ister.
- RESTful servisler, bunu belirli kurallara göre yapar.
- Bu kurallara uyan servisler “RESTful” olarak adlandırılır.


### Çalışma Mantığı:

- **İstemci : kısaca kullanıcya hizmet verir ve veri gösterir işlem yapmaz sadece sunucuda olan veriyi kullanıcıya gösterrir. Web tarayıcısı, mobil uygulama veya başka bir servis olabilir. Örnek olarak Google,Firefox Mobil olarak ise IOS,Android örnek gösterilebilir. Sunucu değişse bile istemci sorunsuz çalışır**

- **Sunucu : Veriyi saklar işler ve istemciye kullanıcıya sunması için ayarlar iş mantığı ve veri yönetiminden sorumludur İstemci bir konuda veri istediğinde ona sunmakla görevli olandır Sunucu DB'den gerekli veriyi çeker ve kullanıcıya gösterir**

- **HTTP Çalışması : RESTful servislerde istemci ile sunucu arasındaki iletişim HTTP üzerinden olur bu yüzden HTTP çok önemli bir rol alır. İlk adım olarak istemci isteği oluşturur ardından URL belirlenir hangi kaynağa erişmek istediğini belirler HTTP metodu ne yapmak istediğini belirtir (GET,POST,DELETE,PUT) İkinci Adımda sunucu isteği alır ve yorumlar URL ve HTTP metoduna göre hangi kaynak olacağının hedefini belirler gerekirse DB'ye erişir veya iş mantığını çalıştırır Üçüncü Adımda ise sunucu reponse(yanıtı) gönderir Örn: HTTP statü kodu vs..**

- **DİPNOT : RESTful servisler stateless çalışır. Her HTTP isteği bağımsızdır, sunucu önceki isteği hatırlamaz. Yani Sunucu, istemcinin daha önce ne yaptığını bilmez; gerekli tüm bilgiyi her istekte istemci gönderir. HTTP isteği sunucuya "Ben bunu yapmak istiyorum." demesidir ancak Stateless sunucu öncekileri hatırlamaz her istek bağımsızdır**

</details>


<details>
<summary><strong>json veri formatı ve kullanım amacı<strong></summary>

## Json veri formatı nedir?

- JSON (JavaScript Object Notation), verileri düz metin olarak saklayan ve paylaşan bir formattır.
- İnsan tarafından okunabilir, bilgisayar tarafından kolay işlenebilir.
- Web uygulamaları, API’ler ve sunucular arasında veri alışverişi yapmak için sık kullanılır.

## Örnek Json:
```
{
  "id": 1,
  "username": "emir",
  "age": 16,
  "isStudent": true,
  "hobbies": ["yazılım", "futbol", "müzik"]
}
```
## Kullanım Alanları
- Web API’leri ile veri göndermek ve almak
- JavaScript uygulamalarında veri depolamak
- Sunucular ve istemciler arasında iletişim

</details>


<details>
<summary><strong>SOAP ve GraphQL nedir, REST' ten farkları<strong></summary>


### 1. SOAP (Simple Object Access Protocol)
- XML tabanlı bir web servis protokolüdür.  
- Çok katı kurallara sahiptir, güvenlik özellikleri güçlüdür.  
- Daha çok kurumsal sistemlerde (banka, sigorta vb.) tercih edilir.  
- Ağır çalışır ve modern web uygulamalarında az kullanılır.  

### 2. REST (Representational State Transfer)
- HTTP üzerinden çalışan en yaygın web servis mimarisi.  
- Veri genellikle JSON formatında gönderilir/alınır.  
- Basit, hızlı ve hafif yapısıyla modern web uygulamalarında en çok tercih edilen yöntemdir.  
- Stateless (durumsuz) çalışır, her istek bağımsızdır.  

### 3. GraphQL
- Facebook tarafından geliştirilmiş modern API sorgulama dilidir.  
- Tek endpoint üzerinden çalışır.  
- İstemci sadece ihtiyaç duyduğu veriyi alır (over-fetching ve under-fetching sorunlarını çözer).  
- REST’ten daha esnek ama öğrenmesi biraz daha zordur.  

---


### Önemli Farklar

| Özellik          | SOAP                      | REST                          | GraphQL                          |
|------------------|---------------------------|-------------------------------|-----------------------------------|
| Veri Formatı     | XML                      | Genelde JSON (XML de olabilir)| JSON                             |
| Karmaşıklık      | Karmaşık                 | Basit                        | Orta                             |
| Kullanım Alanı   | Kurumsal sistemler        | Web/Mobil uygulamalar         | Modern web uygulamaları          |
| Esneklik         | Düşük                    | Orta                         | Yüksek (alan seçilebiliyor)      |
| Performans       | Daha yavaş               | Hızlı                        | Çok hızlı (gereksiz veri yok)    |

---

</details>

## 4.ASP.NET 🛜

<details>
<summary><strong>ASP.NET ve ASP.NET Core nedir? Avantajları farkları<strong></summary>


## ASP.NET ve ASP.NET Core Nedir? Avantajları ve Farkları

### ASP.NET Nedir?
- Microsoft tarafından geliştirilmiş **web uygulamaları geliştirme framework’üdür**.  
- .NET Framework üzerinde çalışır (Windows tabanlıdır).  
- Web Forms, MVC ve Web API gibi farklı geliştirme modelleri içerir.  
- 2000’li yıllardan itibaren yaygın olarak kullanılmıştır.  

**Avantajları:**
- Windows ortamı için güçlü destek  
- Visual Studio ile entegre çalışır  
- Geniş topluluk ve kütüphane desteği  

---

### ASP.NET Core Nedir?
- Microsoft’un 2016’da çıkardığı **modern, açık kaynaklı ve cross-platform** framework’tür.  
- .NET Core üzerine inşa edilmiştir.  
- Hem Windows, hem Linux, hem de macOS üzerinde çalışabilir.  
- Yüksek performans, esneklik ve bulut odaklı projeler için geliştirilmiştir.  

**Avantajları:**
- Cross-platform (Windows, Linux, macOS) desteği  
- Daha hafif ve yüksek performanslı  
- Modern mimari (Dependency Injection, Middleware)  
- Açık kaynak (GitHub üzerinden geliştiriliyor)  
- Mikroservis ve bulut tabanlı sistemlere uygun  

---

### ASP.NET vs ASP.NET Core Farkları

| Özellik              | ASP.NET (Framework)             | ASP.NET Core                      |
|----------------------|---------------------------------|-----------------------------------|
| **Çalışma Ortamı**   | Sadece Windows                  | Windows, Linux, macOS (cross-platform) |
| **Performans**       | Daha yavaş                      | Daha hızlı ve optimize            |
| **Açık Kaynak**      | Hayır                           | Evet                              |
| **Modüler Yapı**     | Monolitik (büyük yapı)          | Modüler (middleware tabanlı)      |
| **Bulut Desteği**    | Kısıtlı                         | Bulut ve mikroservis dostu        |
| **Geliştirme Modeli**| Web Forms, MVC, Web API         | MVC, Razor Pages, Blazor, Minimal API |

---

</details>

<details>
<summary><strong>MVC nedir ne için kullanılır?<strong></summary>


**MVC (Model - View - Controller)**, yazılım geliştirmede kullanılan bir **mimari desendir**.  
Amaç: **Uygulamayı farklı katmanlara ayırarak daha düzenli, esnek ve bakımı kolay hale getirmek.**

### Katmanlar:
1. **Model (M):**
 - Uygulamanın **veri ve iş mantığını** içerir.
- Veritabanı ile iletişimi sağlar.
- Örn: Kullanıcı bilgilerini saklayan `User` sınıfı.

2. **View (V):**
- Kullanıcıya gösterilen **arayüz kısmıdır**.
- HTML, CSS, JavaScript veya Razor sayfaları olabilir.
- Örn: Kullanıcının profil sayfası.

3. **Controller (C):**
- Kullanıcıdan gelen isteği alır, gerekli işlemleri yapar ve sonucu View’a gönderir.
- Örn: `UserController` → kullanıcı bilgilerini alıp View’a yollar.

---

### MVC’nin Kullanım Amacı:
- Kodun **daha düzenli ve okunabilir** olmasını sağlar.  
- **Bakım ve geliştirmeyi kolaylaştırır.**  
- Takım çalışmasında kolaylık:  
- Backend geliştirici **Model** ile ilgilenir.  
- Frontend geliştirici **View** kısmını yapar.  
- Controller, bu ikisini birbirine bağlar.  

---

</details>

<details>
<summary><strong>Middleware nedir ne için kullanılır?<strong></summary>

## Middleware Nedir? Ne İçin Kullanılır?

**Middleware**, ASP.NET Core uygulamalarında **HTTP isteklerini ve cevaplarını işleyen yazılım bileşenleridir**.  
Yani, **istemci (client) ile sunucu (server) arasındaki istek/cevap akışını yöneten küçük parçalar**dır.

---

### Ne İçin Kullanılır?
- Gelen istekleri kontrol etmek ve işlemek  
- Yanıtı (response) değiştirmek veya yönlendirmek  
- Hata yönetimi yapmak  
- Kimlik doğrulama (Authentication) ve yetkilendirme (Authorization) işlemleri  
- Loglama ve performans takibi  
- Statik dosya sunmak (CSS, JS, resimler vb.)  

---

### Çalışma Mantığı
Middleware bileşenleri **pipeline (boru hattı)** mantığıyla çalışır.  
- Her gelen istek sırasıyla middleware’lerden geçer.  
- Her middleware isteği işleyebilir, değiştirebilir veya bir sonrakine iletebilir.  
- Son middleware cevap (response) üretip geriye döner.  

---

### Basit Örnek (ASP.NET Core Program.cs)
```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

// Middleware 1: Basit log
app.Use(async (context, next) =>
{
    Console.WriteLine("İstek geldi: " + context.Request.Path);
    await next.Invoke(); // bir sonraki middleware'e geç
});

// Middleware 2: Statik dosyalar
app.UseStaticFiles();

// Middleware 3: Routing
app.MapGet("/", () => "Merhaba Middleware!");

app.Run();
```

</details>

<details>
<summary><strong>Dependency Injection (DI) nedir neden önemlidir?<strong></summary>

## Dependency Injection (DI) Nedir? Neden Önemlidir?

**Dependency Injection (Bağımlılık Enjeksiyonu)**, yazılım geliştirmede kullanılan bir tasarım desenidir.  
Amaç: Sınıfların birbirine olan **bağımlılığını azaltmak** ve **esneklik, test edilebilirlik** sağlamaktır.  

---

### Neden Önemlidir?
- Kodun **daha esnek** ve **bakımı kolay** olur.  
- Sınıflar birbirine sıkı sıkıya bağlı olmaz (**loosely coupled**).  
- Mock nesnelerle **kolay test yapılabilir**.  
- Gereksiz kod tekrarını önler.  

---

## Dependency Injection (Doğru Kullanım Örneği)

```csharp
// Interface
public interface IUserRepository
{
    string GetUserById(int id);
}

// Concrete class
public class UserRepository : IUserRepository
{
    public string GetUserById(int id) => "Kullanıcı: Bayram";
}

// Service (DI ile bağımlılık azaltıldı)
public class UserService
{
    private readonly IUserRepository _repo;

    public UserService(IUserRepository repo)
    {
        _repo = repo; // dışarıdan enjekte edildi
    }

    public void GetUser()
    {
        Console.WriteLine(_repo.GetUserById(1));
    }
}

// Program.cs (ASP.NET Core DI Container)
var builder = WebApplication.CreateBuilder(args);

// Bağımlılıkları kaydet
builder.Services.AddScoped<IUserRepository, UserRepository>();
builder.Services.AddScoped<UserService>();

var app = builder.Build();

app.MapGet("/", (UserService userService) =>
{
    userService.GetUser();
    return "Çalıştı!";
});

app.Run();
```
</details>

<details>
<summary><strong>Katmanlı Mimari(Layered Architecture)<strong></summary>

<br>
 
**Katmanlı Mimari (Layered Architecture)**, uygulamayı farklı sorumluluklara ayırarak daha **düzenli, esnek ve bakımı kolay** hale getiren bir yazılım yaklaşımıdır.  

<br>

**En yaygın kullanılan 3 katman şunlardır:**

---

### 1. Presentation Layer (Sunum Katmanı)
- Kullanıcı ile doğrudan etkileşimde bulunan katmandır.  
- Web arayüzü (HTML, CSS, JS, Razor Pages, Blazor) veya mobil uygulama olabilir.  
- Kullanıcıdan gelen veriyi **Business Layer**’a gönderir, oradan gelen sonucu ekrana yansıtır.  

Örnek:  
- ASP.NET MVC Controller  
- Blazor / Razor Page  
- Angular, React, Vue arayüzü  

---

### 2. Business Layer (İş Katmanı)
- Uygulamanın **iş kurallarını ve mantığını** barındırır.  
- Sunum katmanından gelen verileri işler, doğrulamalar yapar, gerekirse Data Access katmanına iletir.  
- İş süreçlerinin merkezi burasıdır.  

Örnek:  
- Kullanıcı kayıt olurken şifre kontrolü  
- Ürün eklerken stok miktarını kontrol etmek  

---

### 3. Data Access Layer (Veri Erişim Katmanı)
- Veritabanı ile iletişimi sağlar.  
- CRUD (Create, Read, Update, Delete) işlemleri bu katmanda yapılır.  
- ORM (Entity Framework, Dapper) veya SQL sorguları kullanılır.  

Örnek:  
- `UserRepository` → veritabanından kullanıcı bilgilerini çeker  
- `ProductRepository` → ürünleri ekler, siler, günceller  

---

<img width="300" height="300" alt="ChatGPT Image 13 Eyl 2025 15_06_53" src="https://github.com/user-attachments/assets/159c0efb-b286-4cb1-9e2a-de4044e49be2" />

</details>

<details>
<summary><strong>Clean Architecture<strong></summary>



Bu katmanlar genellikle **Clean Architecture** veya **Onion Architecture** yaklaşımında kullanılır.  
Amaç: Uygulamayı bağımsız, esnek ve kolay test edilebilir hale getirmektir.  

---

### 1. Domain Layer (Alan Katmanı)
- Uygulamanın **kalbidir**.  
- İş kuralları, **entity**’ler ve domain servisleri burada bulunur.  
- Başka hiçbir katmana bağımlı değildir.  

Örn: `User`, `Product`, `Order` gibi entity sınıfları.  

---

### 2. Application Layer (Uygulama Katmanı)
- **Domain** katmanındaki kuralları kullanarak uygulamanın iş akışını yönetir.  
- **Use Case**’ler ve servisler burada bulunur.  
- Domain’e bağımlıdır ama Infrastructure’a bağımlı değildir.  

Örn: `"Kullanıcı kaydı oluştur",` `"Sipariş ver"` gibi senaryolar.  

---

### 3. Infrastructure Layer (Altyapı Katmanı)
- Veritabanı, dosya sistemi, üçüncü parti servisler gibi **teknik detayları** içerir.  
- **Data Access** (Repository), e-posta gönderimi, loglama gibi işlemler burada yapılır.  
- Application ve Domain katmanlarına hizmet eder.  

Örn: `Entity Framework, Dapper, SMTP, Redis, File Storage.`

---

### 4. API Layer (Sunum Katmanı)
- Dış dünya ile iletişim kurulan katmandır.  
- Kullanıcı veya istemcilerden gelen istekleri alır, **Application Layer**’a iletir.  
- ASP.NET Core Web API, GraphQL API, gRPC vb. olabilir.  

Örn: `UserController`, `ProductController`.  

---

<hr>


### Katmanlar Arası İlişki
- **API → Application → Domain → Infrastructure**  
- Dışarıdan içeriye bağımlılık vardır, iç katmanlar dış katmanlara bağımlı değildir.  

---



## Clean Architecture** prensiplerinden en önemlisi:  
**Bağımlılıklar her zaman dış katmanlardan iç katmanlara doğru akmalıdır.**  

---

### Ne Demek?
- İç katmanlar (**Domain, Application**) dış katmanlara bağımlı OLMAZ.  
- Dış katmanlar (**Infrastructure, API**) iç katmanlara bağımlıdır.  
- Böylece iş kuralları (Domain) **teknolojiden bağımsız** kalır.  

---

### Örnek
- **Yanlış:** Domain katmanı doğrudan Entity Framework’e (Infrastructure) bağımlı olursa → Veritabanı değiştiğinde Domain de değişir.  
- **Doğru:** Domain katmanı sadece **arayüz (interface)** tanımlar. Entity Framework veya başka bir veri kaynağı bu interface’i **Infrastructure** tarafında uygular.  

---

### Akış
- API → Application → Domain  
- Domain **bağımsız**dır, dış katmanlardan hiçbir şey bilmez.  
- Infrastructure, Domain ve Application tarafından tanımlanan interface’leri uygular.  

---

### Özet
- **Bağımlılıkların dışa akması ilkesi:** İç katmanlar dış katmanlara bağımlı değil, dış katmanlar iç katmanlara bağımlıdır.  
- Avantajları:  
  - İş kuralları korunur  
  - Teknolojiden bağımsız geliştirme  
  - Kolay test edilebilirlik
 
</details>

 
## 5.VeriTabanı ve ORM

<details>
<summary><strong>SQL nedir?<strong></summary>

## SQL nedir?
- SQL, ilişkisel veri tabanlarını yönetmek, SQL veri tabanları oluşturmak ve farklı işlevler gerçekleştirerek içlerindeki verileri manipüle etmek için standartlaştırılmış bir programlama dilidir.
- Hem veri tabanı yöneticileri hem de geliştiriciler SQL’i verileri manipüle etmek ve veri entegrasyon komut dosyaları yazmak için kullanır. Benzer şekilde, veri analistleri de ilişkisel bir veri tabanını derinlemesine analiz etmek için SQL kullanır.


**4 temel SQL sorgusuna örnek**
```
-- 1. SELECT → Veri listeleme
SELECT * FROM Customers;

-- 2. INSERT → Yeni veri ekleme
INSERT INTO Customers (Name, City) VALUES ('Eren', 'Zonguldak');

-- 3. UPDATE → Veri güncelleme
UPDATE Customers SET City = 'İstanbul' WHERE Name = 'Eren';

-- 4. DELETE → Veri silme
DELETE FROM Customers WHERE Name = 'Eren';
```

</details>

<details>
<summary><strong>İlişkisel ve ilişkisel olmayan veri tabanları arasındaki farklar<strong></summary>


### 1. İlişkisel Veritabanı (RDBMS)
- Veriler **tablolar** halinde saklanır (satır ve sütun).  
- Tablolar arasında **ilişkiler (foreign key)** vardır.  
- **SQL dili** kullanılır.  
- Veriler tutarlı ve güvenilir şekilde yönetilir.  

**Örnekler:** MySQL, PostgreSQL, SQL Server, Oracle  

---

### 2. İlişkisel Olmayan Veritabanı (NoSQL)
- Veriler tablolar yerine farklı yapılarda saklanır:  
  - **Document** (JSON benzeri) → MongoDB  
  - **Key-Value** → Redis  
  - **Column-based** → Cassandra  
  - **Graph** → Neo4j  
- Esnek şema (schema-less) vardır.  
- Yüksek hız, esneklik ve ölçeklenebilirlik sunar.  

**Örnekler:** MongoDB, Redis, Cassandra, Neo4j  

---

### Temel Farklar

| Özellik              | İlişkisel Veritabanı (SQL) | İlişkisel Olmayan Veritabanı (NoSQL) |
|-----------------------|----------------------------|---------------------------------------|
| **Veri Yapısı**       | Tablo (rows, columns)      | JSON/Döküman, Key-Value, Graph, Column |
| **İlişkiler**         | Tablo ilişkileri (JOIN)    | Genelde yok, denormalize veri          |
| **Sorgu Dili**        | SQL                        | Kendi sorgu yapısı (ör. Mongo Query)  |
| **Şema (Schema)**     | Katı, önceden tanımlı      | Esnek, schema-less                     |
| **Ölçeklenebilirlik** | Dikey (vertical)           | Yatay (horizontal)                     |
| **Kullanım Alanı**    | Finans, ERP, CRM, geleneksel uygulamalar | Büyük veri, IoT, sosyal medya, gerçek zamanlı uygulamalar |

---

</details>

<details>
<summary><strong>ORM nedir? Entity Framework Core nedir?<strong></summary>


### ORM (Object Relational Mapping) Nedir?
- **ORM**, programlama dilindeki nesneler (class, object) ile **ilişkisel veritabanı tabloları** arasında köprü kuran bir tekniktir.  
- Yani, veritabanındaki tabloları **C# sınıfları**, satırları ise **nesneler** gibi kullanmamıza imkân tanır.  
- SQL sorgularını elle yazmak yerine, nesneler üzerinden veritabanı işlemleri yapılır.  

**Avantajları:**
- Daha az SQL kodu yazılır.  
- Kod daha okunabilir ve bakımı kolay olur.  
- Veritabanı bağımsızlığı sağlar (farklı veritabanlarıyla kullanılabilir).  
- Nesne yönelimli programlama ile uyumludur.  

---

### Entity Framework Core Nedir?
- **Entity Framework Core (EF Core)**, Microsoft tarafından geliştirilen bir **ORM aracıdır**.  
- ASP.NET Core projelerinde en çok kullanılan veri erişim teknolojisidir.  
- Farklı veritabanlarını (SQL Server, PostgreSQL, MySQL, SQLite, Oracle vb.) destekler.  
- Açık kaynaklı ve cross-platform çalışır.  

**Avantajları:**
- LINQ (Language Integrated Query) desteği ile SQL yazmadan sorgu yapılabilir.  
- Migration sistemi ile veritabanı tabloları otomatik yönetilebilir.  
- Kod-first veya database-first yaklaşımı kullanılabilir.  

---

</details>

<details>
<summary><strong>DbContext Nedir? Nasıl Kullanılır??<strong></summary>

### DbContext Nedir?
- **DbContext**, Entity Framework Core’da **veritabanı ile uygulama arasındaki köprü**dür.  
- Veritabanındaki tabloları, C# sınıfları (Entity) ile eşleştirir.  
- CRUD işlemleri (Create, Read, Update, Delete) için gerekli fonksiyonları sağlar.  
- EF Core’un en temel sınıfıdır, `Microsoft.EntityFrameworkCore` namespace’i içinde bulunur.  

---

## DbContext Kullanım Örneği

```
csharp
using Microsoft.EntityFrameworkCore;
using System;
using System.Linq;

// Entity (Tablo)
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
}

// DbContext
public class AppDbContext : DbContext
{
    public DbSet<User> Users { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("Server=.;Database=MyDb;Trusted_Connection=True;");
    }
}

class Program
{
    static void Main()
    {
        using var context = new AppDbContext();

        // Ekleme
        context.Users.Add(new User { Name = "Emir" });
        context.SaveChanges();

        // Okuma
        var users = context.Users.ToList();
        foreach (var user in users)
        {
            Console.WriteLine(user.Name);
        }
    }
}

```

</details>

<details>
<summary><strong>LINQ nedir? En çok kullanılan LINQ ifadeleri<strong></summary>

## LINQ Nedir?
- **LINQ (Language Integrated Query)**, .NET ortamında **veri kaynaklarını (koleksiyonlar, veritabanı, XML, vs.) sorgulamak için** kullanılan bir yapıdır.  
- SQL'e benzer şekilde çalışır ama **C# kodunun içine gömülü** halde yazılır.  
- Çalıştığı veri kaynakları: List, Array, Dictionary, Entity Framework, XML, JSON vb.  

---

## En Çok Kullanılan LINQ İfadeleri

```
csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        var numbers = new List<int> { 1, 2, 3, 4, 5, 6 };
        var names = new List<string> { "Ali", "Ayşe", "Emir" };

        // 1. Where (Filtreleme)
        var evenNumbers = numbers.Where(n => n % 2 == 0);
        Console.WriteLine("Where: " + string.Join(", ", evenNumbers)); // 2, 4, 6

        // 2. Select (Veri seçme/dönüştürme)
        var upperNames = names.Select(n => n.ToUpper());
        Console.WriteLine("Select: " + string.Join(", ", upperNames)); // ALI, AYŞE, EMIR

        // 3. OrderBy / OrderByDescending (Sıralama)
        var sorted = numbers.OrderBy(n => n);
        Console.WriteLine("OrderBy: " + string.Join(", ", sorted)); // 1, 2, 3, 4, 5, 6

        var sortedDesc = numbers.OrderByDescending(n => n);
        Console.WriteLine("OrderByDescending: " + string.Join(", ", sortedDesc)); // 6, 5, 4, 3, 2, 1

        // 4. First / FirstOrDefault
        Console.WriteLine("First: " + numbers.First());                 // 1
        Console.WriteLine("FirstOrDefault: " + numbers.FirstOrDefault()); // 1

        // 5. Any / All
        Console.WriteLine("Any > 3: " + numbers.Any(n => n > 3)); // True
        Console.WriteLine("All > 0: " + numbers.All(n => n > 0)); // True

        // 6. Count / Sum / Average / Max / Min
        Console.WriteLine("Count: " + numbers.Count());     // 6
        Console.WriteLine("Sum: " + numbers.Sum());         // 21
        Console.WriteLine("Average: " + numbers.Average()); // 3.5
        Console.WriteLine("Max: " + numbers.Max());         // 6
        Console.WriteLine("Min: " + numbers.Min());         // 1
    }
}
```













































  
















  





















