# Türkçe Terim Sözlüğü Tamamlama — Uygulama Planı

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** `property-names/tr.json` ve `space-names/tr.json` dosyalarındaki 160 özellik + 148 uzay çevirisini tamamla.

**Architecture:** Her görev bir JSON dosyasına yeni girişler ekler; mevcutlara dokunmaz. JSON geçerliliği her görev sonrası kontrol edilir. Çeviriler mevcut 83+74 girişin terminoloji örüntüsünü takip eder.

**Tech Stack:** JSON (tr.json), Node.js (validation), pnpm (dev server), SvelteKit HMR

---

## Dosya Haritası

| Dosya | Durum | Açıklama |
|---|---|---|
| `web/packages/viewer/src/i18n/property-names/tr.json` | Mevcut — değiştirilecek | 83 → 243 giriş |
| `web/packages/viewer/src/i18n/space-names/tr.json` | Mevcut — değiştirilecek | 74 → 222 giriş |
| `CHANGELOG.md` | Mevcut — değiştirilecek | v0.3.0 girişi |

---

## Görev 1 — Özellik çevirileri: P000024–P000083

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/property-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini `property-names/tr.json` dosyasına kapanış `}` parantezinden önce ekle**

```json
  "P000024": "Yerel görece tıkız",
  "P000025": "Tıkızlarla tüketilir",
  "P000034": "Tam normal",
  "P000035": "Tam $T_4$",
  "P000038": "Enjektif yol bağlantılı",
  "P000043": "Yerel enjektif yol bağlantılı",
  "P000045": "Dağılım noktası var",
  "P000054": "$\\sigma$-yerel sonlu baz var",
  "P000056": "Silik",
  "P000058": "Kardinalite $\\lt\\mathfrak c$",
  "P000059": "Kardinalite $\\leq 2^{\\mathfrak c}$",
  "P000060": "Güçlü bağlantılı",
  "P000061": "Sıfır-dışı tümlüklü",
  "P000062": "Zayıf Lindelöf",
  "P000065": "Kardinalite $=\\mathfrak c$",
  "P000066": "Menger",
  "P000068": "Rothberger",
  "P000069": "Stratejik Menger",
  "P000070": "Markov Menger",
  "P000071": "$\\sigma$-görece tıkız",
  "P000072": "2-Markov Menger",
  "P000073": "Sober",
  "P000074": "Kozmik",
  "P000075": "Spektral",
  "P000076": "Yakınsal",
  "P000077": "Corson tıkız",
  "P000079": "Dizisel",
  "P000081": "Sayılabilir dar",
  "P000082": "Yerel metrikleştirilebilir",
  "P000083": "Meta-Lindelöf"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/property-names/tr.json','utf8')); console.log('OK')"
```

