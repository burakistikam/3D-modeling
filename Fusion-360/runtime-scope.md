# Yerel Fusion Print altyapısının kapsamı

Bu belge mevcut genel altyapı sözleşmesinin paylaşılabilir özetidir. Runtime ve
kurulum dosyaları bu repoda bulunmaz. Kurulu sürümün davranışını çalışma öncesinde
doğrulayın. Çalışma kuralları [AGENTS.md](AGENTS.md) içindedir.

## İş akışı

Yerel CLI/MCP istemcisi dosya kuyruğuna iş yazar. Fusion eklentisinin worker'ı
dosya IO ve custom event ile işi ana thread'e aktarır; CAD API çağrıları burada
çalışır. Tarif, CAD inspection ve başarılıysa F3D/STEP/STL ile görünüş çıktıları
üretilir. STL denetimi Fusion dışında yapılır.

Dosya kuyruğu güvenilen yerel kullanıcı ve checkout varsayar; bir sandbox veya
çok kullanıcılı servis değildir. Tarif güvenilen Python kodudur. İçe aktarırken
yan etki üretmemeli, çalıştırılmadan önce incelenmelidir.

## Destek sınırları

- Standart build yeni belgede root BRep gövdeleri üretir. Açık belge düzenleme,
  assembly denetimi ve yalnız CAD export/inspection için ayrı standart komut yoktur.
- Genel CAD gate'i root gövdeleri destekler; occurrence içeren assembly'yi genel
  gate doğrulamış gibi göstermeyin. Yetkili assembly işi ayrı denetim gerektirir.
- `validate(parameters)` çevrimdışı parametre kontrolüdür; canlı geometriyi doğrulamaz.
  `build(context, parameters)` geometri oluşturur; `inspect(context, parameters)`
  salt okunur kontrol yapar ve boş olmayan `{kontrol_adı: bool}` sonucu döndürür.
- Boyutlara ek olarak beklenen min/max konumu görev niyetinden belirlenmelidir.
  Beklenen ölçüleri son çıktının kendisinden türetmeyin. İç geometriyi ayrıca ölçün.
- Her iş kimliği en fazla bir kez çalıştırılır. Bekleme timeout'u CAD işlemini
  iptal etmez. Başlamış veya kesintiye uğramış işi otomatik yeniden göndermeyin.
- Bir checkout için tek Fusion Print örneği varsayılır. Ortak runtime'ı çalışan
  iş sırasında değiştirmeyin; aynı canlı modele paralel yazma göndermeyin.
- Otomatik undo, kullanıcı belgesini kapatma, cloud save veya eski modeli silme
  standart akışın parçası değildir. Hata belgesini inceleme için koruyun.

## Kanıtın anlamı

CAD denetimi gövde sayısı, katılık, pozitif hacim, boyut/konum, timeline sağlığı ve
tarife özgü ölçümleri kapsar. Mesh denetimi kapalı mesh, winding, hacim, shell,
dejenere yüzler ve CAD ile ölçü eşleşmesini inceler. Bunlar genel minimum duvar,
overhang, dayanım, slicer veya CAM onayı değildir. Kanıtı ilgili iş ve revizyonla
eşleştirin; sonraki geometri değişikliği önceki raporu güncel kanıt yapmaz.
