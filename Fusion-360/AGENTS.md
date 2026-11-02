# Fusion 360 çalışma kuralları

[Ortak kurallar](../AGENTS.md) geçerlidir. Yerel Fusion Print altyapısı kullanılıyorsa
[runtime kapsamını](runtime-scope.md) okuyun. Bu public klasör runtime kodunu içermez;
komutları kurulu altyapının repository kökünden çalıştırın.

## Hazırlık ve modelleme

- Canlı işlem öncesi `fusion-print doctor`, ardından `fusion-print ping` çalıştırın.
  Heartbeat tek başına Fusion ana thread'inin yanıt verdiğini kanıtlamaz.
- Yerel model işi `models/<parça>/model.json` ve `recipe.py` ile tanımlanır. Ölçüleri
  önce kaydedin, `fusion-print validate models/<parça>/model.json` çalıştırın.
  Bu görev dosyaları public yönetim reposuna senkronize edilmez.
- Dış uzunluk birimi mm; Fusion `Point3D` uzunlukları cm, hacimler cm³'tür.
  Nokta oluştururken mm değerini 10'a bölün; ölçüm dönüşümünü açıkça yapın.
- Parametrik feature'lar ve adlandırılmış user parameter'lar kullanın; parametrelerin
  gerçek feature ölçülerine bağlı olduğunu doğrulayın.
- Tarif importunda `adsk` çağırmayın. Recipe tek başına kopyalanabilir olmalı;
  göreli import kullanmayın. `inspect()` geometriyi değiştirmemelidir.
- Aynı üretim parçasını bir component olarak tanımlayın, tekrarlarını occurrence
  olarak yerleştirin. Karşı taraf için önce döndürme/taşıma eşdeğerliğini kontrol
  edin; gerçek sağ/sol farkı gerekiyorsa ilişkili mirror kullanın.

## API ve denetim

- Fusion API yalnız ana thread'de çalışır. Worker'a `adsk` sorgusu eklemeyin.
- API adlarını ve koordinat dönüşümlerini kullanmadan önce doğrulayın. İlk sketch
  ve extrusion sonrasında root min/max konumlarını ve yönü ölçün.
- Döndürülmüş sketch'lerde gerçek sketch/model dönüşümünü kullanın. Join/cut için
  hedefi açıkça seçin; profil sayısını doğrulamadan `item(0)` seçmeyin.
- Topoloji değişince yüz/kenarları yeniden sorgulayın; salt sıra indeksine güvenmeyin.
- Timeout sonrası yeni build göndermeyin; aynı ID ile status okuyun. Kesintiye
  uğramış işin belgesini ve artifact'lerini incelemeden yeni ID oluşturmayın.
- Aynı işe ait `inspection.json`, `mesh-inspection.json` ve PNG'leri incelemeden
  model doğrulandı demeyin. Eksik inspection veya export'u eksik/başarısız bildirin.
- Kullanıcının açık belge talebi hedefi belirler. Standart CLI'nin yeni belge açması
  bunu değiştirmez; uygun bir mevcut-belge yöntemi yoksa sınırı açıkça raporlayın.

## Yerel altyapı geliştirme

- Mevcut FusionMCP eklentisi Fusion Print'in bağımlılığı değildir; onu değiştirmeyin.
- Runtime değişince Python import önbelleği nedeniyle Fusion'ı yeniden başlatın.
- Runtime kodu değişirse yerel altyapıda `.venv/Scripts/python -m pytest` ve
  `.venv/Scripts/python -m ruff check .` çalıştırın; canlı testleri ayrı raporlayın.
- Salt public belge güncellemesi için Fusion'a bağlanmak veya model build etmek
  gerekmez. Yerel `.fusion/`, `artifacts/` ve `.venv/` içeriklerini yayımlamayın.