Beklenen çıktı: `OK`

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/property-names/tr.json
git commit -m "i18n: Türkçe özellik çevirileri P000024-P000083"
```

---

## Görev 2 — Özellik çevirileri: P000084–P000161

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/property-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini ekle**

```json
  "P000084": "Yerel Hausdorff",
  "P000085": "Temelden bağlantısız",
  "P000087": "Grup topolojisi var",
  "P000088": "Koleksiyonca normal",
  "P000089": "Sabit nokta özelliği",
  "P000090": "Aleksandrov",
  "P000091": "Eberlein tıkız",
  "P000092": "$k_{\\omega,3}$-uzayı",
  "P000093": "Yerel sayılabilir",
  "P000094": "Yerel sonlu",
  "P000096": "Yerel ark bağlantılı",
  "P000097": "$\\mathbb R$'ye gömülebilir",
  "P000098": "$k_{\\omega,1}$-uzayı",
  "P000099": "US",
  "P000100": "KC",
  "P000101": "Kapalı retraktı var",
  "P000103": "Güçlü KC",
  "P000105": "Para-Lindelöf",
  "P000106": "$G_\\delta$-köşegeni var",
  "P000107": "Kapalı noktası var",
  "P000108": "Kalıtsal koleksiyonca normal",
  "P000109": "Monoton normal",
  "P000110": "Gelişebilir",
  "P000113": "Moore uzayı",
  "P000114": "Kardinalite $=\\aleph_1$",
  "P000115": "Alt-para-tıkız",
  "P000117": "$\\sigma$-yerel sonlu ağı var",
  "P000118": "$\\sigma$-yerel sonlu $k$-ağı var",
  "P000120": "Yerel sıralanabilir",
  "P000123": "Yerel $n$-Öklidyen",
  "P000125": "Birden fazla noktası var",
  "P000126": "Kapı uzayı",
  "P000127": "Dowker",
  "P000128": "$k$-Lindelöf",
  "P000132": "$G_\\delta$ uzayı",
  "P000133": "LOTS",
  "P000134": "$R_1$",
  "P000135": "$R_0$",
  "P000136": "Antitıkız",
  "P000138": "Sayılabilir sürekli öz-dönüşüm",
  "P000140": "$k_1$-uzayı",
  "P000141": "$k_2$-uzayı",
  "P000142": "$k_3$-uzayı",
  "P000143": "Zayıf Hausdorff",
  "P000144": "Yerel sözde-metrikleştirilebilir",
  "P000147": "P-uzayı",
  "P000148": "CGWH",
  "P000149": "$\\omega$-Lindelöf",
  "P000150": "$\\omega$-Rothberger",
  "P000151": "Stratejik Rothberger",
  "P000152": "Markov Rothberger",
  "P000153": "$\\omega$-Menger",
  "P000154": "GO-uzayı",
  "P000155": "Yerel $1$-Öklidyen",
  "P000156": "$k$-Rothberger",
  "P000157": "Stratejik $k$-Rothberger",
  "P000158": "Markov $k$-Rothberger",
  "P000159": "$k$-Menger",
  "P000160": "Stratejik $k$-Menger",
  "P000161": "Markov $k$-Menger"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/property-names/tr.json','utf8')); console.log('OK')"
```

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/property-names/tr.json
git commit -m "i18n: Türkçe özellik çevirileri P000084-P000161"
```

---

## Görev 3 — Özellik çevirileri: P000163–P000244

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/property-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini ekle**

