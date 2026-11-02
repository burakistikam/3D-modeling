# 3D modeling

Fusion 360, Rhino, SolidWorks ve Blender için paylaşılabilir ajan çalışma kuralları.
Bu public repository yönetim belgeleri ve yeniden kullanılabilir skill içerir.
CAD modelleri, müşteri işleri, oturum kayıtları ve yerel bağlantı ayarları içermez.

## Kullanım

Önce [ortak kuralları](AGENTS.md), ardından kullanılan uygulamanın kurallarını okuyun.
Uygulama klasörleri kendi çalışma alanlarına taşınırsa ortak kuralları da taşıyın
ve göreli bağlantıları yeni konuma uyarlayın.

| Uygulama | Yönetim dosyası | Ek kaynak |
|---|---|---|
| Fusion 360 | [AGENTS.md](Fusion-360/AGENTS.md) | [Yerel altyapının kapsamı](Fusion-360/runtime-scope.md) |
| Rhino | [AGENTS.md](Rhino/AGENTS.md) | Başlangıç çalışma kuralları |
| SolidWorks | [AGENTS.md](SolidWorks/AGENTS.md) | [solidworks-design skill](SolidWorks/skills/solidworks-design/SKILL.md) |
| Blender | [AGENTS.md](Blender/AGENTS.md) | Başlangıç çalışma kuralları |

Fusion 360 kuralları mevcut genel proje talimatlarından, SolidWorks skill'i mevcut
kişisel tasarım skill'inin paylaşılabilir yöntemlerinden uyarlanmıştır. Rhino ve
Blender kuralları başlangıç rehberidir; canlı uygulamada test edilmiş bir otomasyon
paketi oldukları iddia edilmez. Bu repo uygulamaları, MCP sunucularını, Fusion Print
runtime'ını veya otomatik çalışan bir senkronizasyon servisini kurmaz.

## Public paylaşım ve senkronizasyon

Codex ile her geliştirme tamamlandığında, paylaşılabilir yönetim/skill değişiklikleri
kontrol edilerek commit ve push yapılır. Kalıcı işlem adımları
[AGENTS.md](AGENTS.md#geliştirme-sonunda-github-senkronizasyonu) içindedir. Yalnız
CAD modelinin değişmesi public repoda yeni commit gerektirmez. Codex dışında dosya
kaydetmek kendiliğinden push başlatmaz.

Public hedef: [burakistikam/3D-modeling](https://github.com/burakistikam/3D-modeling).

- Yalnız incelenmiş yönetim belgelerini ve skill dosyalarını ekleyin.
- Kaynak çalışma alanını topluca kopyalamayın. Her güncellemede seçilen dosyaları
  karşılaştırın; kişisel yolları, kimlik bilgilerini ve göreve özel verileri çıkarın.
- `.gitignore` varsayılan olarak yeni dosyaları dışlar. Yeni bir paylaşılabilir belge
  gerektiğinde tam dosya yolunu izin listesine ekleyin; `git add -f` kullanmayın.
- Commit öncesi `git diff --cached` ve `git diff --cached --name-only` ile içeriği
  ve dosya listesini inceleyin. İzin listesi içerik denetiminin yerine geçmez.
- Public commit metinlerine, commit yazar e-postasına ve dosya geçmişine de dikkat
  edin. Kişisel e-posta yerine hesabın doğrulanmış gizlilik/noreply adresini kullanın.
- Push sonrasında uzak commit ile yerel commit'in eşleştiğini doğrulayın.

Bir tasarım görevinin özel girdilerini bu repoya koymak yerine ayrı, uygun erişim
izinlerine sahip bir çalışma alanında tutun. Public belgeyi güncellemek, kaynak
çalışma alanındaki kuralları veya kurulu skill'i kendiliğinden değiştirmez.
