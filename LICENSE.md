# Lisanslar / Licenses

## TopoHub'a Özgü Değişiklikler

TopoHub kapsamında eklenen kod (Türkçe i18n altyapısı, sözlükler, marka değişiklikleri, Windows uyumluluk düzeltmeleri, bu kök klasördeki belgeler):

**MIT Lisansı**

Copyright (c) 2026 Kadirhan Polat

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Üçüncü Taraf Bağımlılıklar

### pi-base/web (web/ klasöründeki tüm orijinal kod)

**MIT Lisansı**, Copyright (c) 2014-2025 James Dabbs

Tam metin: `web/LICENSE.md`

### pi-base/data (data/ klasöründeki tüm matematik verisi)

**Creative Commons Attribution 4.0 International (CC-BY 4.0)**

Copyright (c) 2014-2025 Steven Clontz, James Dabbs ve katkıda bulunanlar

Tam metin: `data/LICENSE.md` ve <https://creativecommons.org/licenses/by/4.0/>

Bu lisans, kaynaklara atıf zorunlu kılar. TopoHub bu atfı şu yerlerde sağlar:

- Sitenin footer'ında ("Built on pi-Base")
- README.md ve CLAUDE.md belgelerinde
- HTML meta tags'lerde

### npm bağımlılıkları

`web/node_modules/` altındaki tüm paketler kendi lisanslarına tabidir. Ana bağımlılıklar:

- SvelteKit (MIT)
- Vite (MIT)
- svelte-i18n (MIT)
- @pi-base/core, /compile, /viewer (MIT — bu monorepo'nun parçaları)

Tam liste: `pnpm -C web ls --depth=0`
