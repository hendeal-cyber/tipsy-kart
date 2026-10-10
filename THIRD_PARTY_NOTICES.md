# Third-party notices

Tipsy Kart's own code is original. This repository vendors the following third-party files unmodified, each under its own licence:

| File | Project | Version | Licence |
| --- | --- | --- | --- |
| `public/vendor/three.module.min.js` | [three.js](https://threejs.org/), Copyright 2010-2024 Three.js Authors | r169 | MIT. The full text is in `public/vendor/THREE_LICENSE.txt`, and the SPDX header is kept in the file. |
| `public/vendor/qrcode.js` | [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator), Copyright (c) 2009 Kazuhiko Arase | 2.0.4 (`dist/qrcode.js`, per `docs/research/phone-controls.md`) | MIT. The original licence header is kept at the top of the file. "QR Code" is a registered trademark of DENSO WAVE INCORPORATED. |

npm dependencies (`ws`, `selfsigned`, `three`, and `playwright-core` for tests only) are installed by `npm install` and are not vendored. Their licences ship in `node_modules/`.

## MIT licence (qrcode-generator)

```
Copyright (c) 2009 Kazuhiko Arase

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
