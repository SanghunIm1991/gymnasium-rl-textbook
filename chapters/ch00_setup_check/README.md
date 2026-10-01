# 第0章 動作確認：CartPole をでたらめに動かした様子

[第0章の Notebook](ch00_setup_check.ipynb) の4節で作った GIF です。著者が確かめたところ、GitHub の private リポジトリでは Notebook の中の GIF が表示されなかったため（2026-10-01）、このページで見られるようにしています。

台車を、毎回でたらめに左右へ押した様子です（seed = 0）。棒は少しずつ傾き、18 回動かしたところで倒れてエピソードが終わります。GIF は、実際の CartPole の時間（1回の行動あたり 0.02 秒）の5倍ゆっくり再生しています。

![でたらめに動かした CartPole。棒が傾いていき、18 回で倒れる](figures/ch00_random_cartpole.gif)

CartPole の仕様（1回の行動あたり 0.02 秒など）の出典は、[第0章の Notebook](ch00_setup_check.ipynb) の末尾の「出典」の節にあります。絵は、Gymnasium（MIT License）の CartPole の描画処理が出力したものです。ライセンスは、リポジトリの [LICENSE.md](../../LICENSE.md) を見てください。
