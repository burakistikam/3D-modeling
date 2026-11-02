# Rhino çalışma kuralları

[Ortak kurallar](../AGENTS.md) geçerlidir. Bu dosya başlangıç yönetim rehberidir;
kurulu Rhino sürümü veya belirli bir MCP aracının yetenekleri hakkında garanti vermez.

## Çalışma öncesi

- Mevcut bağlantı araçlarını keşfedin; belge kimliği, birim sistemi, mutlak/açısal
  tolerans ve aktif çalışma düzlemini salt okunur sorguyla doğrulayın.
- Hedef belgenin yedeğini alın. Nesne kimliklerini ve değiştirilecek katmanları
  belirleyin; kullanıcı nesnelerini yalnız görünümde seçili oldukları için değiştirmeyin.
- Ölçek ile birim etiketini ayırın. Birim değiştirme veya import sırasında
  geometri ölçeklenip ölçeklenmediğini bilinen bir ölçüyle kontrol edin.

## Modelleme

- Eğri, yüzey, polysurface, SubD veya mesh seçimini istenen teslim biçimine göre
  yapın; dönüşümün düzenlenebilirlik ve hassasiyet etkisini belirtin.
- Mantıksal katman ve nesne adları kullanın. Tekrarlanan parçalar için uygun
  olduğunda block instance kullanın; bağımsız kopya ancak geometri ihtiyacıyla yapılır.
- Join/boolean öncesi eğri kapanışlarını, toleransı ve kesişimleri kontrol edin.
  Başarısız işlemi çözmek için belge toleransını gerekçesiz gevşetmeyin.
- Komut veya API dönüşünün başarılı olması son geometriyi kanıtlamaz. Çıktı
  nesnelerini sorgulayın; silinen, eklenen ve değişen nesneleri izleyin.
- Grasshopper kullanılıyorsa definition ve parametreleri düzenlenebilir tutun;
  bake işleminin hangi nesneleri ürettiğini izleyip yinelenen üretimi önleyin.

## Teslim kontrolü

- Kritik ölçüleri, konumları, nesne/gövde sayısını ve hedef toleransı kontrol edin.
- Katı bekleniyorsa kapalı geçerli geometriyi, naked/non-manifold kenarları ve
  hacmi inceleyin; açık yüzey istenmişse onu gereksiz yere katıya zorlamayın.
- Mesh export'ta tessellation ayarlarını, birimi, yönü ve manifold durumunu
  doğrulayın. Görüntüde düzgün görünmek üretim uygunluğu kanıtı değildir.
- İstenen `.3dm` ve export'ları ayrı özel çalışma alanına kaydedin; yeniden okuma
  ve görsel kontrol sonucunu raporlayın. Bu public repoya model veya kanıt yüklemeyin.
