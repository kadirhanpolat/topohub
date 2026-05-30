# CLAUDE.md

Bu dosya Claude Code'a (ve diğer AI asistanlara) TopoHub projesi hakkında bağlam sağlar. Bu klasörde çalışan asistanlar buraya bakmalı.

## Proje Özü

TopoHub, topoloji eğitmeni Kadirhan Polat'ın öğrenciler için geliştirdiği, pi-base/web (MIT) forkundan türetilmiş, Türkçe arayüzlü topoloji bilgi tabanı. Kaynaklar:

- Pi-base orijinal: <https://topology.pi-base.org> ve <https://github.com/pi-base>
- TopoHub kök repo (bu klasör): <https://github.com/kadirhanpolat/topohub>
- TopoHub web fork: <https://github.com/kadirhanpolat/topohub-web>

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

## Klasör Yapısı

```
topohub/                       <- bu kök git repo
├── data/                      <- pi-base/data klonu (ayrı git, gitignored)
├── web/                       <- kendi fork'unuz (ayrı git, gitignored)
│   ├── packages/core/         <- pi-base motor (build edilmeli: pnpm -C core build)
│   ├── packages/compile/      <- veri sunucusu (pnpm -C compile start, port 3141)
│   ├── packages/viewer/       <- SvelteKit uygulaması (pnpm -C viewer dev, port 5173)
│   │   └── src/i18n/          <- TR/EN sözlükler ve overlay'ler
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

## Yol Haritası

- Sınıf modu prototipi (paylaşılan link, vurgulama)
- Quiz/değerlendirme motoru
- Mathlib/Lean köprüsü (her teoremin formal sürümüne link)
- Cloudflare Pages'a deployment
- Daha çok Türkçe çeviri (özellik 80 → 243, uzay 70 → 222)
- Markdown body'lerde Türkçe açıklama (data tarafında)

## Kullanıcı Tercihleri

- Türkçe iletişim
- Derinlemesine analiz ister (Opus + max effort sıklıkla)
- Pi-base'in tasarım kararlarına saygı (statik mimari, CC-BY atıf)
- Sınıfta canlı kullanım önceliği (offline çalışabilirlik, hızlı yükleme)
