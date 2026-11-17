# Bağlantı ve yerel kurulum

Bu belge bağlantı yöntemlerini tarif eder; makine config'i veya gizli bilgi içermez.
Ortak davranış için [AGENTS.md](AGENTS.md), modelleme için ilgili uygulama kuralları geçerlidir.

## Kaynak, runtime ve çıktı ayrımı

Yönetim checkout'u, kurulu MCP/runtime ve özel görev alanını ayrı konumlarda tutun.
Yerel yönlendirmede yönetim checkout'unun yolunu açıkça kaydedin; örneğin
`3D_MODELING_HOME` yerel bir yol sözleşmesi olabilir, istemcinin otomatik keşif özelliği değildir.
Bir istemci bu değişkeni desteklemiyorsa gerçek yolu kendi yerel ayarına yazın.

Proje AGENTS.md dosyası yalnız ortak AGENTS.md ve ilgili uygulama dosyasına
yönlendirme, yerel runtime yolu ve göreve özgü gerekli kapsamı içersin.
Skill dizininin tümünü (references ve agents dahil) tek bir kurulum noktasından
yükleyin. Link/junction desteklenmiyorsa yalnız bir kurulu kopyayı güncelleyin.
Plugin cache'i yeniden kurulursa yönlendirmenin hâlâ geçerli olduğunu kontrol edin.
Kayıtlı bir plugin varsa aynı skill'i ayrıca kullanıcı skill klasörüne kurmayın.

## Bağlantı envanteri

| Bağlantı | Yerel yapı | Salt okunur kontrol |
|---|---|---|
| Fusion Print | Python stdio MCP + FusionPrint add-in; ortak yerel dosya kuyruğu | CLI doctor, sonra ping veya MCP fusion_health, sonra fusion_ping ve aynı ID ile durum |
| Fusion 360 MCP | Ayrı MCP sunucusu + FusionMCP add-in | Kurulu aracın durum/belge sorgusu; Fusion Print ile karıştırmayın |
| SolidWorks | Yerel solidworks-mcp stdio sunucusu + çalışan SolidWorks | solidworks_status ve hedef belge bilgisi |
| Rhino | Kurulu Rhino MCP router/plugin | Kurulu şemadaki sürüm, belge ve bağlantı sorguları |
| Blender | Yerel MCP sunucusu + Blender eklentisi | Kurulu şemadaki sahne/dosya sorgusu |

Sunucunun listelenmesi uygulamanın veya ana thread'in yanıt verdiğini kanıtlamaz.
Şema ve komut adlarını kurulu sürümden okuyun; tablo sabit bir araç kataloğu değildir.
Durum kontrolü için yeni model oluşturmayın. Kapalı uygulamayı çevrimdışı olarak
raporlayın; offline protokol testiyle canlı CAD bağlantısını birbirine karıştırmayın.

## Fusion Print

Runtime'ın yerel kökü `<FUSION_PRINT_ROOT>`; altında `src/`, `addin/`,
`pyproject.toml`, `.venv/`, `models/`, `references/`, `.fusion/` ve
`artifacts/` bulunur. Son dört klasörün görev içeriği özel kalır.
Bu düzenin bir Git checkout'u olması gerekmez.

Yeni bir yerel runtime kurulumu için, eldeki runtime kaynak dizininde:

```powershell
python -m venv .venv
.\.venv\Scripts\python -m pip install -e '.[mcp,inspection,dev]'
.\.venv\Scripts\fusion-print install
.\.venv\Scripts\fusion-print codex-config
```

`install` yalnız FusionPrint eklentisini kurar. Fusion'da Scripts and Add-Ins
üzerinden etkinleştirin. Kurulu eklentinin `workspace.json` dosyası aynı runtime
köküne bakmalı. Başka bir kurulumu gösteren dosyayı doğrulamadan üzerine yazmayın.
FusionMCP bağımsızdır; Fusion Print kurulumu için değiştirilmez.

Üretilen MCP bölümünü mevcut istemci ayarlarını koruyarak birleştirin. Örnek:

```toml
[mcp_servers.fusion_print]
command = '<FUSION_PRINT_ROOT>/.venv/Scripts/python.exe'
args = ['-m', 'fusion_print.mcp_server', '--root', '<FUSION_PRINT_ROOT>']
startup_timeout_sec = 20
tool_timeout_sec = 60
```

Yer tutucuları gerçek yerel yollarla değiştirin. Komutları runtime kökünde çalıştırın
veya `fusion-print --root <FUSION_PRINT_ROOT> doctor` biçimini kullanın.
CLI model argümanı `models/` dizinine göredir:
`fusion-print validate mounting_plate/model.json`; başına ikinci bir `models/` eklemeyin.
Diğer komutlar ve tarif sözleşmesi [Fusion Print skill](Fusion-360/skills/fusion-print/SKILL.md) içindedir.

## Diğer yerel bağlantılar

- SolidWorks: mevcut stdio executable/interpreter yolunu koruyun.
  `SW_MCP_OUTPUT_ROOT` özel çıktı klasörü olmalı. MCP/COM önceliği ve doğrulama
  [SolidWorks skill](SolidWorks/skills/solidworks-design/SKILL.md) içindedir.
- Fusion 360 MCP: kurulu sunucunun Python ortamı ve FusionMCP eklentisi ayrı
  yönetilir. Bağlantının command/args alanlarını kendi kurulumundan alın.
- Rhino: router/plugin sürümünü ve hedef Rhino ana sürümünü eşleştirin;
  başka sürümdeki sabit paket dizinini kopyalamayın.
- Blender: sunucu komutu ile Blender içindeki eklentinin bağlantı ayarlarını
  eşleştirin. Eklenti etkin değilse stdio sunucusunun açılması yeterli değildir.

## Yerel taşıma kontrolü

1. Runtime, eklenti ayarı, MCP command/args, editable Python paketleri, başlangıç
   kısayolları ve proje yönlendirmelerinde kullanılan mevcut yolları belirleyin.
2. Özel dosyaları ve ayarları repo dışında yedekleyin. Çalışan CAD işi varken
   runtime taşımayın; açık kullanıcı belgelerini kapatmayın.
3. Runtime'ı bağımsız yerel konuma taşıyın. Sanal ortamları yeniden kurun veya
   tüm interpreter/paket/entrypoint yollarını onarıp doğrulayın.
4. Eklenti, istemci ve proje yönlendirmelerini aynı yeni konuma bağlayın.
   Yüklü MCP süreci eski yolu tutuyorsa istemci bağlantısını yenileyin.
   Fusion runtime'ı yüklüyse Python import önbelleği için Fusion yeniden başlatılır.
5. Offline testleri, gerçek MCP initialize/list-tools çağrısını ve uygulama açıksa
   salt okunur canlı bağlantıyı doğrulayın. Eksik canlı kontrolü açıkça raporlayın.
6. Eski aktif yol bağımlılığı kalmadığını ve özel dosyaların korunduğunu doğruladıktan
   sonra eski kurulumu kaldırın. Tarihsel kanıt/yedek içindeki eski yolları topluca
   değiştirmeyin; bunlar aktif config değildir.
