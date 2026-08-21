/ib-transaction-uygula

TALEP:
[İşin talep metni]

SERVİS BİLGİSİ:
[Varsa servis adı ve metodu]

REFERANS TRANSACTION:
[Varsa benzer işlem]



/ib-transaction-denetle

TALEP:
[İşin asıl talep metni]

KAPSAM:
Mevcut branch’te yapılan değişiklikler

KARŞILAŞTIRMA BRANCH’I:
develop

Önce sadece denetle. Ben onay vermeden kodu değiştirme.



/ib-transaction-ogren

ÖĞRENİLECEK TRANSACTION:
[Transaction adı veya değişiklik yapılan branch]

REFERANS TALEP:
[Talep metni]

Bu transaction tamamlandı ve doğrulandı. Mevcut PLAYBOOK ile karşılaştır; yalnızca yeni ve tekrar kullanılabilir bilgileri öğrenerek dokümanları güncelle.



flowchart LR
    A["Uygula"] --> B["Denetle"]
    B --> C["Sen test et"]
    C --> D["Öğren"]