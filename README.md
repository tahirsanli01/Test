GÖREV: Standart İB Transaction Geliştirme Sistemini Öğren ve Oluştur

Amaç

İB projesindeki standart transaction geliştirme yapısını öğren.

İB’de bir transaction aşağıdaki sayfalardan geçerek tamamlanmaktadır:

1. start.aspx
2. confirm.aspx
3. execute.aspx

Hedefin, daha önce tamamlanmış transaction’ları inceleyerek bu üç aşamalı yapının A’dan Z’ye nasıl geliştirildiğini öğrenmek ve sonraki transaction taleplerinde benden mümkün olan en az bilgiyi isteyerek:

* Gerekli bütün dosyaları doğru dizinlerde oluşturmak
* Sayfaları çalışır hâle getirmek
* Servis bağlantılarını yapmak
* Request/response dönüşümlerini tamamlamak
* Validasyonları uygulamak
* Sayfalar arasındaki veri aktarımını kurmak
* Menü, yetki, resource, configuration ve kayıt işlemlerini tamamlamak
* Build ve test işlemlerini yapmak
* Transaction’ı anahtar teslim çalışır duruma getirmek

Bu öğrenme sistemi standart İB transaction geliştirme içindir.

Kesin kapsam dışı: MFA

Bu çalışmaya hiçbir şekilde aşağıdakileri dahil etme:

* Seal MFA
* MFA
* OTP
* Challenge
* İkinci faktör doğrulama
* MFA başlatma/doğrulama servisleri
* MFA transaction kodları
* MFA’ya özel session/model/configuration
* MFA dokümanları ve promptları

.github/prompts/seal-mfa-*.prompt.md ve docs/copilot/seal-mfa/** dosyalarını değiştirme.

İncelenen bir transaction MFA içeriyorsa yalnızca standart transaction altyapısıyla ilgili bölümlerini değerlendirebilirsin. MFA’ya özgü kodları örnek, zorunlu adım veya varsayılan davranış olarak kaydetme.

Öncelikle MFA içermeyen tamamlanmış transaction örneklerini tercih et.

1. Projeyi ve mevcut talimatları tanı

Önce repository ve solution yapısını belirle.

Varsa aşağıdaki dosyaları oku:

* .github/copilot-instructions.md
* .github/instructions/**/*.instructions.md
* AGENTS.md
* README.md
* Solution ve proje dosyaları
* Build/test yönergeleri
* Projeye ait mimari dokümanlar

Mevcut talimatlara uy. Mevcut dosyaları silme veya bütünüyle yeniden yazma. Gerekirse yalnızca kısa ve uyumlu bölümler ekle.

Şunları tespit et:

* İB web projesinin kök dizini
* Servis/proxy/client projeleri
* Model/DTO projeleri
* Ortak kütüphaneler
* Resource/localization projeleri
* Test projeleri
* Veritabanı script konumu
* Menü/yetki/transaction kayıtlarının bulunduğu yerler
* Build ve test komutları

2. Tamamlanmış transaction örneklerini bul

Mümkünse en az beş farklı, çalışan ve MFA içermeyen transaction incele.

Örnekler şu çeşitleri mümkün olduğunca kapsasın:

* Salt sorgulama/görüntüleme işlemi
* Servisten başlangıç verisi alan işlem
* Kullanıcıdan form girdisi alan işlem
* Finansal olmayan kayıt/güncelleme işlemi
* Finansal veya kritik execute işlemi
* Liste/seçim içeren işlem
* Birden fazla servis operasyonu kullanan işlem
* Başarı sonucu/dekont/referans numarası gösteren işlem

Her örnekte üç sayfayı birlikte incele:

* start.aspx ve ilişkili dosyaları
* confirm.aspx ve ilişkili dosyaları
* execute.aspx ve ilişkili dosyaları

Yalnızca .aspx dosyalarına bakma. İlgili bütün bileşenleri bul:

* Code-behind dosyaları
* Designer dosyaları
* Base page/sınıflar
* User control’ler
* Master page bağlantıları
* JavaScript dosyaları
* CSS/class kullanımları
* DTO/model/request/response sınıfları
* Service client/proxy/factory
* Mapper veya converter’lar
* Validation sınıfları
* Resource dosyaları
* Configuration
* Dependency/service registration
* Menü ve yetki kayıtları
* Transaction registry
* Veritabanı scriptleri
* Unit/integration testleri
* Sonuç/dekont sayfaları
* Route ve navigation tanımları