```json
  "P000163": "Kardinalite $\\leq\\mathfrak c$",
  "P000164": "Her ölçülebilir kardinalden küçük kardinalite",
  "P000165": "Sözde normal",
  "P000166": "Daha kaba ayrılabilir metrikleştirilebilir topoloji var",
  "P000167": "Dizisel ayrık",
  "P000168": "Sayılabilir kümeler ayrık",
  "P000169": "Yarı-Hausdorff",
  "P000170": "$k_1$-Hausdorff",
  "P000171": "$k_2$-Hausdorff",
  "P000172": "Radyal",
  "P000173": "Sözde radyal",
  "P000174": "İyi tabanlı",
  "P000175": "Kardinalite $\\geq 3$",
  "P000176": "Kardinalite $\\geq 4$",
  "P000177": "$\\sigma$-uzayı",
  "P000178": "$\\aleph$-uzayı",
  "P000179": "$\\aleph_0$-uzayı",
  "P000181": "Sayılabilir sonsuz",
  "P000182": "Sayılabilir ağı var",
  "P000183": "Sayılabilir $k$-ağı var",
  "P000184": "Öklidyen uzaya gömülebilir",
  "P000185": "Bölüm topolojisi",
  "P000186": "Topolojik $W$-gruba gömülür",
  "P000187": "W-uzayı",
  "P000189": "$\\sigma$-bağlantılı",
  "P000190": "Ordinal uzayı",
  "P000191": "Noktalar $G_\\delta$",
  "P000192": "Yarı-sober",
  "P000193": "Büzüşen",
  "P000194": "Alt-meta-tıkız",
  "P000197": "Sayılabilir yayılım",
  "P000198": "Sayılabilir genişlik",
  "P000201": "Genel noktası var",
  "P000202": "Tekil komşuluğu olan nokta var",
  "P000203": "Neredeyse ayrık",
  "P000204": "Kesme noktası var",
  "P000205": "Kesme noktalı uzay",
  "P000206": "Güçlü Choquet",
  "P000207": "Güçlü koleksiyonca normal",
  "P000208": "Noetherian",
  "P000209": "Yoğunluk $\\leq\\mathfrak c$",
  "P000210": "$\\alpha_1$",
  "P000211": "$\\alpha_{1.5}$",
  "P000212": "$\\alpha_2$",
  "P000213": "$\\alpha_3$",
  "P000214": "$\\alpha_4$",
  "P000215": "Kalıtsal reel-tıkız",
  "P000219": "Toronto",
  "P000222": "Son-sonlu topolojisi var",
  "P000223": "Yerel büzülebilir",
  "P000224": "Zayıf yerel büzülebilir",
  "P000225": "$LC$",
  "P000226": "Artinian",
  "P000227": "$\\mathfrak c$ boyutlu ayrık kapalı alt kümesi var",
  "P000228": "Zayıf birinci sayılabilir",
  "P000229": "Yarı-yerel basit bağlantılı",
  "P000230": "Yerel basit bağlantılı",
  "P000231": "Zayıf yerel basit bağlantılı",
  "P000232": "$LC^1$",
  "P000233": "Açık yol bileşenleri var",
  "P000234": "Açık bağlantılı bileşenleri var",
  "P000235": "Yerel Öklidyen yarı-uzay",
  "P000236": "Yerel $n$-Öklidyen yarı-uzay",
  "P000237": "Sınırlı topolojik $n$-manifold",
  "P000238": "Reel TVS topolojisi var",
  "P000239": "Yarı-yerel büzülebilir",
  "P000241": "Yerel Öklidyen yarı-doğru",
  "P000242": "Zayıf büzülebilir",
  "P000243": "Sayılabilir $\\pi$-ağırlık",
  "P000244": "Sayılabilir $\\pi$-karakter"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/property-names/tr.json','utf8')); console.log('OK')"
```

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/property-names/tr.json
git commit -m "i18n: Türkçe özellik çevirileri P000163-P000244"
```

---

## Görev 4 — Uzay çevirileri: S000006–S000098

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/space-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini `space-names/tr.json` dosyasına kapanış `}` parantezinden önce ekle**

```json
  "S000006": "$\\mathbb R\\setminus\\mathbb Z$ üzerinde silinmiş tamsayı topolojisi",
  "S000007": "Üç noktalı küme üzerinde belirli nokta topolojisi",
  "S000008": "Sayılabilir sonsuz küme üzerinde belirli nokta topolojisi",
  "S000009": "$\\mathbb R$ üzerinde belirli nokta topolojisi",
  "S000011": "Üç noktalı küme üzerinde dışlanan nokta topolojisi",
  "S000012": "Sayılabilir sonsuz küme üzerinde dışlanan nokta topolojisi",
  "S000013": "$\\mathbb R$ üzerinde dışlanan nokta topolojisi",
  "S000014": "Ya-ya topolojisi",
  "S000018": "$\\mathbb R$ üzerinde çift noktalı ko-sayılabilir topoloji",
  "S000019": "Öklidyen reel sayılar için tıkız tümlüklü topoloji",
  "S000021": "Ayrılabilir Hilbert uzayı üzerinde zayıf topoloji",
  "S000022": "$\\mathbb R$ üzerinde Fortissimo uzayı",
  "S000024": "$\\mathbb R$ üzerinde değiştirilmiş Fort uzayı",
  "S000031": "$\\mathbb Q$'nun tek-nokta tıkızlaştırmasının karesi",
  "S000037": "Uç noktası ikilenmiş $\\omega_1+1$",
  "S000040": "Değiştirilmiş uzun ışın",
  "S000042": "Reeller üzerinde sağ ışın topolojisi",
  "S000045": "Örtüşen aralık topolojisi",
  "S000046": "İç içe geçen aralık topolojisi",
  "S000047": "Sierpinski uzaylarının sayılabilir toplamı",
  "S000048": "Açık olmayan genel nokta ile genişletilmiş $\\omega$ üzerinde son-sonlu topoloji",
  "S000049": "Bölen topolojisi",
  "S000050": "Odak noktasıyla genişletilmiş $\\mathbb Q$",
  "S000052": "Görece asal tamsayı topolojisi",
  "S000053": "Asal tamsayı topolojisi",
  "S000055": "Reel sayılar üzerinde sayılabilir tümlüklü genişletme topolojisi",
  "S000058": "$\\mathbb R$'nin aşikar rasyonel genişlemesi",
  "S000059": "$\\mathbb R$'nin aşikar irrasyonel genişlemesi",
  "S000060": "$\\mathbb R$'nin noktalı rasyonel genişlemesi",
  "S000061": "$\\mathbb R$'nin noktalı irrasyonel genişlemesi",
  "S000062": "$\\mathbb R$'nin ayrık rasyonel genişlemesi",
  "S000064": "Düzlemin rasyonel genişlemesi",
  "S000065": "Telofaz topolojisi",
  "S000066": "Çift orijinli düzlem",
  "S000067": "İrrasyonel eğim topolojisi",
  "S000068": "Silinmiş çap topolojisi",
  "S000069": "Silinmiş yarıçap topolojisi",
  "S000070": "Yarı-disk topolojisi",
  "S000071": "Düzensiz kafes topolojisi",
  "S000072": "Arens karesi",
  "S000073": "Basitleştirilmiş Arens karesi",
  "S000075": "Rasyonel teğet disk topolojisi",
  "S000077": "Michael doğrusunun irrasyonel sayılarla çarpımı",
  "S000080": "B. Scott'ın değiştirilmiş Arens karesi",
  "S000081": "Aleksandroff tahtası",
  "S000082": "Süreklilik sayıda sağ ışın topolojisinin toplamı",
  "S000084": "Sayılabilir çok orijinli doğru",
  "S000085": "Sayılamaz çok orijinli doğru",
  "S000086": "Her yerde ikili doğru",
  "S000087": "Silinmiş Dieudonné tahtası",
  "S000089": "Silinmiş Tihonov tirbuşonu",
  "S000090": "Hewitt'in yoğunlaştırılmış tirbuşonu",
  "S000091": "Thomas tahtası",
  "S000092": "Thomas tirbuşonu",
  "S000094": "Güçlü paralel doğru topolojisi",
  "S000097": "Sıralı $S_\\omega$ fanının tek-nokta tıkızlaştırması",
  "S000098": "Minimal Hausdorff topolojisi"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/space-names/tr.json','utf8')); console.log('OK')"
