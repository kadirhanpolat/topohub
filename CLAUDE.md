# CLAUDE.md

Bu dosya Claude Code'a (ve diğer AI asistanlara) TopoHub projesi hakkında bağlam sağlar. Bu klasörde çalışan asistanlar buraya bakmalı.

## Proje Özü

TopoHub, topoloji eğitmeni Kadirhan Polat'ın öğrenciler için geliştirdiği, pi-base/web (MIT) forkundan türetilmiş, Türkçe arayüzlü topoloji bilgi tabanı. Kaynaklar:

- Pi-base orijinal: <https://topology.pi-base.org> ve <https://github.com/pi-base>
- TopoHub kök repo (bu klasör): <https://github.com/kadirhanpolat/topohub>
- TopoHub web fork: <https://github.com/kadirhanpolat/topohub-web>

## Şu Anki Durum (2026-05-31 itibarıyla)

İlk geliştirme oturumu tamamlandı. Versiyon 0.2.0 yayında.

**Çalışan özellikler:**
- TopoHub markası (her yerde, pi-Base atfı korunarak)
- TR/EN i18n + navbar dil seçici + localStorage kalıcılığı
- 80 özellik + 70 uzay Türkçe sözlük (graceful fallback ile)
- Sunum modu (`?present=1`): büyük font, navbar gizli, ←/→ ile gezinme, konum sayacı
- Sınıf modu (canlı oturum): hoca → öğrenci pathname + scrollY senkronu (polling, antivirüs-dayanıklı)
- Tam ekran butonu (hem hoca hem öğrencide tek tıkla)
- Questions sayfası sonsuz döngü güvenliği, exit race condition fix
- Windows uyumluluğu (glob path, build script, lint-staged)

