GÖREV: Mobil Transaction Geliştirme Sistemini Öğren ve Kalıcılaştır

Amaç

Mobil projesindeki tamamlanmış transaction’ları incele. Bir Mobil transaction’ın ekranlarından servis bağlantısına kadar A’dan Z’ye nasıl geliştirildiğini öğren.

Sonraki taleplerde benden mümkün olan en az bilgiyi alarak:

* Gerekli ekran ve bileşenleri oluştur
* Navigation/route bağlantılarını yap
* Servis/API bağlantılarını tamamla
* Request/response mapping işlemlerini yap
* State yönetimini kur
* Form ve iş kuralı validasyonlarını uygula
* Onay ve sonuç akışlarını tamamla
* Resource/localization kayıtlarını ekle
* Gerekli configuration ve registration işlemlerini yap
* Test, lint ve build işlemlerini çalıştır
* Transaction’ı anahtar teslim çalışır duruma getir

Bu çalışma yalnızca Mobil projesi içindir.

Kesin kapsam dışı

Bu öğrenme sistemine aşağıdakileri dahil etme:

* İB/İnternet Bankacılığı projesi
* start.aspx, confirm.aspx, execute.aspx Web Forms yapısı
* Seal MFA
* MFA
* OTP
* Challenge
* İkinci faktör doğrulama
* MFA’ya özel servis, model, ekran ve configuration
* İB veya Seal MFA dokümanları

Şu dosyaları değiştirme:

* docs/copilot/ib-transaction/**
* docs/copilot/seal-mfa/**
* .github/prompts/ib-transaction-*.prompt.md
* .github/prompts/seal-mfa-*.prompt.md

Bir Mobil transaction MFA içeriyorsa yalnızca standart Mobil transaction yapısını incele. MFA’ya özel adımları genel kurallara ekleme.

1. Mobil mimarisini keşfet

Önce mevcut talimatları oku:

* .github/copilot-instructions.md
* .github/instructions/**/*.instructions.md
* AGENTS.md
* README.md
* Package/proje/solution dosyaları
* Build, test ve çalıştırma yönergeleri

Mobil teknolojisini koddan belirle:

* React Native
* Native Android
* Native iOS
* Flutter
* Hybrid
* Kuruma özel framework
* Başka bir teknoloji

Teknolojiyi tahmin etme; proje dosyalarından doğrula.

Şunların konumlarını belirle:

* Screen/page/view dosyaları
* Component’ler
* Navigation/route tanımları
* State yönetimi
* Store/action/reducer/effect/saga yapısı
* ViewModel/controller/presenter yapısı
* Service/API/client katmanı
* DTO/model/request/response
* Mapper/converter
* Validation
* Resource/localization
* Theme/style
* Configuration/environment
* Permission/menu/feature registration
* Test projeleri
* Mock/fixture dosyaları
* Build ve lint komutları

2. Mevcut transaction’ları incele

Mümkünse en az beş güncel, çalışan ve MFA içermeyen Mobil transaction incele.

Örnekler mümkün olduğunca şunları kapsasın:

* Form girişi yapılan işlem
* Liste/seçim yapılan işlem
* Servisten başlangıç verisi alan işlem
* Onay ekranı bulunan işlem
* Servise kayıt/güncelleme gönderen işlem
* Başarı/sonuç/referans gösteren işlem
* Hata ve tekrar deneme akışı bulunan işlem
* Birden fazla servis operasyonu kullanan işlem

Her transaction’da yalnızca ekran dosyasına bakma. Uçtan uca bağlı bütün dosyaları bul:

* Giriş ekranı
* Onay/özet ekranı
* Sonuç ekranı
* Ortak component’ler
* Navigation
* State/store
* Service/API client
* Request/response modelleri
* Mapper
* Validation
* Resource
* Configuration
* Registration
* Test ve mock dosyaları

Git geçmişine erişebiliyorsan transaction’ın oluşturulduğu değişiklikleri de incele:

* git log
* git log --all --grep
* git log -S
* git log -G
* git show
* git diff

Eski ve yeni mimari birlikte bulunuyorsa güncel ve aktif yaklaşımı belirle. Merge, revert ve cherry-pick kopyalarını ayrı örnek sayma.