```

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/space-names/tr.json
git commit -m "i18n: Türkçe uzay çevirileri S000006-S000098"
```

---

## Görev 5 — Uzay çevirileri: S000100–S000200

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/space-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini ekle**

```json
  "S000100": "David Gao'nun ultra-bağlantılı büzülemez uzayı",
  "S000101": "Sayılabilir ayrık uzayın süreklilik üssü",
  "S000102": "$\\mathfrak c$ ağırlıklı Baire uzayı $B(\\mathfrak c)$",
  "S000103": "$[0,1]$'in süreklilik üssü",
  "S000104": "Birim aralıkların süreklilik üssüyle ilk sayılamaz ordinalin çarpımı",
  "S000107": "Reellerin sayılabilir kutu çarpımı",
  "S000109": "Novak uzayı",
  "S000110": "Güçlü ultrasüzgeç topolojisi",
  "S000111": "$\\beta\\omega$'nun tekil ultrasüzgeç alt uzayı",
  "S000112": "Reel düzlemdeki iç içe dikdörtgenler",
  "S000115": "Genişletilmiş topoloğun sinüs eğrisi",
  "S000117": "Kapalı sonsuz süpürge",
  "S000118": "Tamsayı süpürgesi",
  "S000119": "Reel düzlemdeki iç içe açılar",
  "S000120": "Sonsuz kafes",
  "S000121": "Bernstein'in bağlantılı kümesi",
  "S000122": "Gustin'in dizi uzayı",
  "S000123": "Roy'un kafes uzayı",
  "S000124": "Roy'un kafes alt uzayı",
  "S000126": "Delinmiş Knaster-Kuratowski yelpazesi",
  "S000128": "Miller'ın çift bağlantılı kümesi",
  "S000129": "Göbeği olmayan tekerlek",
  "S000130": "Tangora'nın bağlantılı uzayı",
  "S000131": "$\\omega$ kollu sıralı fan",
  "S000132": "Duncan uzayı",
  "S000133": "Postane metriğiyle reel doğru",
  "S000134": "Düzlemdeki radyal metrik",
  "S000135": "$\\mathbb R^2$ üzerinde radyal aralık topolojisi",
  "S000136": "Bing'in G Örneği",
  "S000137": "Bing'in G Örneğinin Michael alt uzayı",
  "S000140": "Ko-sayılabilir açık komşuluklu noktayla genişletilmiş $\\mathbb R$",
  "S000141": "Sıralı uzay $\\omega_1+1+\\omega^*$",
  "S000142": "Erdős uzayı",
  "S000143": "Kelebek uzayı",
  "S000144": "Aleksandrov topolojili elmas kısmi sıralı küme $2\\times 2$",
  "S000145": "$\\omega$ üzerinde serbest ultrasüzgeç topolojisi",
  "S000147": "(CH) Reellerin Luzin alt kümesi (Özel Luzin kümesi $L$)",
  "S000148": "(CH) Reellerin Luzin alt kümesi (Genel Luzin kümesi $H$)",
  "S000150": "$[0,1]\\cap\\mathbb Q$ üzerinde sağ kapalı-ışın topolojisi",
  "S000151": "$[0,1]\\cap\\mathbb Q$ üzerinde sağ açık-ışın topolojisi",
  "S000152": "Aleksandrov topolojili $\\{-1,0_a,0_b\\}\\cup\\{1/n\\}_{n=1}^\\infty$ kısmi sıralı kümesi",
  "S000153": "Açık uzun ışın",
  "S000154": "Reel sayılar üzerinde Fort uzayı",
  "S000155": "$\\aleph_1$ boyutlu Fortissimo uzayı",
  "S000157": "$\\aleph_2$ boyutlu Fortissimo uzayı",
  "S000159": "$[0,1]$ üzerinde sağ açık-ışın topolojisi",
  "S000160": "$\\omega+1$ üzerinde sağ açık-ışın topolojisi",
  "S000161": "Van Douwen'in anti-Hausdorff Fréchet uzayı",
  "S000164": "Tek noktalı uzay ile iki noktalı aşikar uzayın toplamı",
  "S000165": "Arens-Fort uzayının tek-nokta tıkızlaştırması",
  "S000166": "$\\omega+1$ üzerinde sol ışın topolojisi",
  "S000167": "$\\omega+1+\\omega^*$ üzerinde sağ açık-ışın topolojisi",
  "S000171": "Brian Örneği",
  "S000172": "Kannan-Rajagopalan-Hart uzayı",
  "S000173": "Uzun ışının kapalı aralığın süreklilik üssüyle çarpımı",
  "S000174": "Pol'un $T_6$ para-tıkız olmayan uzayı",
  "S000175": "Radyal düzlem",
  "S000177": "Misra'nın $E_0$ uzayı",
  "S000178": "Misra'nın $E_0$ alt uzayı",
  "S000179": "Peng-Wu Grubu",
  "S000180": "Solomon'un dağınık uzayı",
  "S000181": "Sayılabilir $\\sigma$-çarpım $\\sigma(\\omega_1+1)^\\omega$",
  "S000182": "$\\mathbb Q$'nun süreklilik sayıda kopyasının ayrık birleşimi",
  "S000183": "KP Hart'ın dizisel ayrık olmayan değiştirilmiş ko-sayılabilir topolojisi",
  "S000184": "Bir çift iki noktalı aşikar uzayın toplamı",
  "S000185": "Metrik fanın tek-nokta tıkızlaştırması",
  "S000186": "Hausdorff olmayan uzayların yakınsayan dizisi",
  "S000187": "Üç noktalı küme üzerinde sağ ışın topolojisi",
  "S000188": "Tek noktalı uzay ile Sierpinski uzayının toplamı",
  "S000192": "Değiştirilmiş telofaz topolojisi",
  "S000195": "$\\omega_1$ üzerinde son-sonlu ve sol ışın topolojilerinin birleşimi",
  "S000198": "Reeller ile tek noktalı uzayın ayrık birleşimi",
  "S000199": "$\\omega$ üzerinde sol ışın topolojisi",
  "S000200": "$\\omega$ üzerinde sağ ışın topolojisi"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/space-names/tr.json','utf8')); console.log('OK')"
```

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/space-names/tr.json
git commit -m "i18n: Türkçe uzay çevirileri S000100-S000200"
```

---

## Görev 6 — Uzay çevirileri: S000202–S000223

**Dosyalar:**
- Modify: `web/packages/viewer/src/i18n/space-names/tr.json`

- [ ] **Adım 1: Aşağıdaki JSON girişlerini ekle**

```json
  "S000202": "$\\omega$ kollu metrik fan",
  "S000203": "$\\{\\{0\\},X\\}$ bazlı üç noktalı küme",
  "S000204": "$\\{\\{0,1\\},X\\}$ bazlı üç noktalı küme",
  "S000206": "Silinmiş aralıklar dizisi topolojisi",
  "S000207": "Cohen'in $\\omega_1\\times(\\omega_1+1)$ modifikasyonu",
  "S000208": "Rudin'in Dowker uzayının Hewitt reel-tıkızlaştırması",
  "S000211": "$\\omega_1+1$ üzerinde son-sonlu ve değiştirilmiş sağ kapalı-ışın topolojilerinin birleşimi",
  "S000212": "Sözlüksel sıralı Hilbert küpü $[0,1]^\\omega$",
  "S000214": "Sözlüksel sıralı $\\mathbb Z^{\\omega_1}$",
  "S000216": "Katětov'un $\\beta\\mathbb N$ üzerindeki normal olmayan alt uzayı",
  "S000217": "$\\omega_1$ üzerinde sol ışın topolojisi",
  "S000218": "Çarpım uzayı $\\omega_1\\times(\\omega_1+1)$",
  "S000219": "$2^{\\mathfrak c}$ boyutlu ayrık uzay",
  "S000220": "$\\omega_1$ üzerinde sağ kapalı-ışın topolojisi",
  "S000221": "$\\omega_1$ üzerinde sağ açık-ışın topolojisi",
  "S000222": "$\\omega^{2^\\mathfrak{c}}$ üzerinde çarpım topolojisi",
  "S000223": "$[\\omega]^\\omega$ üzerinde Ellentuck topolojisi"
