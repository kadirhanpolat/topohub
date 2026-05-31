# Changelog

## [0.2.0] — 2026-05-31

Sınıf modu + sunum modu eklendi. Aynı geliştirme oturumunun ikinci yarısı.

### Eklenen

**Sunum modu (`?present=1`)**
- Sunum modu URL parametresi: navbar/footer/status gizlenir, font %40 büyür, container 1400px'e açılır
- Navbar'da "▶ Sunum" butonu (tek tıkla sunum modunu açar)
- ESC ile çıkış, sağ üstte yanıp sönen kırmızı "● Sunum modu · Çık" düğmesi
- Klavye gezinme: ←/PageUp (önceki), →/PageDown/Space (sonraki) — sadece /spaces/[id], /properties/[id], /theorems/[id] detay sayfalarında
- Sol üstte "12 / 222" konum göstergesi (mevcut koleksiyondaki yer)
- `beforeNavigate` hook: link tıklandığında `?present=1` parametresi otomatik korunur
- Üst ortada "⛶ Tam ekran" butonu — `requestFullscreen()` çağırır, F11 araması gereksiz (hem hoca hem öğrencide tek tık)
- `exiting` bayrağı ile race condition düzeltildi: ESC veya çıkış butonu sunum modundan temiz çıkar

**Sınıf modu — canlı oturum**
- Server: `lib/server/classroom.ts` (in-memory state), `POST /api/classroom/[id]` (hoca push), `GET /api/classroom/[id]` (öğrenci poll), `GET /api/classroom/[id]/events` (SSE, gelecek için)
- Hoca: sunum modunda "🎓 Sınıfa paylaş" butonu → 10 karakter random session ID üretir, modal'da öğrenci linki gösterir (kopyala/seç)
- Öğrenci: `?follow=xxx` linki ile bağlanır, server'ı 500ms aralıkla poll eder
- Senkronize edilen: pathname (sayfa) + scrollY (kaydırma konumu — 150ms throttle)
- "Canlı oturum · xxx" (hoca) ve "Hoca takip ediliyor" (öğrenci) durum göstergeleri sağ alt köşede
- **Polling SSE yerine seçildi:** Kaspersky ve diğer antivirüs/proxy yazılımları uzun süreli HTTP stream'leri buffer'lar; polling her ortamda çalışır

**i18n eklemeleri**
- `present.*` namespace'i: active, start, exit, share, shareTitle, shareHint, copy, copied, close, copyLink, broadcasting, following, fullscreen, fullscreenExit

### Düzeltilen

- **Sunum modu çıkış kilidi:** `beforeNavigate` hook'u eski URL params'tan `active`'i hâlâ true gördüğü için exit girişimini cancel + goto ile geri çeviriyordu (`exiting` bayrağı ile düzeltildi)
- **Reactive declaration drift:** Function-call içinde state assignment (`readParams(...)`) Svelte 4 tarafından derinlemesine track edilmiyordu; inline reactive declarations kullanıldı (`$: hostId = ... ?? ''` gibi)
- **Race condition (startSharing):** Yeni session ID URL'e eklenirken `hostIdOverride` ile pre-emptive state set edildi

### Bilinen Sınırlamalar

- Classroom state in-memory (dev için yeterli). Production'da Redis veya Cloudflare Durable Objects gerekir.
- Tek dev sunucu instance'ında çalışır.
- Hoca sekmesi kapanırsa session in-memory'de kalır, öğrencinin görüntüsü son pathname'de takılı kalır.

---

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
- `web/package.json` — `lint-staged` Windows için doğrudan `prettier --write` kullanır (önceki `pnpm lint` cmd üzerinde glob expansion yapamıyordu)

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
