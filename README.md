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

Business kodunu değiştirme. Sonuçta yalnızca güncellenen dokümanları ve bulunan önemli çelişkileri bildir.