```

- [ ] **Adım 2: JSON geçerliliğini doğrula**

```powershell
node -e "JSON.parse(require('fs').readFileSync('web/packages/viewer/src/i18n/space-names/tr.json','utf8')); console.log('OK')"
```

- [ ] **Adım 3: Commit**

```bash
git add web/packages/viewer/src/i18n/space-names/tr.json
git commit -m "i18n: Türkçe uzay çevirileri S000202-S000223"
```

---

## Görev 7 — EN↔TR karşılaştırma tablosu üret

**Dosyalar:**
- Read: her iki tr.json

- [ ] **Adım 1: Karşılaştırma tablosunu üret**

Aşağıdaki Node.js komutuyla EN↔TR karşılaştırma tablosunu üret (yalnızca yeni eklenen girişler — Görev 1-6'da eklenenler):

```powershell
node -e "
const fs = require('fs');
const propTr = JSON.parse(fs.readFileSync('web/packages/viewer/src/i18n/property-names/tr.json','utf8'));
const data = JSON.parse(fs.readFileSync('E:/PYTHON/topohub/data/properties/P000001.md','utf8').match(/.*/)[0]||'{}');
console.log('Özellik tablosu üretildi. Toplam giriş:', Object.keys(propTr).length);
"
```

Gerçek karşılaştırma tablosu review aşamasında kullanıcıya sunulur; Claude Code oturumunda `ctx_execute` ile üretilir.

- [ ] **Adım 2: Kullanıcıya tabloyu sun ve düzeltme iste**

Tüm yeni çeviriler gözden geçirilir. Yanlış girişler işaretlenir, düzeltmeler aynı dosyalara uygulanır.

- [ ] **Adım 3: Son commit (eğer düzeltme varsa)**

```bash
git add web/packages/viewer/src/i18n/property-names/tr.json web/packages/viewer/src/i18n/space-names/tr.json
git commit -m "i18n: Türkçe sözlük review düzeltmeleri"
```

---

## Görev 8 — CHANGELOG.md güncelle

**Dosyalar:**
- Modify: `CHANGELOG.md`

- [ ] **Adım 1: CHANGELOG'a v0.3.0 girişini ekle (en başa, `## [0.2.0]` satırından önce)**

```markdown
## [0.3.0] — 2026-06-11

Türkçe terim sözlüğü tamamlandı.

### Eklenen

**Türkçe Terim Sözlüğü Genişletmesi**
- `property-names/tr.json`: 83'ten 243'e — 160 özellik için Türkçe karşılık eklendi
- `space-names/tr.json`: 74'ten 222'ye — 148 uzay için Türkçe karşılık eklendi
- Tüm pi-base özellik ve uzay adları artık Türkçe görüntüleniyor (graceful EN fallback korundu)

---
```

- [ ] **Adım 2: Commit**

```bash
git add CHANGELOG.md
git commit -m "docs: v0.3.0 CHANGELOG girişi — Türkçe sözlük tamamlandı"
```
