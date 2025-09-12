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

## Backend Geliştirme Temelleri🅱️

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
















  
















  





















