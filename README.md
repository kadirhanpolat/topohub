# TopoHub

Topoloji öğretimi için etkileşimli web uygulaması. [pi-Base](https://github.com/pi-base) açık kaynak altyapısı üzerine kurulu, Türkçe arayüz ve Türkçe terim sözlüğüyle genişletilmiş.

> **TopoHub** is a topology teaching tool built on the [pi-Base](https://github.com/pi-base) open-source infrastructure, extended with a Turkish UI and a Turkish term dictionary for use in classroom settings.

---

## İçindekiler / Contents

- [Ne Var?](#ne-var)
- [Kurulum](#kurulum)
- [Çalıştırma](#çalıştırma)
- [Klasör Yapısı](#klasör-yapısı)
- [Lisans ve Atıflar](#lisans-ve-atıflar)

---

## Ne Var?

| | |
|---|---|
| **Uzay sayısı** | 222 |
| **Özellik sayısı** | 243 |
| **Teorem sayısı** | 902 |
| **Trait sayısı** | 2099 |
| **Diller** | Türkçe, İngilizce (otomatik tespit + manuel seçici) |
| **Türkçe terim sözlüğü** | 80 özellik + 70 uzay (genişletilebilir) |

Pi-Base'in tüm matematiksel verisini ve çıkarım motorunu kullanır; üstüne TopoHub'ın eklediği özellikler:

- **Türkçe arayüz** — navbar, başlıklar, footer, ana sayfa, formlar
- **Türkçe terim sözlüğü** — `compact → tıkız`, `hausdorff → Hausdorff`, `sorgenfrey line → Sorgenfrey doğrusu` gibi
- **Marka** — TopoHub (pi-Base atıfı korunur)
- **Windows uyumluluğu** — build script ve glob path düzeltmeleri
- **Questions sayfası güvenliği** — sonsuz döngü riski giderildi

---

## Kurulum

Gereksinimler:

- **Node.js 20+** (geliştirme `v24` ile yapıldı)
- **pnpm 11+** (`npm install -g pnpm`)
- **Git** (data ve web repolarını klonlamak için)
- **gh CLI** (opsiyonel, fork için kolaylık)

İlk kurulum:

```bash
# 1. Kök klasörü klonla (bu repo)
git clone <topohub-master-repo> topohub
cd topohub

# 2. pi-base/data'yı al
git clone https://github.com/pi-base/data.git

# 3. Kendi fork'unuzu (web) klonla
git clone https://github.com/<kullaniciAdi>/topohub.git web

# 4. Bağımlılıkları kur
cd web
pnpm install
```

---

## Çalıştırma

İki süreç çalışır:

```bash
# Terminal 1 - Veri sunucusu (port 3141)
pnpm -C web/packages/compile start

# Terminal 2 - Web sunucusu (port 5173)
pnpm -C web/packages/viewer dev
```

Tarayıcıda: <http://localhost:5173>

İlk çalıştırma için `core` paketini build edin:

```bash
pnpm -C web/packages/core build
```

---

## Klasör Yapısı

```
topohub/
├── data/                  # pi-base/data klonu (CC-BY 4.0 veri)
├── web/                   # pi-base/web forku (MIT, kendi düzenlemelerinizle)
│   └── packages/
│       ├── core/          # Veri modeli, çıkarım motoru
│       ├── compile/       # Veri bundle derleyici (port 3141)
│       ├── viewer/        # SvelteKit web uygulaması (port 5173)
│       │   └── src/i18n/  # TR/EN çeviriler + property/space sözlükleri
│       └── vscode/        # VS Code eklentisi
├── README.md
├── CHANGELOG.md
├── CLAUDE.md              # Yapay zeka asistan rehberi
└── LICENSE.md
```

---

## Lisans ve Atıflar

TopoHub'a özgü değişiklikler: **MIT** (LICENSE.md)

Bağımlı kaynaklar:

- **pi-base/web** — MIT, © 2014-2025 James Dabbs
- **pi-base/data** — CC-BY 4.0, © 2014-2025 Steven Clontz & James Dabbs

Atıf zorunlu — pi-base verisinin orijinaline ve katkıda bulunanlara teşekkürler.

---

## Türkçe Terim Sözlüğü Hakkında

`web/packages/viewer/src/i18n/property-names/tr.json` ve `space-names/tr.json` dosyalarında. Yeni çeviri eklemek için yalnızca JSON'a yeni `"PXXXXXX": "Türkçe karşılık"` veya `"SXXXXXX": "Türkçe karşılık"` satırı eklemek yeter.

Çeviri kararları geleneksel Türk matematik literatürünü (Mamak, Çoker) yansıtacak şekilde yapıldı:
- `compact → tıkız`
- `compactification → tıkızlaştırma`
- `indiscrete → aşikar topoloji`

Modern alternatif terimler (`kompakt`, `kaba`) tercih ediyorsanız sözlük dosyalarında değiştirebilirsiniz.
