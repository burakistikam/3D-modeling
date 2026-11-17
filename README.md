# 3D modeling

Fusion 360, Rhino, SolidWorks ve Blender kullanan yapay zekalar için ortak kaynak:
ajan kuralları, yeniden kullanılabilir skill'ler ve taşınabilir bağlantı bilgileri.
CAD modelleri, görev kayıtları, çıktılar ve çalışan yerel runtime bu repoya kaydedilmez.

## Kullanım

Önce [ortak kuralları](AGENTS.md), ardından hedef uygulamanın kurallarını okuyun.
Kurulum ve bağlantı için [bağlantı rehberini](connections.md) kullanın.

| Uygulama | Kurallar | Skill / teknik kapsam |
|---|---|---|
| Fusion 360 | [AGENTS.md](Fusion-360/AGENTS.md) | [Fusion Print skill](Fusion-360/skills/fusion-print/SKILL.md), [runtime kapsamı](Fusion-360/runtime-scope.md) |
| Rhino | [AGENTS.md](Rhino/AGENTS.md) | Uygulamaya özgü çalışma kuralları |
| SolidWorks | [AGENTS.md](SolidWorks/AGENTS.md) | [solidworks-design](SolidWorks/skills/solidworks-design/SKILL.md) |
| Blender | [AGENTS.md](Blender/AGENTS.md) | Uygulamaya özgü çalışma kuralları |

## Tek kaynak ve yerel çalışma

- Genel kurallar ve skill içeriği bu repoda düzenlenir. Proje klasöründeki kısa
  yönlendirme dosyası ortak ve ilgili uygulama kurallarına bağlanır; bunları kopyalamaz.
- Kurulu skill için aynı skill'in ikinci bir varyantını oluşturmayın. Mevcut
  kurulum noktasını bu kaynağa bağlayın veya tek kurulu kopyayı kontrollü güncelleyin.
  Yerel plugin hook'ları ve MCP sunucusu ayrı altyapıdır; körlemesine değiştirmeyin.
- Repo yolu, Python/uygulama yolları, MCP komutları ve özel çıktı kökleri makineye
  özgü config'te tutulur. Paylaşılan örneklerde yer tutucular kullanılır.
- Runtime, sanal ortamlar, eklentiler ve özel görev klasörleri repo dışında yaşar.
  Bu repo bir CAD uygulaması veya MCP sunucusu kurmaz; başka bir kaynak reposunun
  varlığına da dayanmaz. Yerel runtime çalışmak için Git metadata'sı gerektirmez.
- Güncelleme gerektiğinde yerel ve public yöntemleri karşılaştırarak birleştirin:
  tekrarları kaldırın, çelişkileri çözün ve çalışan bağlantıları doğrulayın.

## Güncelleme ve paylaşım

Public hedef: [burakistikam/3D-modeling](https://github.com/burakistikam/3D-modeling).
Yalnız bu kapsamda gerçek değişiklik olduğunda [yayın akışını](AGENTS.md#geliştirme-sonunda-github-senkronizasyonu)
uygulayın. Model kaydetmek veya bir CAD görevini bitirmek tek başına commit/push
gerektirmez; otomatik dosya senkronizasyon servisi yoktur.

İzin listesindeki dosyaları ve commit içeriğini inceleyin. Müşteri verisi, tasarım,
ölçü, görsel, export, oturum kaydı, makineye özel yol veya kimlik bilgisi yayımlamayın.
