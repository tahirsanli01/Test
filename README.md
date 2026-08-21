Yalnızca Mobil projesini incele. İB, Seal MFA, MFA ve OTP kapsam dışıdır.

Amaç: Yeni Mobil transaction’ları minimum kullanıcı sorusuyla geliştirebilmek için kalıcı ve kısa bir çalışma hafızası oluşturmak.

Token tasarrufu kuralları:

* Repository’yi topluca okuma.
* Önce dosya adları ve symbol aramasıyla transaction yapısını tespit et.
* En güncel, çalışan ve MFA içermeyen yalnızca 3 temsilî transaction incele.
* Her transaction’da yalnızca ilgili ekran, navigation, state, service/API, model, mapper, validation, resource ve test dosyalarını aç.
* Büyük kod bloklarını çıktıya kopyalama.
* Git geçmişini yalnızca dosya ilişkisini anlayamazsan kullan.
* İş kodunu değiştirme.

Şunları öğren:

* Mobil teknoloji ve mimari
* Transaction’ın giriş, form, onay, servis çağrısı ve sonuç akışı
* Ekranlar arası veri taşıma
* Navigation
* State yönetimi
* Servis/API bağlantısı
* Request/response mapping
* Validation ve hata yönetimi
* Loading ve tekrar gönderim kontrolü
* Resource/configuration
* Yeni dosya path, isim ve package/namespace kuralları
* Test, lint ve build komutları

Sonucu şu dosyaya yaz:

docs/copilot/mobile-transaction/PLAYBOOK.md

Her kuralda kısa kanıt kullan:

dosya yolu | symbol | yaklaşık satır | örnek transaction

PLAYBOOK en fazla 200 satır ve mümkünse 2.500 token olsun. Tekrar ve genel yazılım açıklaması ekleme. Sohbet cevabında yalnızca incelenen 3 transaction’ı ve oluşturulan dosyayı bildir.