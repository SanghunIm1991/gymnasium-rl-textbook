# ライセンス

この教科書は、文章とコードで別のライセンスを使っています。

| 対象 | ライセンス |
|---|---|
| 文章と図（Markdown のファイル、Notebook の Markdown のセル、`figures/`・`diagrams/` の画像。下の行のコードブロックを除く） | [クリエイティブ・コモンズ 表示 4.0 国際（CC BY 4.0）](https://creativecommons.org/licenses/by/4.0/legalcode.ja) |
| コード（Notebook のコードのセル、Python のファイル、Markdown のファイルや Notebook の Markdown のセルの中のコードブロック） | MIT License（下に全文） |

著作権者: Copyright (c) 2026 SanghunIm1991

## MIT License

```text
MIT License

Copyright (c) 2026 SanghunIm1991

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
```

## 第三者のソフトウェア

この教科書は、次のソフトウェアを使っています。リポジトリには含めておらず、読者が環境構築マニュアルに従って PyPI 等から導入します。ライセンスは、各パッケージに登録された情報（2026-10-01 確認）によります。

| ソフトウェア | ライセンス | この教科書との関わり |
|---|---|---|
| Gymnasium（Farama Foundation） | MIT License | 環境。第0・1章の `figures/` の環境の絵（GIF 等）は、Gymnasium の描画処理が出力したもの（第3章の地図・GIF は、Gymnasium の描画を使わず matplotlib で描いたもの） |
| Stable-Baselines3 | MIT License | 学習アルゴリズム |
| PyTorch | BSD-3-Clause ほか（複数のライセンスの組み合わせ） | ニューラルネットワークの計算 |
| NumPy | BSD-3-Clause ほか（複数のライセンスの組み合わせ） | 数値計算 |
| matplotlib | Python Software Foundation License に基づく matplotlib のライセンス | グラフと図の作成 |
| imageio | BSD-2-Clause | GIF の作成 |
| Pillow | MIT-CMU License | 絵への線と文字の書き込み。文字は Pillow に同梱の既定のフォント Aileron Regular（dotcolon.net、「No Rights Reserved」＝ CC0 相当）で描いている |
| TensorBoard | Apache License 2.0 | 学習の記録の書き出しと、グラフでの表示 |
| IPython | BSD-3-Clause | Notebook の中での画像の表示（`IPython.display.Image`） |
| pygame-ce | LGPL v2.1 | Gymnasium の環境の描画 |
| Box2D（`box2d`） | zlib License | 物理シミュレーションの環境 |

参照した公式の文書は、各冊の末尾の「出典」に書いています。文章は著者の言葉でまとめたもので、逐語の転載はしていません。
