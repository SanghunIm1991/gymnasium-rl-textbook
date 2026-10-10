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
| 5 | 概要資料（地図） | ここまでの体験と、これからの章をつなぐ4本の資料。順番は自由で、各章から何度でも戻って読める | 第2章 |
| | ・[強化学習](overview/rl.md) | 基本の言葉、考え方を分ける3つの軸、手法の地図と章の対応 | |
| | ・[Gymnasium](overview/gymnasium.md) | 環境の一覧と章の対応、基本の操作、ベクトル化環境 | |
| | ・[Stable-Baselines3](overview/sb3.md) | アルゴリズムと扱える行動の種類、学習・保存・評価の操作 | |
| | ・[PyTorch](overview/pytorch.md) | テンソル、自動微分、学習の基本の流れ（第7章から使う） | |
| 6 | [第3章 FrozenLake](chapters/ch03_frozenlake/ch03_frozenlake.ipynb) | 滑る氷の湖を、Q学習のサンプルで試行錯誤して渡り、湖の仕組みから計算で解く価値反復・方策反復と比べる（[GIF はこちら](chapters/ch03_frozenlake/README.md)） | 第2章・概要資料（強化学習） |
| 7 | [第4章 CliffWalking](chapters/ch04_cliffwalking/ch04_cliffwalking.ipynb) | 崖のそばのマス目を、SARSA と Q学習のサンプルで渡り、2つの手法が学ぶ道の違いから、方策オンと方策オフの違いを確かめる（[GIF はこちら](chapters/ch04_cliffwalking/README.md)） | 第3章 |
| 8 | [第5章 Taxi](chapters/ch05_taxi/ch05_taxi.ipynb) | 状態が 500 個ある町でタクシーに客を運ばせ、ε の減衰と行動マスクという探索の工夫を、外したときと比べて確かめる（[GIF はこちら](chapters/ch05_taxi/README.md)） | 第4章 |
| 9 | [第6章 Blackjack](chapters/ch06_blackjack/ch06_blackjack.ipynb) | ブラックジャックを、勝負を最後まで遊んでから報酬の平均で覚えるモンテカルロ法のサンプルで学ばせ、ルールから計算した最適な方策と比べる（[GIF はこちら](chapters/ch06_blackjack/README.md)） | 第5章 |
| 10 | [第7章 CartPole（DQN）](chapters/ch07_cartpole_dqn/ch07_cartpole_dqn.ipynb) | 連続した観測を区切った表の Q学習と、表をニューラルネットワークに置き換えた DQN（Stable-Baselines3 と、PyTorch の短いサンプル）で棒を立て、経験再生とターゲットネットワークを外して比べる（[GIF はこちら](chapters/ch07_cartpole_dqn/README.md)） | 第6章・概要資料（PyTorch） |
| 11 | [第8章 CartPole の続き（方策勾配法）](chapters/ch08_cartpole_reinforce/ch08_cartpole_reinforce.ipynb) | 行動を選ぶ確率を直接学ぶ方策勾配法で棒を立てる。Stable-Baselines3 の A2C で動かし、PyTorch の短い REINFORCE のサンプルを読んで、収益の標準化を外して比べ、第7章の DQN と結果を並べる（[GIF はこちら](chapters/ch08_cartpole_reinforce/README.md)） | 第7章 |
| 12 | [第9章 MountainCar／Acrobot](chapters/ch09_mountaincar_acrobot/ch09_mountaincar_acrobot.ipynb) | ゴールに着くまで報酬が変わらない環境で、でたらめな探索の難しさを測り、Stable-Baselines3 の DQN（RL Zoo の値）で山を登る台車と振り上げる振り子を学習させ、表形式の Q学習のサンプルで報酬設計（ポテンシャルに基づく形）を加えて比べる（[GIF はこちら](chapters/ch09_mountaincar_acrobot/README.md)） | 第8章 |

第10章（Pendulum）以降は準備中です。

## ライセンス

文章と図は CC BY 4.0、コードは MIT License です。詳しくは [LICENSE.md](LICENSE.md) を見てください。
