# Windows での環境構築マニュアル

強化学習の面白さは、自分のパソコンの中でエージェントが少しずつ上達していく様子を眺めるところにあります。最初はすぐに倒れていた棒が、数分の学習のあとには台車の上でずっと立ち続けるようになります。この教科書では、そうした様子を Jupyter Notebook の中で実際に動かしながら学びます。

このマニュアルは、そのための道具を Windows 11 のパソコンに一から用意する手順書です。ここで用意する環境は、この後のすべての章で使います。最後まで進めると、第0章（動作確認）の Notebook を開ける状態になります。

- **想定環境**: Windows 11（64 ビット）、インターネットに接続できること
- **前提**: なし（この教科書で最初に読む冊です）
- **所要の目安**: 30〜60 分（ダウンロードの速さによります）
- **GPU**: 無くても構いません。この教科書は CPU だけで進められるように作っています。各章の冒頭に、使う装置と CPU での学習時間の目安を書きます

> **注記**
> - **確認日**: 版の番号とコマンドは、2026-10-01 に公式の文書と配布元（python.org・docs.python.org・PyPI・PyTorch の公式リポジトリ）で確かめたものです。新しい版が出ていることがあるので、食い違う場合は公式の文書を優先してください。
> - **期待する結果の出どころ**: 3-2節の `py -3.13 --version` と `py -0p` の表示と、6-2節の版の確認の表示は、著者の環境で実際に確かめたものです（2026-10-01）。インストーラの画面の説明と、4節〜6-1節・7節の表示は、公式の文書と PyPI に登録された依存関係の情報から想定したものです。ライブラリの版の番号や、一緒に入る依存ライブラリの顔ぶれは、実行した時期によって変わります。
> - **GPU 版の手順**（5-2節）は、公式の情報をもとに書いたもので、著者の環境では動作を確かめていません。PyTorch の公式サイトの画面の選択肢の名前も確かめていません。
> - **8節の表**の一部（2行目）は、著者の環境で起きた現象と、そこからの推定にもとづいています。
> - **実行環境が無くても読めるように**: 各手順の直後に、成功したときの表示と、その読み方を書いています。

## 0. 学習目標と完了条件

このマニュアルを終えると、次のことができるようになります。

1. Python 3.13 を入れ、教材のフォルダに専用の仮想環境（`.venv`）を作れる
2. 仮想環境に PyTorch・Gymnasium・Stable-Baselines3 などを入れ、版を表示して確かめられる
3. VS Code で教材の Notebook を開き、仮想環境をカーネルとして選べる

完了条件は、6-2節の確認コマンドで各ライブラリの版が表示され、7節で第0章の Notebook のカーネルに `.venv` を選べることです。

## 1. 全体像

用意するものは、下から順に積み上がっています。

| 順番 | 用意するもの | 役割 | 節 |
|---|---|---|---|
| 1 | 教材のフォルダ | Notebook と図が入っている。この中で作業する | 2節 |
| 2 | Python 3.13 | プログラムを動かす土台 | 3節 |
| 3 | 仮想環境（`.venv`） | この教科書のためだけのライブラリ置き場 | 4節 |
| 4 | PyTorch | ニューラルネットワークの計算を受け持つ | 5節 |
| 5 | Gymnasium・Stable-Baselines3 ほか | 強化学習の環境と、学習アルゴリズムの実装 | 6節 |
| 6 | VS Code と拡張機能 | Notebook を開いて実行する | 7節 |

**仮想環境**とは、プロジェクトごとに分けたライブラリの置き場です。ほかの用途で入れた Python のライブラリと版がぶつからないように、この教科書用のライブラリはすべてここに入れます。

## 2. 教材を入手する

教材のフォルダを、作業しやすい場所に置きます。以降の手順はすべて、このフォルダの中で行います。

- **Git を使う場合**: PowerShell で、置きたい場所に移動してから次を実行します。

```powershell
git clone <この教材のリポジトリのURL>
```

- **Git を使わない場合**: GitHub のリポジトリの画面で「Code」→「Download ZIP」を選び、ダウンロードした ZIP ファイルを展開します。

<!-- TODO（著者用）: 公開の形が決まったら、リポジトリの URL を書き入れる -->

ここから先のコマンドは、**教材のフォルダ（`README.md` があるフォルダ）で開いた PowerShell** で実行します。エクスプローラーで教材のフォルダを開き、アドレスバーに `powershell` と入力して Enter を押すと、そのフォルダで PowerShell が開きます。

