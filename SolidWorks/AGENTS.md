# SolidWorks çalışma kuralları

[Ortak kurallar](../AGENTS.md) geçerlidir. Parça ve montaj tasarımı için
[solidworks-design skill](skills/solidworks-design/SKILL.md) ve yalnız görevle
ilgili destek belgelerini okuyun. Teknik resim ayrı bir görev kapsamıdır.

- Hedef dosyayı, belge türünü, aktif konfigürasyonu ve birimleri doğrulayın.
- Düzenlenebilir native feature'ları ve konfigürasyona özel ölçü/mate ilişkilerini
  koruyun; donanım ve tekrarlar için aynı kaynak parça tanımını kullanın.
- Özgün konumu gerektiğinde referans konfigürasyonunda koruyun. Hareket göstermek
  amacıyla mevcut parça/donanımı bağımsız kopyalarla çoğaltmayın.
- Sadeleştirilmiş satın alınan donanımı `ENVELOPE_ONLY` olarak işaretleyin.
- Kaydetme sonrası rebuild, hata/uyarı, kritik ölçü, konfigürasyon ve kayıt durumunu
  geri okuyun. Başarılı bir yazma çağrısı tek başına teslim doğrulaması değildir.
- Worker/Reviewer akışı yalnız kullanıcı veya geçerli çalışma alanı talimatı
  gerektiriyorsa kullanılır. Bağımsız ajan incelemesi yapılmadıysa yapılmış demeyin.
- CAD dosyaları, görev çıktıları ve geçici COM yardımcıları özel çalışma alanında
  kalır. Public repoya yalnız incelenmiş genel kurallar ve skill içeriği eklenir.
