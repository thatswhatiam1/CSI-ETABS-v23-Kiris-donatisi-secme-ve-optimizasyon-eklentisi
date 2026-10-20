# Güvenlik politikası / Security policy

[Türkçe](#türkçe) · [English](#english)

## Türkçe

### Desteklenen sürümler

Yalnızca [Releases](../../releases) bölümündeki **en son sürüm** desteklenir.
Güvenlik düzeltmeleri yeni bir sürüm olarak yayınlanır; eski sürümlere yama
yapılmaz.

| Sürüm | Destek |
|---|---|
| v10 | ✅ |
| v10'dan eski | ❌ |

### Güvenlik açığı bildirme

Güvenlik açıklarını **herkese açık issue olarak bildirmeyin.** Bunun yerine
reponun **Security** sekmesindeki **Report a vulnerability** düğmesini
kullanın; bildirim yalnızca repo sahibine görünür.

Bildirime şunları ekleyin: etkilenen sürüm, ETABS sürümü (eklentiyse),
sorunun tarifi ve yeniden üretme adımları. Müşteri modeli ya da kişisel veri
eklemeyin; gerekiyorsa küçük bir sentetik örnek yeterli.

Bu kişisel bir projedir; bildirimler en kısa sürede incelenir ama belirli bir
yanıt süresi taahhüt edilmez. Doğrulanan açık düzeltildikten sonra sürüm
notunda bildirene teşekkür edilir (istemezse adı yazılmaz).

### Kapsam

Güvenlik açığı sayılanlar: programın ya da kurulum betiğinin kullanıcının
haberi olmadan dosya yazması/silmesi, beklenmedik kod çalıştırması, hazırlanmış
bir girdi dosyasıyla (xlsx, csv) istismar edilebilmesi gibi durumlar.

**Mühendislik hesabındaki hatalar** (yanlış donatı, yönetmelik yorumu, eksik
kontrol) güvenlik açığı değildir; bunları normal bir **issue** olarak bildirin.
Bu tür hataların proje güvenliğine etkisi için README'deki sorumluluk reddine
bakın: her çıktı mühendis tarafından kontrol edilmelidir.

### Programın yaptıkları

- **Ağ bağlantısı kurmaz.** Telemetri, güncelleme denetimi ya da veri gönderimi
  yoktur; ETABS modeli ve çıktılar bilgisayardan çıkmaz.
- Okur: ETABS'ın açık modeli (eklenti) ya da seçilen `.xlsx` dosyası.
  Yazar: çıktı klasörüne (önerilen yer modelin ya da xlsx'in yanındaki
  `done-cikti`, model hiç kaydedilmemişse `%TEMP%\done-cikti`; kullanıcı
  değiştirebilir) ve ayar profilleri için `%APPDATA%\KirisDone\`.
- `KUR.cmd` eklenti dosyalarını `C:\ETABSPlugins\KirisDone-v5\` klasörüne
  kopyalar ve o klasörde kalmış eski bir `CSiAPIv1.dll` kopyasını siler; başka
  bir yere yazmaz ve kayıt defterine dokunmaz.
- `bagimsiz\BASLAT.cmd`, .NET çalışma zamanı eksikse ve kullanıcı onaylarsa
  tarayıcıda Microsoft'un .NET indirme sayfasını açar.
- ETABS'ın kendi API kütüphanesi (`CSiAPIv1.dll`) pakete dahil değildir;
  ETABS'ın kurulu kopyası kullanılır.

### İndirilen paketi doğrulama

Dosyalar kod imzalı **değildir**; Windows SmartScreen uyarı verebilir. Paketi
yalnızca bu reponun Releases bölümünden indirin ve özetini kontrol edin:

```powershell
Get-FileHash .\KirisDone-v10.zip -Algorithm SHA256
```

| Paket | SHA-256 |
|---|---|
| `KirisDone-v10.zip` | `37C8245673F6C54ECBD493A88833A5172FF90C5D15EA1B451DC1749753CACC72` |

---

## English

### Supported versions

Only the **latest release** under [Releases](../../releases) is supported.
Security fixes ship as a new release; older versions are not patched.

| Version | Supported |
|---|---|
| v10 | ✅ |
| older than v10 | ❌ |

### Reporting a vulnerability

**Do not report vulnerabilities as public issues.** Use the **Report a
vulnerability** button in the repository's **Security** tab instead; the
report is visible only to the repository owner.

Include the affected version, the ETABS version (for the plugin), a
description and steps to reproduce. Do not attach client models or personal
data; a small synthetic example is enough.

This is a personal project: reports are looked at as soon as possible, but no
response time is guaranteed. Once a confirmed issue is fixed, the reporter is
credited in the release notes (or left unnamed, if preferred).

### Scope

In scope: the program or the install script writing/deleting files without the
user's knowledge, running unexpected code, or being exploitable through a
crafted input file (xlsx, csv).

**Errors in the engineering calculation** (wrong reinforcement, code
interpretation, a missing check) are not security vulnerabilities; please open
a regular **issue**. See the disclaimer in the README: every output must be
checked by an engineer.

### What the program does

- **It makes no network connections.** No telemetry, no update check, no data
  upload; the ETABS model and the outputs never leave the computer.
- It reads the open ETABS model (plugin) or the selected `.xlsx` file. It
  writes to the output folder (suggested: `done-cikti` next to the model or
  the xlsx, or `%TEMP%\done-cikti` if the model was never saved; the user can
  change it) and to `%APPDATA%\KirisDone\` for setting profiles.
- `KUR.cmd` copies the plugin files to `C:\ETABSPlugins\KirisDone-v5\` and
  deletes a stale `CSiAPIv1.dll` copy left in that folder; it writes nowhere
  else and does not touch the registry.
- `bagimsiz\BASLAT.cmd` opens Microsoft's .NET download page in the browser,
  only if the .NET runtime is missing and the user agrees.
- ETABS' own API library (`CSiAPIv1.dll`) is not shipped; the installed ETABS
  copy is used.

### Verifying the download

The files are **not** code-signed; Windows SmartScreen may warn. Download the
package only from this repository's Releases and check its hash:

```powershell
Get-FileHash .\KirisDone-v10.zip -Algorithm SHA256
```

| Package | SHA-256 |
|---|---|
| `KirisDone-v10.zip` | `37C8245673F6C54ECBD493A88833A5172FF90C5D15EA1B451DC1749753CACC72` |
