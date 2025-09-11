# trex_research
## 1. Modern Yazılım Geliştirme Pratikleri🤷‍♂️

<details>
<summary>Git nedir? GitHub nedir?</summary>

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
<summary>Temel Git komutları: init, clone, add, commit, push, pull, branch, merge</summary>

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
<summary>Merge conflict nedir? Nasıl Çözülür?</summary>
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

<summary>.NET nedir? Tarihçesi amacı,neden kullanılır?</summary>



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

<summary>.NET Framework, .NET Core ve .NET 7/8+ farkları</summary>

<img width="1793" height="980" alt="3103b3d4-4683-4e3c-9dbf-8854276eac22" src="https://github.com/user-attachments/assets/610d3e75-a682-4eb4-bb24-608392d070f5" />


  





















