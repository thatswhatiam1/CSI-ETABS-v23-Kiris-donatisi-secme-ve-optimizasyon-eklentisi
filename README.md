# KirisDone — ETABS kiriş donatısı asistanı

[Türkçe](#türkçe) · [English](#english)

> **KirisDone bir otomasyon değil, bir asistandır.** Önerir, hesaplar, çizer;
> ama karar ve sorumluluk projeyi imzalayan mühendistedir. Hiçbir çıktı
> kontrol edilmeden projede kullanılmamalıdır.
>
> **KirisDone is an assistant, not an automation.** It proposes, calculates
> and draws; the decision and the responsibility stay with the engineer who
> signs the project. No output should be used without being checked.

---

## Türkçe

ETABS'ın kiriş tasarım sonuçlarını okur ve her kiriş için boyuna donatı
(montaj, alt donatı, mesnet ilaveleri, gövde) ile etriye/çiroz önerir; sonucu
Excel listesi ve DXF paftası olarak verir. ETABS'ın **Tools** menüsüne gömülü
eklenti olarak ya da ETABS'sız, ETABS'tan alınmış `.xlsx` çıktısıyla çalışan
bağımsız program olarak kullanılabilir.

### Ne yapar

- **Boyuna donatı seçimi:** montaj, alt, sol/sağ mesnet ilavesi ve gövde
  donatısı için adet × çap. Komşu kirişlerin ortak mesnedinde ilave
  ortaklaştırılır; ilave çapı montaj çapını geçmez.
- **Kesme tahkiki ve çiroz:** etriye aralığı ve kol sayısı kesme tahkikinden;
  kapasite kesmesi kontrolü dahil.
- **Burulma:** ETABS'ın verdiği burulma boyuna payı montaj ve alt donatı
  talebine eklenir; enine payı bayraklanır.
- **Yönetmelik profili:** TS 500 / TBDY 2018 ya da ACI 318-19.
- **Done Düzenle:** her kiriş için adet × çap matrisi; uygun olmayan seçenekler
  kırmızı ve nedeni yazılı. Elle seçim de aynı kontrollerden geçer.
- **Ayarlar ve Ayarlarım:** programın bazı kararları kullanıcıya açık (asgari
  adet tablosu, ikinci sıra, süreklilik, çift adet…). Ayarlar kullanıcı adıyla
  profil olarak kaydedilir; güncelleme profillere dokunmaz. Hiçbir ayar
  yönetmelik sınırını gevşetemez.
- **Çıktılar:** `done-listesi.xlsx` (uyarılar ve parametreler dahil), Revit'e
  aktarım için `kiris done ciktilari.xlsx`, kat kat DONE planı ve kiriş açılımı
  DXF'leri (metraj tablosuyla), kirdet CSV'leri.
- Belirsiz ya da yönetmeliği zorlayan her durumda sessizce karar vermez,
  **bayrak koyar**: uyarılar Excel'de ve paftada ayrı katmanda görünür.

### Kurulum

[Releases](../../releases) bölümünden son paketi indirin, klasörün tamamını
açın ve `OKU-BENI.txt`'yi izleyin. Kısaca:

| Kullanım | Gerekenler | Nasıl |
|---|---|---|
| ETABS eklentisi | ETABS 23 (ya da .NET 8 tabanlı bir sürüm) | ETABS kapalıyken `KUR.cmd`, sonra **Tools › Add/Show Plugins** |
| Bağımsız program | .NET 8 Desktop Runtime (x64); ETABS gerekmez | `bagimsiz\BASLAT.cmd` |

Bağımsız program ETABS 22.5 ve 23'ün tablo çıktılarını tanır.

### Nasıl yapıldı

Bu program **vibe coding** ile, yapay zekâ (Anthropic Claude) ile birlikte
yazıldı. Mühendislik kuralları, kabuller ve kararlar bir inşaat mühendisinden;
kodun büyük kısmı yapay zekâdan. Sentetik bir ETABS projesi, bağımsız bir
doğrulayıcı ve gerçek modellerle sınandı — yine de hata içerebilir. Kaynak kod
şimdilik yayınlanmıyor.

### Sorumluluk reddi

KirisDone bir mühendislik yardımcısıdır; hesap, tasarım ve kontrol
sorumluluğunu üstlenmez. Çıktılar, yetkin bir mühendisin değerlendirmesinin ve
yürürlükteki yönetmeliklere göre yapılması gereken tahkiklerin yerine geçmez.
Programın kullanımından ya da çıktılarına dayanılarak verilen kararlardan
doğabilecek doğrudan veya dolaylı zararlardan yazar sorumlu tutulamaz.
Çıktıları bağımsız olarak doğrulamak kullanıcının sorumluluğundadır.

---

## English

KirisDone reads ETABS beam design results and proposes, for every beam, the
longitudinal reinforcement (top continuous, bottom, support extras, side bars)
and the stirrups/ties; the result comes out as an Excel schedule and DXF
drawings. It runs either as a plugin inside ETABS' **Tools** menu or as a
standalone program working from an ETABS `.xlsx` table export, with no ETABS
needed. The interface and the outputs are in Turkish.

### What it does

- **Longitudinal bar selection:** count × diameter for top continuous, bottom,
  left/right support extras and side bars. Extras are shared at common
  supports of neighbouring beams; an extra bar is never thicker than the
  continuous top bar.
- **Shear check and ties:** stirrup spacing and leg count follow from the shear
  check, including capacity-design shear.
- **Torsion:** the longitudinal torsion demand reported by ETABS is added to
  the top and bottom demand; the transverse part is flagged.
- **Code profile:** TS 500 / TBDY 2018 (Turkish codes) or ACI 318-19.
- **Edit tab:** a count × diameter matrix per beam; options that do not work
  are red, with the reason. Manual choices go through the same checks.
- **Settings and profiles:** some of the program's decisions are open to the
  user (minimum bar counts, second layer, continuity, even counts…). Settings
  are saved as named user profiles that survive updates. No setting can relax
  a code limit.
- **Outputs:** `done-listesi.xlsx` (with warnings and parameters), an Excel
  file for Revit, per-storey reinforcement plans and beam elevation DXFs (with
  a bar schedule), and kirdet CSV files.
- Wherever a case is ambiguous or pushes a code limit, it does not decide
  silently — it **raises a flag**, shown in Excel and on a separate drawing
  layer.

### Installation

Download the latest package from [Releases](../../releases), extract the whole
folder and follow `OKU-BENI.txt` (Turkish). In short:

| Use | Requirements | How |
|---|---|---|
| ETABS plugin | ETABS 23 (or any .NET 8 based version) | run `KUR.cmd` with ETABS closed, then **Tools › Add/Show Plugins** |
| Standalone | .NET 8 Desktop Runtime (x64); no ETABS needed | `bagimsiz\BASLAT.cmd` |

The standalone program recognises the table exports of ETABS 22.5 and 23.

### How it was made

This program was **vibe coded** together with an AI (Anthropic Claude). The
engineering rules, assumptions and decisions come from a civil engineer; most
of the code was written by the AI. It was tested with a synthetic ETABS
project, an independent checker and real models — it may still contain
errors. The source code is not published for now.

### Disclaimer

KirisDone is an engineering aid; it does not take over responsibility for
analysis, design or checking. Its outputs do not replace the judgement of a
qualified engineer or the checks required by the applicable codes. The author
cannot be held liable for any direct or indirect damage arising from the use
of the program or from decisions based on its outputs. Verifying the outputs
independently is the user's responsibility.

<br>

<p align="right"><sub><sup>Mutluhan Göçer · 2026</sup></sub></p>
