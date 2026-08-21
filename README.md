Verdiğim nesne adını projede bul, türünü belirle, kurallara göre denetle ve onayım olmadan hiçbir kaynak kodu değiştirme.

NESNE_ADI: [BURAYA_NESNE_ADINI_YAZ]

1. Kalıcı kural dosyası

Önce proje kökündeki .github/WALL_DTO_RULES.md dosyasını kontrol et.

Dosya varsa

* Dosyayı oku ve ana kural kaynağı olarak kullan.
* Kuralları keşfetmek için projeyi yeniden genel taramadan geçirme.
* Yalnızca verilen nesneyi, doğrudan ilişkili sınıfları ve gerekli kullanım noktalarını incele.
* Yeni ve açık bir kural tespit edersen doğrudan ekleme; raporda “önerilen yeni kural” olarak belirt.

Dosya yoksa

Projede kullanılan WALL ve DTO nesnelerinden güncel ve temsil gücü yüksek örnekleri incele.

Şu kaynaklara öncelik ver:

* Proje dokümantasyonu
* .editorconfig ve analyzer ayarları
* Aynı klasör ve namespace içindeki nesneler
* Base class ve interface tanımları
* Mapping kodları
* Güncel ve yaygın kullanılan WALL/DTO örnekleri
* İlgili testler

Aşağıdaki kuralları ayrı ayrı keşfet:

* Bir nesnenin WALL veya DTO olarak sınıflandırılma ölçütleri
* Class ve dosya adlandırması
* Değişken, property ve metot adlandırması
* Property türleri ve null kullanılabilirliği
* Erişim belirleyicileri
* Constructor kullanımı
* Collection/list tanımlama kuralları
* Eleman sayısı bilinen listelerde başlangıç kapasitesi verilmesi
* Attribute ve annotation kullanımı
* Kalıtım ve interface kuralları
* Mapping kuralları
* Serialization kuralları
* Validation kuralları
* WALL nesnelerine özel kurallar
* DTO nesnelerine özel kurallar
* Yasaklanan veya bulguya neden olan kullanımlar

Tespit edilen kuralları .github/WALL_DTO_RULES.md dosyasına yaz.

Her kural şu yapıda olsun:

* Kural kimliği: WALL-XXX, DTO-XXX veya COMMON-XXX
* Kural açıklaması
* Uygulandığı nesne türü
* Doğru kullanım örneği
* Yanlış kullanım örneği
* Kaynak dosya ve satır referansı
* Güven seviyesi: Kesin / Güçlü / Aday
* Bulgu önem seviyesi: Kritik / Yüksek / Orta / Düşük

Tek bir örneğe bakarak kural üretme. Emin olmadığın kuralları “Aday” olarak kaydet ve kesin bulgu üretmek için kullanma.

Kural dosyasını oluşturduktan sonra sonraki çalışmalarda projeyi yeniden genel olarak tarama.

2. Verilen nesneyi bul

NESNE_ADI değerini kullanarak:

* Nesnenin tanımlandığı dosyayı bul.
* Aynı isimde birden fazla nesne varsa namespace ve kullanım yerlerini karşılaştır.
* Doğru nesneyi kesin belirleyemiyorsan seçenekleri gösterip bana sor.
* Dosyanın tamamını ve yalnızca gerekli doğrudan ilişkili kodları incele.
* Gereksiz klasörleri ve tüm projeyi tarama.

3. Nesnenin türünü belirle

Nesnenin WALL mı DTO mu olduğunu yalnızca adına bakarak belirleme.

Şu kanıtları birlikte değerlendir:

* Bulunduğu proje ve klasör
* Namespace
* Base class
* Uyguladığı interface’ler
* Attribute/annotation bilgileri
* Mapping işlemleri
* Metot parametresi veya dönüş tipi olarak kullanımı
* Benzer nesnelerin yapısı
* Projede tanımlanan WALL ve DTO kuralları

Sonuçta şunları bildir:

* Belirlenen tür: WALL / DTO / Belirsiz
* Güven seviyesi: Yüksek / Orta / Düşük
* Türü belirlemekte kullanılan kısa kanıtlar

Tür kesin belirlenemiyorsa tahmin ederek denetime devam etme; bana sor.

4. Nesneyi denetle

Nesne WALL ise yalnızca:

* COMMON-*
* WALL-*

kurallarını uygula.

Nesne DTO ise yalnızca:

* COMMON-*
* DTO-*

kurallarını uygula.

Şunları kontrol et:

* Class adı ve dosya adı
* Değişken ve property adları
* Metot adları ve imzaları
* Property türleri
* Null tanımlamaları
* Collection/list kullanımları
* Başlangıç kapasitesi verilmesi gereken listeler
* Constructor yapısı
* Attribute/annotation kullanımları
* Mapping uyumu
* Validation
* Serialization
* Erişim belirleyicileri
* Kullanılmayan üyeler
* Projeye özel diğer WALL/DTO kuralları

Sadece nesnenin kendisindeki ve doğrudan bu nesneden kaynaklanan bulguları raporla. İlişkisiz proje bulgularını rapora ekleme.

5. Onay öncesi rapor

Bu aşamada hiçbir kaynak kodu değiştirme.

Bulguları şu tabloda göster:

No	Kural	Önem	Dosya:Satır	Bulgu	Önerilen düzeltme

Tablodan sonra şunları ayrıca yaz:

* Nesne türü
* İncelenen ana dosya
* Toplam bulgu sayısı
* Kritik/yüksek/orta/düşük dağılımı
* Değiştirilecek dosyalar
* Davranış değişikliği riski
* Önerilen yeni aday kurallar

Bulgu yoksa açıkça “Bu nesnede mevcut kurallara göre bulgu bulunamadı” yaz.

Raporun sonunda dur ve yalnızca şu soruyu sor:

Listelenen düzeltmeleri uygulamamı onaylıyor musunuz?

6. Onay verilirse

Ben açıkça onay vermeden:

* Kaynak kodu değiştirme.
* Otomatik düzeltme çalıştırma.
* Refactoring yapma.
* İlgisiz dosyalara dokunma.

Onay verirsem:

1. Yalnızca raporda listelenen ve onaylanan bulguları düzelt.
2. Nesnenin mevcut işlevsel davranışını değiştirme.
3. İlgisiz kodu biçimlendirme veya yeniden düzenleme.
4. Mevcut kullanıcı değişikliklerini koru.
5. Uygun testleri çalıştır.
6. Mümkünse projeyi derle.
7. Yeni hata oluşup oluşmadığını kontrol et.
8. Sonuçta değiştirilen dosyaları ve yapılan düzeltmeleri kısa şekilde bildir.
9. Her düzeltmeyi ilgili kural kimliğiyle eşleştir.

Bağlam ve token kullanımı

* .github/WALL_DTO_RULES.md mevcutsa kuralları yeniden keşfetme.
* Yalnızca verilen nesneyi ve zorunlu doğrudan bağımlılıklarını incele.
* Build çıktıları, paketler, generated dosyalar ve vendor klasörlerini tarama.
* Uzun kod parçalarını yanıta kopyalama.
* Aynı dosyayı gereksiz yere tekrar okuma.
* Raporu kısa ve bulgu odaklı hazırla.