Git geçmişine erişebiliyorsan ilgili transaction’ların oluşturulduğu commitleri incele:

* git log
* git log --all --grep
* git log -S
* git log -G
* git show
* git diff

Merge, revert ve cherry-pick kopyalarını ayrı örnek olarak sayma.

3. Üç aşamalı transaction yaşam döngüsünü öğren

Mevcut kodun gerçek davranışından aşağıdaki akışı çıkar.

start.aspx

Şunların nasıl yapıldığını tespit et:

* Sayfanın açılması ve ilk yükleme
* IsPostBack kullanımı
* Başlangıç servis çağrıları
* Form kontrollerinin doldurulması
* Dropdown/list verilerinin yüklenmesi
* Varsayılan değerler
* Kullanıcı girdilerinin alınması
* Client-side ve server-side validation
* Request modelinin hazırlanması
* Sayfalar arası aktarılacak transaction modelinin oluşturulması
* Confirm sayfasına geçiş
* Hata gösterimi
* Geri dönüş ve form değerlerinin korunması

confirm.aspx

Şunların nasıl yapıldığını tespit et:

* Start aşamasından gelen verinin alınması
* Verinin session/context/model üzerinden taşınması
* Kullanıcıya gösterilecek özet alanlarının hazırlanması
* Kod/değer bilgilerinin açıklamaya dönüştürülmesi
* Tutar, tarih, hesap ve diğer alanların formatlanması
* Confirm ve vazgeç/geri dön işlemleri
* Tekrarlı postback kontrolü
* Model bütünlüğünün korunması
* Execute sayfasına geçiş
* Direct URL erişimi veya eksik context durumundaki davranış

execute.aspx

Şunların nasıl yapıldığını tespit et:

* Confirm edilmiş modelin alınması
* Gerçek servis request’inin hazırlanması
* Context/header/customer/channel bilgilerinin eklenmesi
* Servis operasyonunun çağrılması
* Response kontrolü
* Hata kodlarının kullanıcı mesajına dönüştürülmesi
* Başarılı işlem sonucu
* Referans numarası/dekont/sonuç bilgisi
* Transaction context temizliği
* Aynı işlemin iki kez yapılmasının engellenmesi
* Refresh, double-click ve tekrar postback davranışı
* Başarı ve hata yönlendirmeleri
* Loglama ve audit davranışı

Bu maddeleri projeye dışarıdan dayatılmış kurallar olarak kabul etme. Mevcut çalışan örneklerde hangi mekanizmaların gerçekten kullanıldığını belirle ve onu kaydet.

4. Servis bağlantı desenini öğren

Servis entegrasyonunu uçtan uca incele:

* Servis client/proxy nasıl elde ediliyor?
* Interface ve implementasyon nerede?
* Endpoint/configuration nasıl belirleniyor?
* Request nesnesi nerede oluşturuluyor?
* Ortak request header/context nasıl ekleniyor?
* Customer, user, channel ve transaction bilgileri nasıl aktarılıyor?
* UI modeli servis request’ine nasıl çevriliyor?
* Servis response’u UI modeline nasıl çevriliyor?
* Başarılı response nasıl belirleniyor?
* Business ve technical hata ayrımı nasıl yapılıyor?
* Timeout ve exception nasıl ele alınıyor?
* Hatalar nasıl loglanıyor?
* Kullanıcıya hangi resource mesajı gösteriliyor?
* Servis registration veya proxy üretimi gerekiyor mu?
* Async/sync kullanım standardı nedir?
* Servis çağrısı hangi aşamada yapılmalıdır?

Servis request ve response alanlarını tahmin ederek uydurma. Gerçek servis contract’larını ve mevcut kullanım örneklerini esas al.

5. Değişmeyenler ve değişkenleri ayır

Her transaction’da tekrar eden standart yapıyı değişmeyen kural olarak kaydet.

Transaction’a göre değişen bilgileri parametre olarak tanımla:

