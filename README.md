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