## 3. Python 3.13 を入れる

この教科書では Python 3.13 を使います。3.13 を選んだのは、この教科書で使う主なライブラリ（Gymnasium 1.3.0・Stable-Baselines3 2.9.0・PyTorch 2.14）が、そろって対応している最も新しい版だからです（2026-10-01 時点）。特に、LunarLander などの物理シミュレーションに使う `box2d` は、Windows 向けのビルド済みのファイルが 3.13 用までしか配布されていません。それより新しい Python では、パソコンの上でビルドが必要になり、導入でつまずきやすくなります。

### 3-1. インストーラで入れる

1. [python.org の Windows 版のダウンロードページ](https://www.python.org/downloads/windows/)を開き、Python 3.13 の最新版（2026-10-01 時点では 3.13.16）の「Windows installer (64-bit)」をダウンロードします。ファイル名は `python-3.13.16-amd64.exe` のようになります。
2. ダウンロードしたファイルを実行します。最初の画面の下にある「Add python.exe to PATH」のチェックは、外したままで構いません。この教科書では、Python を `py` コマンド（Python launcher）から呼ぶためです。
3. 「Install Now」を選び、終わるまで待ちます。

### 3-2. 入ったことを確かめる

PowerShell を開き直してから、次を実行します。

```powershell
py -3.13 --version
```

**期待する結果**:

```text
Python 3.13.16
```

`Python 3.13.` で始まる版が表示されれば成功です（末尾の番号は、入れた時期によって変わります）。

入っている Python の一覧は `py -0p` で見られます。

**期待する結果**（ほかの Python が入っているパソコンの例。一覧の中身はパソコンによって変わります）:

```text
 -V:3.13 *        C:\Users\<ユーザー名>\AppData\Local\Programs\Python\Python313\python.exe
 -V:3.9           C:\Program Files (x86)\Microsoft Visual Studio\Shared\Python39_64\python.exe
```

`-V:3.13` の行があれば成功です。`*` は、版を指定せずに `py` を実行したときに使われる Python の印です。

> **Python install manager について**: python.org は、新しい導入方法として **Python install manager**（`py install 3.13` のように、コマンドで Python を入れたり切り替えたりする道具）を勧め始めています。従来のインストーラは Python 3.14 から非推奨になり、3.16 以降は作られない予定です（2026-10-01 時点、[Python の公式文書](https://docs.python.org/3.14/using/windows.html)による）。この教科書で使う 3.13 は従来のインストーラで入れられるので、このマニュアルでは従来のインストーラを使います。

## 4. 仮想環境を作る

教材のフォルダで次を実行します。フォルダの中に `.venv` という名前の仮想環境ができます。

```powershell
py -3.13 -m venv .venv
```

**期待する結果**: 何も表示されずに終わり、教材のフォルダに `.venv` フォルダができます。

続けて、仮想環境の pip（ライブラリを入れる道具）を新しくします。

```powershell
.venv\Scripts\python -m pip install --upgrade pip
```

**期待する結果**（抜粋。`<…>` の部分は実行した時期によって変わります）:

```text
Requirement already satisfied: pip in .\.venv\Lib\site-packages (<元の版>)
Collecting pip
  Downloading pip-<新しい版>-py3-none-any.whl.metadata (<サイズ>)
...
Successfully installed pip-<新しい版>
```

最後の行が `Successfully installed pip-...` であれば成功です。仮想環境に入っていた pip がすでに最新のときは、`Requirement already satisfied` の行だけで終わります。これも成功です。

> **仮想環境の「有効化」について**
> - **一般的な書き方**: 公式の文書は、`.venv\Scripts\Activate` で仮想環境を有効にしてから `python` や `pip` を使う方法を勧めています。
> - **このマニュアルで変えた理由**: Windows の PowerShell は、初期設定ではスクリプトの実行が制限されていて、有効化のスクリプトが動かないことがあります。この制限を変えずに済むよう、このマニュアルでは `.venv\Scripts\python` を直接呼びます。結果は有効化した場合と同じです。
> - **実務での目安**: 実行の制限を自分で管理できる環境では、有効化して使うほうが手短です。

## 5. PyTorch を入れる

PyTorch は、ニューラルネットワークの計算を受け持つライブラリです。この教科書の学習アルゴリズム（Stable-Baselines3）も、内部で PyTorch を使います。PyTorch には CPU だけで動く版と、NVIDIA の GPU を使う版があり、入れ方が違います。

**迷ったら CPU 版**を選んでください。この教科書で主に使う小さなネットワークは、GPU よりも CPU のほうが速いことがあります（Stable-Baselines3 の PPO は、画像を入力にしない設定で GPU を使うと、CPU を勧める警告を出します）。GPU が効いてくるのは、主に画像を入力にする場合や大きなネットワークの場合で、この教科書では任意の第13章（MuJoCo）で効いてくる見込みです。

### 5-1. CPU 版

```powershell
.venv\Scripts\python -m pip install torch --index-url https://download.pytorch.org/whl/cpu
```

`--index-url` は、PyTorch 公式の配布元のうち、CPU 版が置かれている場所を指定するオプションです。

**期待する結果**（末尾の抜粋。依存ライブラリの版の番号は `<…>` で省略）:

```text
Looking in indexes: https://download.pytorch.org/whl/cpu
Collecting torch
  Downloading https://download.pytorch.org/whl/cpu/torch-2.14.1%2Bcpu-cp313-cp313-win_amd64.whl (<サイズ>)
...
Successfully installed MarkupSafe-<…> filelock-<…> fsspec-<…> jinja2-<…> mpmath-<…> networkx-<…> setuptools-<…> sympy-<…> torch-2.14.1+cpu typing-extensions-<…>
```

最後の行に、`+cpu` が付いた `torch-2.14.1+cpu` が含まれていれば成功です。ほかの名前は、PyTorch が使う補助のライブラリで、一緒に入ります。ファイルは数百 MB あるので、ダウンロードに数分かかることがあります。

### 5-2. GPU（CUDA）版（著者の環境では未検証）

NVIDIA の GPU を使う場合の手順です。

1. NVIDIA のドライバが入っているか確かめます。PowerShell で `nvidia-smi` を実行し、表の右上に `CUDA Version: <版の番号>` が表示されれば、ドライバは入っています。コマンドが見つからない場合は、NVIDIA の公式サイトから GPU に合ったドライバを入れます。
2. [PyTorch の公式サイトの「Get Started」](https://pytorch.org/get-started/locally/)で、「Stable」「Windows」「Pip」「Python」と、CUDA の版を選びます。CUDA の版は、手順1で表示された `CUDA Version` 以下のものを選びます。PyTorch 2.14 では CUDA 12.6・13.0・13.2 が選べます（2026-10-01 時点、PyTorch の公式リポジトリの対応表による）。
3. 表示されたコマンドの `pip3` を `.venv\Scripts\python -m pip` に置き換えて実行します。たとえば CUDA 12.6 を選んだ場合は次のようになります。

```powershell
.venv\Scripts\python -m pip install torch --index-url https://download.pytorch.org/whl/cu126
```

**期待する結果**（末尾の抜粋。CUDA 12.6 を選んだ場合）:

```text
Successfully installed ... torch-2.14.1+cu126 ...
```

`torch-` の後ろに、選んだ CUDA の版を表す `+cu126` のような印が付いていれば成功です。`+cpu` になっている場合は、CPU 版が入っています。手順3のコマンドの `--index-url` を確かめてください。GPU を実際に使えるかどうかは、第0章の Notebook で確かめます。

## 6. Gymnasium・Stable-Baselines3 ほかを入れる

### 6-1. まとめて入れる

```powershell
.venv\Scripts\python -m pip install "gymnasium[classic-control,toy-text,box2d]" stable-baselines3 tensorboard optuna matplotlib imageio ipykernel nbconvert
```

入れるものと、教科書の中での役割は次のとおりです。

| ライブラリ | 役割 |
|---|---|
| `gymnasium` | 強化学習の環境（CartPole など）。`[...]` の中は、使う環境の分類ごとの追加分。`classic-control`（CartPole など）・`toy-text`（FrozenLake など）は画面の描画に、`box2d`（LunarLander など）は物理シミュレーションに必要なものを足す |
| `stable-baselines3` | PPO・DQN などの学習アルゴリズムの実装 |
| `tensorboard` | 学習の進み具合をグラフで見る |
| `optuna` | 学習の設定（ハイパーパラメータ）を自動で探す |
| `matplotlib`・`imageio` | 学習曲線のグラフと、動きの GIF を作る |
| `ipykernel`・`nbconvert` | Notebook から仮想環境を使う、Notebook をまとめて実行する |

**期待する結果**（末尾の抜粋。一緒に入る依存ライブラリは多いので、主なものだけを残して `...` で省略）:

```text
Collecting gymnasium[box2d,classic-control,toy-text]
  Downloading gymnasium-1.3.0-py3-none-any.whl.metadata (<サイズ>)
...
Collecting box2d==2.3.10 (from gymnasium[box2d,classic-control,toy-text])
  Downloading box2d-2.3.10-cp313-cp313-win_amd64.whl.metadata (<サイズ>)
...
Successfully installed ... box2d-2.3.10 ... gymnasium-1.3.0 ... matplotlib-<…> ... numpy-<…> ... optuna-<…> ... pygame-ce-<…> ... stable-baselines3-2.9.0 ... swig-<…> ... tensorboard-<…> ...
```

最後の行が `Successfully installed` で始まり、エラー（`ERROR:`）が出ていなければ成功です。`box2d` の行で、ファイル名が `cp313-cp313-win_amd64.whl` で終わっていることも見ておきます。これは、Python 3.13 の Windows 用にビルド済みのファイルが選ばれたという意味です。

### 6-2. 版を確かめる

```powershell
.venv\Scripts\python -c "import sys, gymnasium, stable_baselines3, torch; print(sys.version.split()[0], gymnasium.__version__, stable_baselines3.__version__, torch.__version__)"
```

**期待する結果**（CPU 版の場合）:

```text
3.13.16 1.3.0 2.9.0 2.14.1+cpu
```

左から Python・Gymnasium・Stable-Baselines3・PyTorch の版です。4つとも表示されれば成功です。後から入れた場合は、より新しい版の番号になっていることがあります。

## 7. VS Code で Notebook を開く

1. [VS Code](https://code.visualstudio.com/) を入れます。
2. VS Code の拡張機能の画面（左端の四角が4つ並んだアイコン）で、Microsoft が提供する「**Python**」と「**Jupyter**」を検索して入れます。
3. 「ファイル」→「フォルダーを開く」で、教材のフォルダを開きます。
4. `chapters/ch00_setup_check/ch00_setup_check.ipynb` を開きます。
5. 右上の「カーネルの選択」→「Python 環境」で、`.venv` を選びます。

**期待する結果**: 右上の表示が `.venv (Python 3.13.16)` のようになります。これで第0章に進む準備ができました。

## 8. うまくいかないとき

| 症状 | 考えられる原因と対処 |
|---|---|
| `py` が見つからない | Python launcher が入っていません。3-1節のインストーラを実行し直し、「Modify」でオプションの「py launcher」にチェックが入っているかを確かめます。そのあと、PowerShell を開き直します |
| Python 3.13 を入れたあと、以前から使っていた別の Python（Anaconda など）が `py -0p` の一覧から消えた | 3.13 のインストーラは、Python launcher も新しい版に更新します。新しい launcher では、それまで一覧に出ていた Python が出なくなることがあります（著者の環境では Anaconda で起きました。Windows への登録のされ方によると考えられます）。この教科書の作業には影響しません。消えた Python は、`py` を使わず、その `python.exe` をフルパスで指定すれば今までどおり使えます |
| 6-1節で `box2d` のビルド（`Building wheel for box2d`）が始まり、失敗する | `box2d` は Python 3.10〜3.13 用にビルド済みのファイルが配布されています（2026-10-01 時点）。ビルドが始まるのは、仮想環境の Python がこれ以外の版のときです。6-2節のコマンドで Python の版を確かめ、3.13 で仮想環境を作り直します |
| VS Code のカーネルの一覧に `.venv` が出ない | 教材のフォルダ（`.venv` があるフォルダ）を開いているかを確かめます。それでも出ない場合は、VS Code を再起動します |

## 次に読むもの

- [第0章 動作確認](../chapters/ch00_setup_check/ch00_setup_check.ipynb)

## 出典

このマニュアルは、次の公式の文書と配布元の情報（2026-10-01 確認）をもとに、著者の言葉でまとめたものです。逐語の転載ではありません。

- Python Software Foundation, "Using Python on Windows"（Python 3.14 のドキュメント）: https://docs.python.org/3.14/using/windows.html
- python.org, "Python Releases for Windows": https://www.python.org/downloads/windows/
- PyTorch, "Release Compatibility Matrix"（`RELEASE.md`）: https://github.com/pytorch/pytorch/blob/main/RELEASE.md
- PyPI の各パッケージのページ（gymnasium・stable-baselines3・torch・box2d）

次のページは、導入の入口として案内しているもので、内容は確かめていません。

- PyTorch, "Get Started": https://pytorch.org/get-started/locally/