* Transaction adı
* Transaction kodu
* Menü/yetki kodu
* Klasör adı
* Namespace
* URL/route
* Servis adı
* Servis operasyonu
* Request tipi
* Response tipi
* Form alanları
* Confirm alanları
* Execute sonucu
* Validasyon kuralları
* Resource metinleri
* Yetki bilgileri
* Menü konumu
* Veritabanı kayıtları
* Test senaryoları

Her parametre için şunları belirle:

* Talepten alınabilir mi?
* Koddan güvenilir biçimde çıkarılabilir mi?
* En yakın örnekten varsayılabilir mi?
* Mutlaka kullanıcıya sorulması gerekir mi?

6. Yeni dosya yolu belirleme kuralları

Yeni dosya oluştururken şu öncelik sırasını kullan:

1. Aynı transaction türündeki en yakın çalışan örnek
2. Aynı modül/menü altındaki transaction’lar
3. Aynı servis ve request/response tipini kullanan transaction’lar
4. Projenin genel klasör, namespace ve isimlendirme standardı
5. Güvenilir örnek yoksa tahmin etme; engelleyici soru olarak bildir

Her dosya türü için kaydet:

Dosya türü	Hedef dizin	Adlandırma kalıbı	Namespace	Baz alınacak örnek	Birlikte güncellenecek dosyalar

Özellikle şu dosyaların konumlarını belirle:

* start.aspx
* start.aspx.cs
* start.aspx.designer.cs
* confirm.aspx
* confirm.aspx.cs
* confirm.aspx.designer.cs
* execute.aspx
* execute.aspx.cs
* execute.aspx.designer.cs
* Transaction modeli
* Servis request/response mapper
* Resource
* JavaScript
* Configuration
* Menü/yetki/transaction kayıtları
* Veritabanı scripti
* Test dosyaları

Designer dosyaları proje tarafından otomatik üretiliyorsa elle oluşturma kuralı koyma; mevcut proje davranışını kaydet.

7. Kanıta dayalı öğrenme

Her önemli çıkarım için gerçek kod referansı kaydet:

repo-relative-path | sınıf/metot/symbol | yaklaşık satır | örnek transaction/commit

Kurallar:

* Dosya yolu ve symbol temel referanstır.
* Satır numarası yalnızca yardımcı bilgidir.
* Büyük kod bloklarını dokümana kopyalama.
* Aynı bilgiyi tekrarlama.
* Secret, token, parola, connection string veya kişisel veri kaydetme.
* Tek örnekte görülen davranışı zorunlu standart olarak kabul etme.
* Bir kuralı mümkünse en az iki çalışan örnekle doğrula.
* Çelişen desenleri kesin kural olarak yazma.
* Eski ve yeni mimari varsa güncel ve aktif deseni belirle.

8. Oluşturulacak kalıcı dosyalar

A. Repository talimatı

Mevcut dosyayı güvenli biçimde güncelle veya yoksa oluştur:

.github/copilot-instructions.md

Bu dosyaya yalnızca kısa bir bölüm ekle:

* Standart İB transaction işlerinde önce docs/copilot/ib-transaction/PLAYBOOK.md okunmalı.
* Transaction akışı start.aspx → confirm.aspx → execute.aspx olarak ele alınmalı.
* MFA/Seal MFA bu standart akışa dahil edilmemeli.
* Yeni dosya ve servis bağlantıları en yakın çalışan örneğe dayanmalı.
* İlgisiz refactor yapılmamalı.
* İşlem hedefli build/test ile doğrulanmalı.

Ayrıntılı geçmişi bu dosyaya koyma. Bu dosya her istekte bağlama gireceği için kısa tut.

B. Ana çalışma hafızası

Oluştur:

docs/copilot/ib-transaction/PLAYBOOK.md

Bu dosya sonraki geliştirmelerin kısa ve kanonik kaynağı olsun.

Şu bölümleri içersin:

