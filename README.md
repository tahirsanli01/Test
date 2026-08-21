Önce yalnızca docs/copilot/mobile-transaction/PLAYBOOK.md dosyasını oku.

PLAYBOOK’un doğruluğunu kontrol etmek için daha önce incelenmeyen, güncel ve MFA içermeyen en fazla 2 Mobil transaction incele.

Repository’yi baştan tarama. Yalnızca PLAYBOOK ile çelişen veya eksik görünen konuların ilgili dosya ve symbol’lerini aç.

Yapılacaklar:

1. Kanıtlanan eksikleri PLAYBOOK’a ekle.
2. Yanlış genellemeleri düzelt.
3. Eski mimariyi güncel standart olarak kaydetme.
4. Tek transaction’a özgü business bilgisini genel kural yapma.
5. İB, MFA, Seal MFA veya OTP bilgisi ekleme.
6. PLAYBOOK’u 200 satır civarında tut.
7. Büyük kod örneği ekleme.

İncelenen toplam 5 transaction için kısa indeks oluştur:

docs/copilot/mobile-transaction/EXAMPLES.md

Tablo:

| Transaction | Tür | Ana ekranlar | Navigation/state | Service/API | Önemli dosyalar |

Business kodunu değiştirme. Sonuçta yalnızca güncellenen dokümanları ve bulunan önemli çelişkileri Yalnızca şu dosyaları oku:

* docs/copilot/mobile-transaction/PLAYBOOK.md
* docs/copilot/mobile-transaction/EXAMPLES.md

Repository’yi veya Git geçmişini yeniden tarama.

Bu bilgilerden aşağıdaki kısa prompt dosyalarını oluştur:

1. .github/prompts/mobile-transaction-uygula.prompt.md
2. .github/prompts/mobile-transaction-denetle.prompt.md
3. .github/prompts/mobile-transaction-ogren.prompt.md
4. docs/copilot/mobile-transaction/USAGE.md

uygula promptu:

* Talep, servis bilgisi ve referans transaction girdilerini alsın.
* Önce PLAYBOOK’u okusun.
* Koddan çıkarılabilen bilgileri kullanıcıya sormasın.
* Yalnızca engelleyici soruları tek seferde sorsun.
* Ekran, navigation, state, API, mapping, validation, resource, test, lint ve build dahil anahtar teslim geliştirsin.
* İB veya MFA eklemesin.

denetle promptu:

* Talep, kapsam ve karşılaştırma branch’i girdilerini alsın.
* Önce kod değiştirmeden eksiklik raporu oluştursun.
* Dosya ve symbol kanıtı göstersin.
* Test, lint ve build sonuçlarını bildirsin.
* Kullanıcı “düzelt” demeden değişiklik yapmasın.

öğren promptu:

* Yalnızca kullanıcı tarafından doğrulanmış transaction’larda çalışsın.
* Yeni ve tekrar kullanılabilir bilgileri PLAYBOOK’a eklesin.
* Transaction’ı EXAMPLES’a eklesin.
* PLAYBOOK’u gereksiz büyütmesin.
* Business kodunu değiştirmesin.

Her prompt kısa ve mümkünse 800 tokenın altında olsun.

USAGE.md içerisinde üç komutun ne zaman ve hangi sırayla çalıştırılacağını, kopyalanabilir kısa örneklerle göster.

Mevcut .github/copilot-instructions.md dosyasını silme. Yalnızca şu kısa yönlendirmeyi uygun yere ekle:

“Mobil transaction işlerinde önce docs/copilot/mobile-transaction/PLAYBOOK.md okunmalı; İB ve MFA yapıları kapsam dışıdır.”

Sohbet cevabında oluşturulan dosyaları listelemek dışında ayrıntı verme.





Bu projedeki yazım, kodlama ve performans kurallarını keşfet; kalıcı olarak belgele ve otomatik denetlenebilir hâle getir.

Amaç

Projede kullanılan:

* Değişken, sabit, property, metot, class, interface ve dosya adlandırma kuralları
* Collection/list tanımlama kuralları
* Liste oluşturulurken mümkünse başlangıç kapasitesi verilmesi
* Metot ve class yapısı
* Erişim belirleyicileri
* Null kontrolü
* Exception yönetimi
* Logging
* Kaynak yönetimi
* Async kullanımı
* Performans kuralları
* Güvenlik kuralları
* Kod tekrarları
* Yasaklanan kullanım biçimleri
* Statik analiz veya kalite kontrol kuralları

gibi standartları tespit et.

Çalışma şekli

1. Önce proje teknolojisini ve klasör yapısını belirle.
2. Tüm dosyaları ayrıntılı biçimde okumak yerine önce şu kaynakları incele:
    * README ve dokümantasyon dosyaları
    * .editorconfig
    * Linter/analyzer ayarları
    * Build dosyaları
    * Sonar, StyleCop, Roslyn, ESLint veya eşdeğer yapılandırmalar
    * Ortak/base class’lar
    * Helper ve utility sınıfları
    * Benzer iş yapan, güncel ve yoğun kullanılan örnek dosyalar
    * Varsa test projeleri
