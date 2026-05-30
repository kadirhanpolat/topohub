# Changelog

## [0.1.0] — 2026-05-31

İlk sürüm. Pi-base/web v0.x forklayıp TopoHub markası altında Türkçe arayüz eklendi.

### Eklenen

**Marka**
- Pi-base markasından TopoHub'a tüm görünür yerlerde dönüşüm (navbar, footer, browser title, meta tags)
- Pi-Base CC-BY 4.0 atfı footer ve README'de korundu

**Uluslararasılaştırma (i18n)**
- `svelte-i18n` ile altyapı kurulumu
- Türkçe (varsayılan) + İngilizce dil desteği
- Navbar dil seçici (TR | EN), localStorage'da hatırlama
- Otomatik tarayıcı dili tespiti
- Çevrilen alanlar: navbar, sayfa başlıkları, footer, form etiketleri, Search/Filter/Examples, Questions sayfası, Home sayfası

**Türkçe Terim Sözlüğü**
- 80 özellik için Türkçe karşılık (`web/packages/viewer/src/i18n/property-names/tr.json`)
- 70 uzay için Türkçe karşılık (`space-names/tr.json`)
- Runtime overlay sistemi — sözlükte olmayan terimler İngilizce'ye fallback eder
- Property linkleri, formula input önerileri, detay sayfaları, listelerde Türkçe ad gösterimi

**Belgeler**
- Kök klasör için README.md, CHANGELOG.md, CLAUDE.md, LICENSE.md
- .gitignore

### Düzeltilen

**Windows Uyumluluğu**
- `web/packages/compile/src/fs.ts` — Glob v8'in Windows backslash'ı escape karakteri yorumlaması düzeltildi (path normalize)
- `web/packages/core/bin/build.mjs` — Bash script yerine cross-platform Node.js build script

**Veri Derleyici**
- `web/packages/compile/src/validations.ts` — Trait için description zorunluluğu kaldırıldı (7 trait dosyası boşken bile bundle derlenebilsin)
- `web/pnpm-workspace.yaml` — `allowBuilds` placeholder'ları `true` olarak ayarlandı (esbuild, sveltekit gibi paketler build script'leri çalıştırabilsin)

**UX**
- `web/packages/viewer/src/components/Questions/Questions.svelte` — `while` sonsuz döngüsü 500 denemeyle sınırlandı (veri boşken donmayı önler)
- `web/packages/viewer/src/routes/+layout.server.ts` — Fixture import'una düşürmeyi engelleyen mantık

### Konfigürasyon

- `web/packages/viewer/.env` — `VITE_BUNDLE_HOST=http://localhost:3141` (compile server endpoint)

### Bilinen Sınırlamalar

- Pi-base bundle'ı localStorage'da önbelleklenir; veri formatı değişince eski cache çakışabilir. Çözüm: `localStorage.clear()` veya gizli sekme.
- Türkçe sözlükte ~150 özellik + ~150 uzay henüz çevirisiz (graceful fallback ile İngilizce gösterilir).
- Markdown body (uzay/özellik açıklamaları) ve teorem ispatları İngilizce kalır (data kaynağından).
- Sınıf modu, quiz, öğrenci hesabı gibi pedagojik özellikler henüz yok (yol haritasında).