1. Mimari kapsam
2. Proje ve modül haritası
3. Transaction türleri
4. Uçtan uca yaşam döngüsü
5. start.aspx kuralları
6. confirm.aspx kuralları
7. execute.aspx kuralları
8. Sayfalar arası state/model aktarımı
9. Servis bağlantı deseni
10. Request/response mapping
11. Validation ve hata yönetimi
12. Menü/yetki/transaction kayıtları
13. Resource/localization
14. Yeni dosya konumlandırma tablosu
15. İsimlendirme ve namespace kuralları
16. Varsayılan kararlar
17. Kullanıcıya sorulması zorunlu bilgiler
18. Build/test/doğrulama komutları
19. Anahtar teslim tamamlanma kontrol listesi
20. Kesinlikle yapılmaması gerekenler

PLAYBOOK kısa ve yoğun olsun. Mümkünse 3.000 tokenı geçmesin.

C. Örnek transaction indeksi

Oluştur:

docs/copilot/ib-transaction/EXAMPLES.md

Şu tabloyu kullan:

Transaction	Tür	Start	Confirm	Execute	Servis operasyonu	Ek dosyalar	Commit

Bu dosya her yeni işte okunmayacak. Yalnızca PLAYBOOK yetersizse veya yeni transaction mevcut desenle uyuşmuyorsa kullanılacak.

D. A’dan Z’ye uygulama promptu

Oluştur:

.github/prompts/ib-transaction-uygula.prompt.md

Bu prompt aşağıdaki girdileri alsın:

TALEP:
${input:talep}
VARSA SERVİS/CONTRACT BİLGİSİ:
${input:servis}
VARSA REFERANS TRANSACTION:
${input:referans}

Prompt şu şekilde çalışsın:

1. Önce yalnızca PLAYBOOK’u oku.
2. Talep metninden bütün parametreleri çıkar.
3. Transaction türünü belirle.
4. En yakın çalışan örneği seç.
5. Yalnızca gerekli dosya ve symbol’leri aç.
6. MFA veya Seal MFA ekleme.
7. Zorunlu olmayan eksik bilgileri mevcut standarttan çıkar.
8. Yalnızca gerçekten engelleyici bilgileri kullanıcıya sor.
9. Sorulacak bütün soruları tek mesajda grupla.
10. Mümkünse birden fazla soru turu oluşturma.
11. Ardından transaction’ı A’dan Z’ye uygula.
12. Gerekli bütün dosyaları oluştur/güncelle.
13. Servis bağlantılarını ve mapping işlemlerini tamamla.
14. Menü, yetki, resource, configuration ve kayıtları unutma.
15. Build ve testleri çalıştır.
16. Hataları düzeltip tekrar doğrula.
17. Anahtar teslim kontrol listesini tamamlamadan işi bitmiş sayma.

E. Denetim promptu

Oluştur:

.github/prompts/ib-transaction-denetle.prompt.md

Bu prompt mevcut bir transaction’ı PLAYBOOK’a göre denetlesin:

* Start sayfası eksikleri
* Confirm sayfası eksikleri
* Execute sayfası eksikleri
* Servis bağlantıları
* Mapping
* Validation
* State aktarımı
* Menü/yetki
* Resource
* Configuration
* Testler
* Build
* Güvenlik ve tekrar işlem riskleri

İlk aşamada kod değiştirmeden eksiklik raporu oluştursun. Kullanıcı “düzelt” demeden değişiklik yapmasın.

F. Öğrenme güncelleme promptu

Oluştur:

.github/prompts/ib-transaction-playbook-guncelle.prompt.md

Bu prompt, yeni bir transaction tamamlanıp kullanıcı tarafından doğru kabul edildiğinde:

* Yeni transaction’ı mevcut PLAYBOOK ile karşılaştırsın.
* Yalnızca gerçekten yeni ve tekrar kullanılabilir desenleri belirlesin.
* PLAYBOOK’u gereksiz büyütmeden güncellesin.
* Transaction’ı EXAMPLES indeksine eklesin.
* Tek işe özgü business bilgilerini genel kural yapmasın.
* MFA ile ilgili hiçbir bilgiyi eklemesin.

9. Minimum kullanıcı sorusu politikası

Amaç kullanıcıdan minimum yanıt beklemektir.

Aşağıdaki bilgiler koddan veya en yakın örnekten güvenilir biçimde çıkarılabiliyorsa sorma:

