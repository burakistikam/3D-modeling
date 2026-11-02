# Blender çalışma kuralları

[Ortak kurallar](../AGENTS.md) geçerlidir. Bu dosya başlangıç yönetim rehberidir;
belirli bir Blender sürümünde test edilmiş bir otomasyon paketi değildir.

## Hedef ve sahne

- Mevcut bağlantı araçlarını keşfedin; hedef `.blend` dosyasını, scene, view layer,
  aktif obje, seçim ve çalışma modunu salt okunur sorguyla doğrulayın.
- Sahne birim sistemi, unit scale ve obje transform'larını ölçülerden önce kontrol
  edin. Görünen ölçü etiketi ile gerçek geometri/export ölçeğini ayırın.
- Var olan sahnede çalışırken yedek alın. Sahnedeki bütün objeleri varsayılan olarak
  silmeyin; yalnız görevin hedef objelerine ve collection'larına yazın.

## Modelleme

- Obje, collection, materyal ve modifier'lara anlamlı adlar verin. Tekrarlar için
  uygun olduğunda linked data veya instance kullanın.
- Modifier ve Geometry Nodes yapısını düzenlenebilir bırakın. Apply, remesh,
  convert veya transform uygulama işlemlerini yalnız gereklilik varsa yapın;
  kaynak geometriyi ve instance ilişkilerine etkisini koruyun veya belgeleyin.
- Script yazmadan önce kurulu API'yi ve operator bağlamını doğrulayın. Aktif obje,
  seçim ve moda bağlı davranışları açıkça yönetin; deneme işlemini küçük tutun.
- Boolean, mirror ve scale sonrası normal yönlerini, transform'ları ve amaçlanan
  boyutu sorgulayın. Shading ile geometri hatalarını birbirine karıştırmayın.
- Dış texture, font, addon ve asset'leri yalnız görev gerektiriyorsa kullanın;
  teslimde lisans ve bağımlılık durumunu belirtin, özel asset'leri yayımlamayın.

## Teslim kontrolü

- İstenen görünüm veya üretim amacına göre ölçü, yerleşim, görünürlük ve modifier
  sonucunu doğrulayın. Render başarısı fiziksel geometri doğrulaması değildir.
- Baskı için non-manifold kenarlar, normal yönü, iç yüzler, kesişimler, duvar ve
  boşlukları uygun yöntemle inceleyin. Slicer incelemesini ayrı raporlayın.
- Export'ta eksen, birim, scale ve modifier uygulanma durumunu kaydedin; mümkünse
  yeniden içe alma/okuma ile kritik ölçüyü kontrol edin.
- `.blend`, export ve görsel kanıtları özel görev alanına kaydedin. Public yönetim
  reposuna sahne, render, texture, cache veya otomatik yedek eklemeyin.
