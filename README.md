# Gymnasium で順番に学ぶ強化学習

強化学習のライブラリ [Gymnasium](https://gymnasium.farama.org/) にそろっている標準の環境を、易しいものから順に解いていく教科書です。棒を立てる台車、凍った湖を渡るロボット、月面に着陸する宇宙船。どの章でも、まず学習アルゴリズムを動かしてエージェントが上達する様子を楽しみ、そのあとサンプルコードを読んで仕組みを理解し、最後に設定を変えて遊びます。

GitHub をブラウザで開けば、実行した結果を含めてそのまま読めます。グラフやコマ送りの図は Notebook の中で、GIF の動きは各章のフォルダの README.md で見られます。手元で動かす場合は、このリポジトリを clone（または ZIP でダウンロード）し、環境構築マニュアルに従って準備します。GPU は無くても構いません。

## 読む順番

| 順番 | 冊 | 内容 | 前提 |
|---|---|---|---|
| 1 | [環境構築マニュアル](setup/windows_setup.md) | Windows 11 に Python 3.13・PyTorch・Gymnasium・Stable-Baselines3 などを用意する | なし |
| 2 | [第0章 動作確認](chapters/ch00_setup_check/ch00_setup_check.ipynb) | ライブラリと装置を確かめ、CartPole をでたらめに動かして GIF にする（[GIF はこちら](chapters/ch00_setup_check/README.md)） | 環境構築マニュアル |
| 3 | [第1章 動かして楽しむ](chapters/ch01_first_training/ch01_first_training.ipynb) | Stable-Baselines3 の PPO で CartPole を学習させ、学習の前後と学習曲線を見比べる（[GIF はこちら](chapters/ch01_first_training/README.md)） | 第0章 |
| 4 | [第2章 Gymnasium の API の基本](chapters/ch02_gymnasium_api/ch02_gymnasium_api.ipynb) | 環境を手で動かして、観測・行動・報酬のやり取りを確かめ、自分で書いた規則で棒を立てる（[クラス図](diagrams/gymnasium_classes.md)） | 第1章 |

第3章（FrozenLake）以降は準備中です。

## ライセンス

文章と図は CC BY 4.0、コードは MIT License です。詳しくは [LICENSE.md](LICENSE.md) を見てください。