**Çalışmayanlar / sınırlamalar:**
- Classroom state in-memory, single-instance — production'da Redis veya Cloudflare Durable Objects gerek
- ~163 özellik + ~152 uzay henüz Türkçe çevirisiz (fallback EN)
- Markdown body içerikleri EN (pi-base data'sından geliyor)
- Henüz yayınlanmadı (local-only)

## Mimari (Önemli Kararlar)

- **Dil**: TypeScript (sadece). Python tercih edildi başlangıçta ama pi-base ekosisteminin TypeScript olması nedeniyle terk edildi (2026-05-31).
- **Framework**: SvelteKit (pi-base'in seçimi, korundu)
- **Veri formatı**: Markdown + YAML frontmatter (`data/properties/*.md`, `data/spaces/*/README.md`, `data/theorems/*.md`)
- **Veri akışı**: `compile` paketi `data/` klasörünü izler, port 3141'de HTTP servis eder. `viewer` (port 5173) `.env`'deki `VITE_BUNDLE_HOST=http://localhost:3141` ile compile server'a bağlanır.
- **Çıkarım motoru**: pi-base'in TypeScript motoru, korundu (`web/packages/core/src/Logic/`)
- **i18n stratejisi**:
  - UI metinleri: `svelte-i18n` + `src/i18n/locales/{tr,en}.json`
  - Property/Space adları: ayrı sözlükler (`src/i18n/property-names/tr.json`, `space-names/tr.json`) + derived store overlay (`src/i18n/propertyNames.ts`, `spaceNames.ts`)
  - Locale tercihi `localStorage` anahtarı `topohub.locale`
- **Classroom senkronu**: SSE değil, **polling**. Antivirüs/proxy MITM (Kaspersky vb.) uzun süreli stream'leri buffer'lar; kısa GET istekleri her ortamda çalışır. (SSE endpoint hâlâ var, gelecekte alternatif olarak kullanılabilir.)
- **Sunum modu state**: URL query params (`present=1`, `host=xxx`, `follow=xxx`) — paylaşılabilir link demek, sayfa yenilemede kaybolmaz.

## Klasör Yapısı

```
topohub/                       <- bu kök git repo
├── data/                      <- pi-base/data klonu (ayrı git, gitignored)
├── web/                       <- kendi fork'unuz (ayrı git, gitignored)
│   ├── packages/core/         <- pi-base motor (build edilmeli: pnpm -C core build)
│   ├── packages/compile/      <- veri sunucusu (pnpm -C compile start, port 3141)
│   ├── packages/viewer/       <- SvelteKit uygulaması (pnpm -C viewer dev, port 5173)
│   │   ├── src/i18n/          <- TR/EN sözlükler ve overlay'ler
│   │   ├── src/lib/server/    <- classroom session state (in-memory)
│   │   ├── src/routes/api/    <- classroom endpoints (POST/GET/SSE)
│   │   └── src/components/PresentMode.svelte  <- sunum + sınıf modu kontrolü
│   └── packages/vscode/       <- VS Code eklentisi (dokunmadı)
└── (kök belgeler: README, CHANGELOG, CLAUDE, LICENSE, .gitignore)
```

## Çalıştırma

```bash
# Terminal 1
pnpm -C web/packages/compile start

# Terminal 2
pnpm -C web/packages/viewer dev

# Tarayıcı: http://localhost:5173
```

İlk seferde:
```bash
pnpm -C web install
pnpm -C web/packages/core build
```

### Sınıf Modu Test Akışı

1. Hoca: http://localhost:5173/spaces/S000043 → ▶ Sunum → 🎓 Sınıfa paylaş → bağlantıyı kopyala
2. Öğrenci: yeni sekmede linki aç (otomatik takip moduna geçer)
3. Hocada ←/→ veya scroll → öğrenci 0.5-1 saniye içinde takip eder
4. Hem hoca hem öğrenci üst ortada **⛶ Tam ekran** ile programatik tam ekrana geçebilir

## Pi-Base Forku Olarak Tutulan Bağlantı

- `web/` deposunda `upstream` remote: <https://github.com/pi-base/web>
- Upstream'den güncellemeleri çekmek: `git -C web fetch upstream && git -C web merge upstream/main`
- Çakışma muhtemelen i18n eklemelerimizde olur. Önemli upstream değişiklikleri Türkçe'ye yansıtın.

## Bilinen Tuzaklar

1. **localStorage cache çakışması**: Pi-base bundle'ı cache'ler. Veri formatı değiştiğinde eski cache crashlere sebep olabilir. Çözüm: tarayıcıda `localStorage.clear(); location.reload()` çalıştır veya gizli sekme.

2. **Windows + bash script**: Pi-base'in `bin/build` scripti bash. Windows'ta WSL yoksa çalışmaz. Cross-platform `bin/build.mjs` (Node.js) eklendi, `package.json`'da `node bin/build.mjs` çağrılıyor.

3. **Windows + glob v8**: `compile/src/fs.ts`'de pattern normalize edilmeli (backslash → forward slash) yoksa pi-base verisi okunamıyor.

4. **Trait `description` zorunluluğu**: Pi-base'in 7 trait dosyası boş description'a sahip. `compile/src/validations.ts`'de `required(trait, 'description', error)` kaldırıldı.

5. **Questions sayfası sonsuz döngü**: Veri boşken `rollOpenQuestion` while loop sonsuza giriyordu. Max 500 deneme sınırı eklendi.

6. **VITE_BUNDLE_HOST**: `viewer/.env`'deki bu değer `'fixture'` ise SSR'da `public/refs/heads/main.json` kullanılır; başka değerse compile server'a fetch edilir. Şu an `http://localhost:3141`.

7. **Antivirüs SSE buffer'lama**: Kaspersky vb. uzun süreli HTTP stream'leri buffer'lar. Sınıf modu polling kullanır (SSE değil), bu yüzden etkilenmez. Aynı sorunla başka özelliklerde karşılaşırsanız (örn. bundle hot reload SSE), polling alternatifi düşünün.

8. **SvelteKit reactive declaration drift**: Function-call içinde state assignment (`readParams(...)`) Svelte 4 tarafından derinlemesine track edilmiyor. Inline reactive declarations kullanın (`$: x = $page.url.searchParams.get(...)`) ki dependency'ler net olsun.

9. **beforeNavigate race condition**: `beforeNavigate` hook'u eski URL params'tan state'i okuyabilir. State değişikliği gerektiğinde (örn. exit) bir bayrak (`exiting`) ile hook'u atlamayı düşünün.

10. **Pi-base husky pre-commit hook + Windows**: `lint-staged` Windows'ta `pnpm lint` ile çalışmıyordu (cmd glob expansion). `web/package.json`'da `lint-staged`'i doğrudan `prettier --write` çağıracak şekilde değiştirildi.

## i18n Yeni Çeviri Eklemek

- **UI metni**: `src/i18n/locales/tr.json` ve `en.json` aynı anahtarla
- **Yeni özellik**: `src/i18n/property-names/tr.json`'a `"P000XXX": "Türkçe karşılık"` (LaTeX'i `$...$` ile koru)
- **Yeni uzay**: `src/i18n/space-names/tr.json`'a `"S000XXX": "Türkçe karşılık"`
- Eklemek için dev sunucusunu durdurmaya gerek yok; HMR otomatik günceller.

## Çeviri Konvansiyonları

Geleneksel Türk matematik literatürü (Mamak, Çoker):
- compact → tıkız (modern: kompakt)
- compactification → tıkızlaştırma
- indiscrete → aşikar topoloji
- Hausdorff → Hausdorff (özel isim, korunur)
- separable → ayrılabilir
- connected → bağlantılı

Modern alternatifleri tercih ederseniz JSON'larda değiştirin.

## Yol Haritası (Sıradakiler)

### Yakın vadeli (sonraki oturumlar)
1. **Deployment** — Cloudflare Pages'a yayınla. Compile output'unu statik bundle olarak yükle. Topology.pi-base.org modelini izle.
   - SvelteKit `@sveltejs/adapter-cloudflare` zaten kurulu (`viewer/package.json`).
   - Classroom state için Cloudflare Durable Object gerekli (in-memory yetmez).
2. **Türkçe sözlük genişletme** — kalan ~163 özellik + ~152 uzay. Otomatik script ile (LLM destekli) ilk taslak üretip elle düzeltmek mantıklı.
3. **Vurgu özelliği (sınıf modunda)** — hoca bir özelliğe tıkladığında öğrencinin ekranında o özellik vurgulansın. Pi-base'de zaten `emphasized` prop'u var Property linkinde.

### Orta vadeli
4. **Quiz / değerlendirme motoru** — Questions sayfasının üzerine, öğrenci cevap girer, doğru/yanlış geri bildirim.
5. **Öğrenci hesap sistemi** — Auth.js veya Clerk ile. Öğrencinin ilerlemesi kaydedilsin.
6. **Ders şablonları** — hoca önceden hazırladığı uzay/özellik koleksiyonlarını saklasın, sınıfta tek linkle açsın.

### Uzun vadeli
7. **LLM köprüsü** — doğal dilden formel sorguya çeviri ("kompakt ama Hausdorff olmayan bir uzay göster" → `compact + ~hausdorff`). Anthropic SDK ile.
8. **Mathlib/Lean eşlemesi** — her teoremin formal sürümüne link. Pi-base'in 902 teoreminin önemli kısmı Mathlib'de var.
9. **Markdown body Türkçeleştirme** — pi-base/data'daki uzay/özellik açıklamalarının Türkçe versiyonu. PR olarak upstream'e gönderilebilir veya data fork'unda tutulabilir.
10. **Z3 WASM ile OR'lu sorgu desteği** — pi-base motorunun yapamadığı disjunctive sorguları SAT solver ile çöz.

## Kullanıcı Tercihleri

- Türkçe iletişim
- Derinlemesine analiz ister (Opus + max effort sıklıkla)
- Pi-base'in tasarım kararlarına saygı (statik mimari, CC-BY atıf)
- Sınıfta canlı kullanım önceliği (offline çalışabilirlik, hızlı yükleme)
- Antivirüs/proxy gibi gerçek dünya engellerine dayanıklı çözümler (Kaspersky deneyiminden ders)