* Dosya yolları
* Namespace
* Base class
* Master page
* Kontrol türleri
* Standart butonlar
* Navigation
* State taşıma yöntemi
* Servis client oluşturma yöntemi
* Hata gösterim yöntemi
* Resource dosyasının konumu
* Test dosyasının konumu
* İsimlendirme biçimi
* Registration yöntemi

Yalnızca aşağıdaki gibi gerçekten engelleyici durumlarda soru sor:

* Kullanılacak servis operasyonu birden fazla ihtimale sahipse
* Servis contract’ı bulunamıyorsa
* İş kuralı talep ve koddan çıkarılamıyorsa
* Transaction veya yetki kodu dış sistemden verilmek zorundaysa
* Aynı güçte fakat çelişkili iki güncel mimari varsa
* Veritabanında geri dönüşü zor veya production etkili işlem gerekiyorsa
* Güven seviyesi %95’in altındaysa

Sorulacak bütün soruları tek seferde, kısa ve numaralı şekilde sor.

Engelleyici olmayan belirsizliklerde:

* En yakın güncel çalışan örneği kullan.
* Yaptığın varsayımı sonuç raporunda belirt.
* İşlemi durdurma.

10. Anahtar teslim tamamlanma ölçütü

Bir transaction ancak aşağıdakilerin tamamı sağlandığında bitmiş sayılır:

* Start sayfası çalışıyor.
* Confirm sayfası doğru bilgileri gösteriyor.
* Execute sayfası doğru servisi çağırıyor.
* Üç sayfa arasındaki state/model aktarımı çalışıyor.
* Request mapping tamamlanmış.
* Response ve hata yönetimi tamamlanmış.
* Validasyonlar mevcut standartla uyumlu.
* Geri/iptal/tekrar postback davranışları kontrol edilmiş.
* Double-click veya tekrar execute riski mevcut standartla yönetilmiş.
* Gerekli resource kayıtları eklenmiş.
* Gerekli menü/yetki/transaction kayıtları eklenmiş.
* Gerekli configuration ve registration işlemleri yapılmış.
* Yeni dosyalar doğru path ve namespace’te.
* Proje derleniyor.
* İlgili testler geçiyor.
* Yeni warning/error oluşturulmamış.
* İlgisiz dosyalar değiştirilmemiş.
* MFA veya Seal MFA eklenmemiş.
* Değişikliklerin tamamı talep kapsamıyla ilişkili.

11. Token tasarrufu

Sonraki transaction taleplerinde:

* Önce yalnızca PLAYBOOK’u oku.
* Tüm repository’yi yeniden tarama.
* PLAYBOOK’taki kesin dosya ve symbol’lerden başla.
* EXAMPLES dosyasını yalnızca gerekirse oku.
* Git geçmişine yalnızca düşük güven veya yeni varyant varsa git.
* Dosyanın tamamı yerine ilgili symbol ve bölümleri aç.
* Büyük kod parçalarını konuşma cevabına kopyalama.
* Uzun analiz günlüğü üretme.
* Aynı bilgiyi tekrar etme.
* İlgisiz build uyarılarını açıklama.
* Formatlama kaynaklı büyük diff oluşturma.
* Sonuç raporunu kısa tut.

12. Bu öğrenme aşamasında yapılmayacaklar

Bu ilk çalışmada:

* Yeni business transaction geliştirme.
* Mevcut transaction kodlarını değiştirme.
* Refactor yapma.
* Dependency güncelleme.
* Production configuration değiştirme.
* Veritabanında script çalıştırma.
* Commit/push/PR oluşturma.
* MFA dokümanlarını değiştirme.

Yalnızca mevcut yapıyı incele ve belirtilen doküman/prompt dosyalarını oluştur.

13. Sonuç raporu

İşlem sonunda yalnızca şunları bildir:

* İncelenen transaction sayısı
* İncelenen transaction türleri
* Tespit edilen start → confirm → execute deseni
* Oluşturulan/güncellenen dosyalar
* Otomatik çıkarılabilecek parametreler
* Kullanıcıdan alınması zorunlu parametreler
* Build/test komutlarının bulunup bulunmadığı
* Çelişkili veya belirsiz mimari noktalar
* Gelecek transaction için kullanılacak komutlar

Ayrıntılı analizi sohbet mesajında tekrarlama; oluşturduğun kalıcı dosyalarda tut.