3. Kuralları tek bir dosyadan tahmin etme. Birden fazla güncel örnekte tekrar eden uygulamaları karşılaştır.
4. Eski kod, istisnai kod veya tesadüfi kullanım biçimlerini genel kural olarak kabul etme.
5. Kesin kanıt bulunmayan kuralları uydurma. Bunları “aday kural” olarak işaretle.
6. Mevcut proje dosyalarını bu aşamada değiştirme.

Oluşturulacak belgeler

Proje kökünde .github/copilot-instructions.md oluştur veya mevcutsa dikkatlice güncelle.

Ayrıca docs/CODING_RULES.md oluştur. Her kural için şunları yaz:

* Kural kimliği
* Kategori
* Kural açıklaması
* Doğru kullanım örneği
* Yanlış kullanım örneği
* Kuralın tespit edildiği dosya ve satır aralığı
* Güven seviyesi: Kesin / Güçlü / Aday
* Otomatik denetlenebilir mi?
* İhlal önem seviyesi: Kritik / Yüksek / Orta / Düşük
* Önerilen düzeltme

Örnek olarak şu kuralı özellikle araştır:

Bir listenin alacağı yaklaşık eleman sayısı önceden biliniyorsa liste başlangıç kapasitesi belirtilmelidir.

Ancak bunu doğrudan kesin proje kuralı kabul etme; proje kodunda, analiz ayarlarında veya dokümantasyonda kanıt ara.

Otomatik denetim

Projenin teknolojisine uygun bir denetim çözümü oluştur:

* Hazır analyzer/linter ile güvenilir şekilde denetlenebilen kurallar için mevcut aracı yapılandır.
* Hazır araçla denetlenemeyen proje özel kuralları için mümkünse özel analyzer/linter veya denetim scripti oluştur.
* C#/.NET ise tercihen Roslyn Analyzer kullan.
* JavaScript/TypeScript ise ESLint custom rule kullan.
* Java/Kotlin ise uygun statik analiz altyapısını kullan.
* Başka bir teknoloji ise projeye en uygun, build sürecine eklenebilen çözümü seç.
* Regex ile kod analizi yalnızca güvenilir parser/analyzer seçeneği yoksa kullan.
* Denetim aracı varsayılan olarak yalnızca rapor üretmeli; kodu otomatik değiştirmemelidir.
* Her özel kural için en az bir uygun kod ve bir ihlal testi ekle.

Denetim raporu

Mevcut projeyi belirlenen kesin ve güçlü kurallara göre denetle ve reports/CODING_RULES_AUDIT.md oluştur.

Her bulguda şunları göster:

* Kural kimliği
* Önem seviyesi
* Dosya yolu
* Satır numarası
* İhlal açıklaması
* Mevcut kodun kısa özeti
* Önerilen düzeltme
* Otomatik düzeltilebilir mi?

Aynı ihlalleri tek tek uzun biçimde tekrar etme; kural bazında grupla ve toplam sayıyı belirt.

Bağlam ve token tasarrufu

* Daha önce oluşturulan docs/CODING_RULES.md güncelse projeyi tekrar tamamen tarama.
* Sonraki çalışmalarda önce bu belgeyi ve değişen dosyaları oku.
* Belgedeki her kuralın kaynak dosya referanslarını sakla.
* Yalnızca değişen, yeni veya ilgili dosyaları yeniden incele.
* Gereksiz dosya içeriklerini yanıta taşıma.
* Büyük üretilmiş dosyaları, bağımlılık klasörlerini, build çıktılarını ve vendor dosyalarını inceleme.
* Bir dosyayı tekrar okumadan önce daha önce kaydedilmiş bilginin yeterli olup olmadığını kontrol et.

Güvenlik

* İş mantığını değiştirme.
* Mevcut kullanıcı değişikliklerini ezme.
* Derleme veya test hatası bulunan projede önce hatanın senden önce var olup olmadığını kontrol et.
* Kuralları otomatik düzeltme; yalnızca denetim altyapısını ve raporları oluştur.
* Emin olunmayan bulguları kesin ihlal olarak raporlama.

Doğrulama

İşlem sonunda:

1. Oluşturulan denetim aracını çalıştır.
2. Analyzer/linter testlerini çalıştır.
3. Mümkünse projeyi derle.
4. Yanlış pozitif olabilecek bulguları ayır.
5. Belgelerdeki dosya ve satır referanslarını doğrula.

Son yanıt

Uzun açıklama yapma. Yalnızca şunları bildir:

* Tespit edilen kesin/güçlü/aday kural sayıları
* Oluşturulan veya değiştirilen dosyalar
* Bulgu sayılarının önem seviyesine göre özeti
* Çalıştırılan doğrulamalar ve sonuçları
* İnsan kararı gereken aday kurallar
* Denetimi yeniden çalıştırmak için tek komut

Eksik bilgi gerektiğinde yalnızca ilerlemeyi gerçekten engelleyen tek bir soru sor. Diğer konularda projedeki kanıtlara göre karar ver ve işlemi tamamla.





