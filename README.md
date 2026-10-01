# Gymnasium で順番に学ぶ強化学習

強化学習のライブラリ [Gymnasium](https://gymnasium.farama.org/) にそろっている標準の環境を、易しいものから順に解いていく教科書です。棒を立てる台車、凍った湖を渡るロボット、月面に着陸する宇宙船。どの章でも、まず学習アルゴリズムを動かしてエージェントが上達する様子を楽しみ、そのあとサンプルコードを読んで仕組みを理解し、最後に設定を変えて遊びます。

GitHub をブラウザで開けば、実行した結果を含めてそのまま読めます。グラフやコマ送りの図は Notebook の中で、GIF の動きは各章のフォルダの README.md で見られます。手元で動かす場合は、このリポジトリを clone（または ZIP でダウンロード）し、環境構築マニュアルに従って準備します。GPU は無くても構いません。

## 読む順番

| 順番 | 冊 | 内容 | 前提 |
|---|---|---|---|
| 1 | [環境構築マニュアル](setup/windows_setup.md) | Windows 11 に Python 3.13・PyTorch・Gymnasium・Stable-Baselines3 などを用意する | なし |
| 2 | [第0章 動作確認](chapters/ch00_setup_check/ch00_setup_check.ipynb) | ライブラリと装置を確かめ、CartPole をでたらめに動かして GIF にする（[GIF はこちら](chapters/ch00_setup_check/README.md)） | 環境構築マニュアル |

第1章（動かして楽しむ）以降は準備中です。

## ライセンス

文章と図は CC BY 4.0、コードは MIT License です。詳しくは [LICENSE.md](LICENSE.md) を見てください。
