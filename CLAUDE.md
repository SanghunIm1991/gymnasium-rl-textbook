# gymnasium-rl-textbook

Gymnasium の標準環境を易しい順に解いていく、強化学習の自作教科書。元アイデアは `docs/idea_origin.md`、判断の経緯は `docs/qa_log.md`（QA表）にある。

## 教科書の方針（`docs/idea_origin.md` からの更新分）

`docs/idea_origin.md` は brainstorming から引き継いだ元の記録として変更しない。そこから変わった方針はこの節に書く（経緯は QA表）。

- 優先順位: ①強化学習を楽しむ（学習者の実装の負担を減らす）→ ②サンプルコードの解説で技術要素の理解を深める
- 学習者の役割は「動かして、読んで、パラメータをいじる」こと。コードを書くことは求めない
- 学習は主に Stable-Baselines3（SB3）で行う。表形式の手法（NumPy）と DQN・方策勾配（PyTorch の短いコード）は、教科書側が用意する解説用のサンプルにする
- 各章の流れ: SB3 で動かして楽しむ → サンプルコードで仕組みを読む → パラメータを変えて遊ぶ
- 第0章の次に、SB3 で数行で学習させて GIF で見る「動かして楽しむ」導入章を置く
- 追加のツール: TensorBoard（GitHub で見られるように matplotlib の図も併用する）、RL Zoo の調整済みハイパーパラメータ（出典を明記する）、Optuna
- 学習者の実行環境: Windows のローカルのみ
- 環境構築マニュアルの GPU 版の手順は、公式で確認して書き、著者の環境では未検証と明記する（このPCには nvidia-smi が無い）
- 作る順番: 最初に「環境構築マニュアル（CPU 版）＋第0章＋動かして楽しむ導入章」を一通り作り、概要資料はそのあとに書く

## このPCでの執筆環境

- Python 3.13（python.org 版）から作るプロジェクト専用の `.venv` を使う。導入はユーザーが行う。anaconda base には入れない
- venv は有効化せず、`.venv\Scripts\python` を直接呼ぶ
- PATH 上の `code` コマンドは Cursor 側が先に見つかる。VS Code の CLI が必要なときはフルパスで呼ぶ

## Git運用

- コミット規約・禁止操作は `git-conventions` スキルに従う
- push の承認: **都度確認**。commit は作業完了時に自動で行ってよいが、`git push` は毎回承認を得る
- リモート: GitHub の private リポジトリ `gymnasium-rl-textbook`（ブランチは `main`）
- push の前に、Notebook の出力に個人のパス（`C:\Users\<ユーザー名>\...` 等）や機微情報が残っていないか点検する
