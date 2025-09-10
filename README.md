# trex_research
## 1. Modern Yazılım Geliştirme Pratikleri

<details>
<summary>Git nedir? GitHub nedir?</summary>

* Git, yazılım geliştirmede kod değişikliklerini kaydeden ve yöneten bir versiyon kontrol sistemidir.  
* Kod üzerinde yapılan her değişiklik bir sürüm olarak saklanır.  
* Aynı proje üzerinde birden fazla kişinin çakışmadan çalışmasına olanak sağlar.  
* Geçmişte yapılan değişikliklere geri dönüp bakılabilir.  

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
 <br>
 Merge Conflict Nasıl Çözülür?

1.Çatışan dosyayı açmak: Git, hangi dosyada çatışma olduğunu gösterir.

2.Değişiklikleri incelemek: Hangi değişikliğin kalacağını veya iki değişikliği birleştirip bir çözüm oluşturacağını seçersin.

3.Değişikliği kaydetmek ve bildir: Çatışmayı çözdükten sonra Git’e bu dosyanın artık hazır olduğunu bildirmek için commit yapılır.

</details>

<details>
<summary>CI/CD Nedir? AzureDevOps, GitHub Actions ile pipeline örnekleri</summary>
   <br>
CI/CD, yazılım geliştirme sürecinde otomasyon ve sürekli teslim sağlayan bir yaklaşımdır. İngilizce açılımı:

***CI (Continuous Integration) → Sürekli Entegrasyon**

***CD (Continuous Delivery / Continuous Deployment) → Sürekli Teslim / Sürekli Yayın***

Kısaca, yazılımın daha hızlı, güvenli ve hatasız geliştirilmesini sağlayan yöntemdir.
<br>
<br>
***CI – Continuous Integration (Sürekli Entegrasyon)***

Geliştiriciler, yaptıkları değişiklikleri sıklıkla ortak koda (main branch) entegre eder.

Her entegrasyon otomatik olarak test edilir, böylece hatalar erken yakalanır.

Amaç: Kodun her zaman çalışır durumda olmasını sağlamak.

Örnek:
Birden fazla kişi aynı projede çalışıyor. Herkes kendi değişikliklerini sık sık ana koda ekliyor ve sistem otomatik olarak test ediyor. Böylece büyük bir hata oluşmadan önlem alınabiliyor.
<br>
<br>
***CD – Continuous Delivery / Deployment (Sürekli Teslim / Yayın)***

Continuous Delivery (Sürekli Teslim): Kod değişiklikleri testlerden geçtikten sonra her an yayına alınabilir hâle getirilir. Ama yayın manuel olabilir.

Continuous Deployment (Sürekli Yayın): Kod değişiklikleri testleri geçtikten sonra otomatik olarak canlıya çıkar.

Örnek:
Testleri geçen bir özellik, insan müdahalesi olmadan direkt kullanıcıya sunulabilir.
<br>
<br>
***CI/CD’nin Avantajları***

1.Hızlı geri bildirim: Hatalar erken bulunur.

2.Daha güvenli kod: Testler sürekli çalışır.

3.Hızlı teslim: Yeni özellikler ve düzeltmeler kullanıcıya çabuk ulaşır.

4.İnsan hatasını azaltır: Otomasyon sayesinde manuel hatalar azalır.
<br>
AzureDevOps Pipeline Örneği