3. Mobil transaction yaşam döngüsünü öğren

Mevcut çalışan kodlardan gerçek akışı çıkar:

1. Transaction’a giriş
2. Başlangıç verilerinin yüklenmesi
3. Kullanıcı girdilerinin alınması
4. Client-side validation
5. State/model oluşturulması
6. Onay/özet ekranına geçiş
7. Servis request’inin hazırlanması
8. Servis operasyonunun çağrılması
9. Response ve hata yönetimi
10. Başarı/sonuç ekranı
11. Geri dönüş, iptal ve tekrar deneme
12. State temizliği

Şunları özellikle belirle:

* Ekranlar arasında veri nasıl taşınıyor?
* Navigation parametresi mi, store mu, context mi kullanılıyor?
* Sayfa yeniden açıldığında state nasıl davranıyor?
* Loading durumu nasıl gösteriliyor?
* Aynı işlemin iki kez gönderilmesi nasıl engelleniyor?
* Network hatası nasıl yönetiliyor?
* Session/token süresi dolduğunda ne oluyor?
* Onay ekranındaki veri ile servise gönderilen veri nasıl eşleştiriliyor?
* Başarı ve hata yönlendirmeleri nasıl yapılıyor?
* Kullanıcı geri döndüğünde form bilgileri korunuyor mu?
* Platforma özel Android/iOS farklılıkları var mı?

Bunları dışarıdan dayatılmış kural olarak kabul etme. Mevcut çalışan Mobil örneklerden öğren.

4. Servis bağlantı desenini öğren

Şunları tespit et:

* API/service client nasıl elde ediliyor?
* Endpoint nasıl tanımlanıyor?
* HTTP metodu nasıl belirleniyor?
* Request header ve ortak context nasıl ekleniyor?
* Authentication/session bilgisi nasıl aktarılıyor?
* Request nesnesi nerede hazırlanıyor?
* UI modeli request modeline nasıl çevriliyor?
* Response UI modeline nasıl çevriliyor?
* Başarılı response nasıl belirleniyor?
* Business ve technical hata ayrımı nasıl yapılıyor?
* Timeout ve network exception nasıl yönetiliyor?
* Hata kodları resource mesajına nasıl çevriliyor?
* Loading başlangıç/bitiş yönetimi nasıl yapılıyor?
* Servis çağrısı hangi lifecycle aşamasında gerçekleştiriliyor?
* Mock ve gerçek servis ayrımı nasıl yapılıyor?

Gerçek servis contract’ını bulmadan request/response alanı uydurma.

5. Değişmeyen ve değişken alanları ayır

Her Mobil transaction’da tekrar eden yapıyı standart kural olarak kaydet.

Transaction’a göre değişenleri parametre olarak belirle:

* Transaction adı/kodu
* Screen adı
* Route/navigation adı
* Servis ve operasyon
* Request/response tipi
* Form alanları
* Liste/seçim kaynakları
* Validasyonlar
* Onay ekranı alanları
* Sonuç ekranı alanları
* Resource metinleri
* Feature/permission bilgisi
* Analytics/log kayıtları
* Android/iOS farklılıkları
* Test senaryoları

Her parametre için şunlardan birini işaretle:

* Talepten alınmalı
* Koddan çıkarılabilir
* En yakın örnekten varsayılabilir
* Mutlaka kullanıcıya sorulmalı

6. Yeni dosya yolu kuralları

Yeni dosya konumunu şu sırayla belirle:

1. Aynı türdeki en yakın çalışan Mobil transaction
2. Aynı modül/feature altındaki transaction’lar
3. Aynı servis veya ekran akışını kullanan transaction
4. Projenin genel klasör, package/namespace ve isimlendirme standardı
5. Güvenilir örnek yoksa yol uydurma; engelleyici soru olarak bildir

Aşağıdaki tabloyu oluştur:

Dosya türü	Hedef dizin	Adlandırma	Package/namespace	Referans transaction	Birlikte güncellenecek dosyalar

Şunların konumunu özellikle kaydet:

* Giriş ekranı
* Onay ekranı
* Sonuç ekranı
* Component
* Navigation/route
* State/store
* Service/API
* Request/response model
* Mapper
* Validation
* Resource
* Style/theme
* Configuration
* Registration
* Test
* Mock/fixture

7. Kanıta dayalı öğrenme

Her önemli çıkarım için gerçek kod referansı ver:

repo-relative-path | sınıf/fonksiyon/component/symbol | yaklaşık satır | transaction/commit

Kurallar:

* Dosya yolu ve symbol temel referanstır.
* Satır numarası yardımcı bilgidir.
* Büyük kod bloklarını dokümana kopyalama.
* Tek örneği genel standart kabul etme.
* Bir kuralı mümkünse en az iki çalışan örnekle doğrula.
* Secret, token, parola veya kişisel veri kaydetme.
* Çelişen desenleri kesin kural yapma.
* Güncel aktif deseni eski mimariye tercih et.

8. Oluşturulacak dosyalar

Repository talimatı

Mevcut dosyayı güvenli biçimde güncelle veya yoksa oluştur:

.github/copilot-instructions.md

Mobil transaction bölümü çok kısa olsun:

* Mobil transaction işlerinde önce docs/copilot/mobile-transaction/PLAYBOOK.md okunmalı.
* En yakın güncel çalışan Mobil transaction örnek alınmalı.
* İB ve MFA yapıları Mobil transaction’a karıştırılmamalı.
* İlgisiz refactor yapılmamalı.
* İşlem test, lint ve build ile doğrulanmalı.

Ana Mobil hafızası

Oluştur:

docs/copilot/mobile-transaction/PLAYBOOK.md

Bölümleri:

1. Teknoloji ve mimari
2. Proje/modül haritası
3. Transaction türleri
4. Uçtan uca yaşam döngüsü
5. Ekran ve component kuralları
6. Navigation
7. State yönetimi
8. Servis/API entegrasyonu
9. Request/response mapping
10. Validation
11. Loading ve hata yönetimi
12. Onay ve sonuç akışı
13. Resource/localization
14. Android/iOS farklılıkları
15. Dosya konumlandırma
16. İsimlendirme
17. Varsayılan kararlar
18. Kullanıcıya sorulması zorunlu bilgiler
19. Test/lint/build komutları
20. Anahtar teslim kontrol listesi
21. Yapılmaması gerekenler

PLAYBOOK kısa ve yoğun olsun; mümkünse 3.000 tokenı geçmesin.

Örnek indeksi

Oluştur:

docs/copilot/mobile-transaction/EXAMPLES.md

Transaction	Tür	Ekranlar	Navigation	Service/API	State	Ek dosyalar	Commit

Bu dosya yalnızca PLAYBOOK yetersiz olduğunda okunsun.

Uygulama promptu

Oluştur:

.github/prompts/mobile-transaction-uygula.prompt.md

Girdileri:

TALEP:
${input:talep}
VARSA SERVİS/CONTRACT:
${input:servis}
VARSA REFERANS TRANSACTION:
${input:referans}

Çalışma sırası:

1. Yalnızca PLAYBOOK’u oku.
2. Talebi parametrelere ayır.
3. En yakın transaction desenini seç.
4. Gerekli dosya ve symbol’leri aç.
5. İB veya MFA yapısı ekleme.
6. Engelleyici olmayan eksikleri mevcut standarttan çıkar.
7. Zorunlu soruları tek mesajda grupla.
8. Transaction’ı A’dan Z’ye uygula.
9. Ekran, navigation, state, servis, mapping, validation ve resource işlemlerini tamamla.
10. Test, lint ve build çalıştır.
11. Hataları giderip yeniden doğrula.
12. Anahtar teslim kontrol listesi tamamlanmadan işi bitmiş sayma.

Denetim promptu

Oluştur:

.github/prompts/mobile-transaction-denetle.prompt.md

Şunları kontrol etsin:

* Talebe uygunluk
* Eksik ekran/component
* Navigation
* State aktarımı
* Servis/API bağlantısı
* Request/response mapping
* Validation
* Loading ve hata yönetimi
* Onay ve sonuç akışı
* Tekrar gönderim riski
* Resource/configuration/registration
* Android/iOS uyumu
* Test/lint/build

