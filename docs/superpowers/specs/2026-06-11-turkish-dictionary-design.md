# Tasarım Dokümanı: Türkçe Terim Sözlüğü Tamamlama

**Tarih:** 2026-06-11  
**Versiyon:** 0.3.0  
**Durum:** Onaylandı

## Özet

TopoHub'ın Türkçe terim sözlüğündeki 160 eksik özellik + 148 eksik uzay çevirisi tamamlanır. Çeviriler bu oturumda doğrudan yapılır; hiçbir harici script veya API çağrısı gerektirmez.

## Kapsam

| | Mevcut | Eksik | Toplam |
|---|---|---|---|
| Özellik (`property-names/tr.json`) | 83 | 160 | 243 |
| Uzay (`space-names/tr.json`) | 74 | 148 | 222 |

**Kapsam dışı:** Markdown body içerikleri, teorem isimleri, UI metinleri.

## Kaynak ve Hedef Dosyalar

- **Kaynak:** `data/properties/P000XXX.md` ve `data/spaces/S000XXX/README.md` frontmatter `name:` alanı  
- **Hedef:** `web/packages/viewer/src/i18n/property-names/tr.json` ve `space-names/tr.json`  
- Mevcut girişlere dokunulmaz; yalnızca eksik ID'ler eklenir.

## Çeviri Metodolojisi

### Öncelik Sırası

1. **CLAUDE.md sözlüğü** — yerleşik eşlemeler önce uygulanır:
   - compact → tıkız
   - compactification → tıkızlaştırma
   - connected → bağlantılı
   - separable → ayrılabilir
   - indiscrete → aşikar topoloji
   - Hausdorff → Hausdorff (korunur)

2. **Mevcut tr.json örüntüsü** — tutarlılık için:
   - "Locally X" → "Yerel X"
   - "Weakly X" → "Zayıf X"
   - "Countably X" → "Sayılabilir X"
   - "Hereditarily X" → "Kalıtsal X"
   - "Strongly X" → "Güçlü X"
   - "Perfectly X" → "Mükemmel X"
   - "Completely X" → "Tamamen X"

3. **Özel isimler korunur** — Hausdorff, Lindelöf, Menger, Rothberger, Čech, Fréchet, Tihonov, Urysohn, Corson, Stone, Baire, Sorgenfrey, Niemytzki, Knaster, Kuratowski, vb.

4. **LaTeX korunur** — `$...$` blokları olduğu gibi geçer; çevresindeki sözcükler Türkçeleşir.

5. **Yerleşmemiş terimler** (Sober, Cosmic, Spectral, Proximal, vb.) — İngilizce özel terim + Türkçe son ek: "Sober uzay", "Cosmic uzay", "Spectral uzay".

## Uygulama Akışı

1. Tüm eksik çeviriler tek geçişte `tr.json` dosyalarına yazılır.
2. EN↔TR karşılaştırma tablosu (ID | İngilizce | Türkçe) üretilir.
3. Kullanıcı tabloyu inceler, hatalı satırları işaretler.
4. Düzeltmeler uygulanır, değiştirilmiş JSON'lar commit edilir.
5. `CHANGELOG.md`'ye v0.3.0 girişi eklenir.

## Teslimatlar

- `web/packages/viewer/src/i18n/property-names/tr.json` (83 → 243 giriş)
- `web/packages/viewer/src/i18n/space-names/tr.json` (74 → 222 giriş)
- EN↔TR karşılaştırma tablosu
- `CHANGELOG.md` v0.3.0 güncellemesi