Önce yalnızca kanıtlı rapor oluştursun. Kullanıcı “düzelt” demeden kod değiştirmesin.

Öğrenme promptu

Oluştur:

.github/prompts/mobile-transaction-ogren.prompt.md

Tamamlanmış ve kullanıcı tarafından doğrulanmış transaction için:

* Yeni transaction’ı PLAYBOOK ile karşılaştır.
* Yalnızca yeni ve tekrar kullanılabilir desenleri belirle.
* PLAYBOOK’u gereksiz büyütmeden güncelle.
* Transaction’ı EXAMPLES dosyasına ekle.
* Tek işe özgü business bilgisini genel kural yapma.
* İB veya MFA bilgisini ekleme.

9. Minimum soru politikası

Koddan güvenilir biçimde çıkarılabiliyorsa şunları sorma:

* Dosya yolları
* Component yapısı
* Navigation yöntemi
* State yönetimi
* API client kullanımı
* Loading/hata gösterimi
* Resource konumu
* İsimlendirme
* Test dosyası konumu
* Build komutları

Yalnızca şu durumlarda soru sor:

* Servis operasyonu belirsizse
* Contract bulunamıyorsa
* İş kuralı çıkarılamıyorsa
* Birden fazla çelişkili güncel desen varsa
* Dışarıdan verilmesi gereken kod/yetki bilgisi eksikse
* Güven seviyesi %95’in altındaysa

Sorulacak bütün soruları tek, kısa ve numaralı mesajda sor. Birden fazla soru turu oluşturma.

Engelleyici olmayan belirsizliklerde en yakın güncel örneği kullan, varsayımı sonuçta bildir ve çalışmayı durdurma.

10. Anahtar teslim tamamlanma ölçütü

Transaction ancak şu koşullarda tamamlanmıştır:

* Gerekli ekranlar çalışıyor.
* Navigation doğru.
* State/veri aktarımı doğru.
* Servis/API çağrısı doğru.
* Request/response mapping tamam.
* Validasyonlar uygulanmış.
* Loading, hata ve tekrar deneme çalışıyor.
* Onay ve sonuç ekranları doğru.
* Tekrar gönderim/double-click riski yönetilmiş.
* Resource ve configuration kayıtları tamam.
* Android/iOS farklılıkları kontrol edilmiş.
* Testler geçiyor.
* Lint geçiyor.
* Build başarılı.
* Yeni warning/error oluşmamış.
* İlgisiz dosya değiştirilmemiş.
* İB veya MFA kodu eklenmemiş.

11. Token tasarrufu

Sonraki işlerde:

* Önce yalnızca PLAYBOOK’u oku.
* Repository’yi yeniden tarama.
* EXAMPLES’ı yalnızca gerekirse oku.
* Git geçmişine yalnızca düşük güven veya yeni varyant varsa git.
* Dosyaların yalnızca ilgili symbol/bölümlerini aç.
* Uzun analiz günlüğü üretme.
* Aynı bilgiyi tekrarlama.
* Büyük ve ilgisiz diff oluşturma.
* Sonuç raporunu kısa tut.

12. İlk öğrenme aşamasında yapma

Bu çalışmada:

* Yeni transaction geliştirme.
* Mevcut business kodunu değiştirme.
* Refactor yapma.
* Dependency güncelleme.
* Production configuration değiştirme.
* Commit/push/PR oluşturma.
* İB veya MFA dokümanlarını değiştirme.

Yalnızca Mobil yapıyı incele ve belirtilen .md/prompt dosyalarını oluştur.

13. Sonuç raporu

Yalnızca şunları bildir:

* İncelenen Mobil transaction sayısı
* Bulunan transaction türleri
* Tespit edilen Mobil yaşam döngüsü
* Oluşturulan/güncellenen dosyalar
* Otomatik çıkarılabilecek parametreler
* Kullanıcıdan mutlaka alınması gereken bilgiler
* Test/lint/build komutları
* Belirsiz veya çelişkili noktalar
* Kullanılacak üç kısa komut