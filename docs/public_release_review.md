# 公開前レビューの観点

このリポジトリを公開する前と、公開後に章を足していく間の定期的な点検で使う観点をまとめたものです。読者向けではなく、リポジトリを保守するための文書です。

- 対象: 追跡しているすべてのファイル（`git ls-files`）と、全履歴（すべてのブランチ・タグ・コミット）
- 実施の目安: 章や資料を足したとき、push する前、公開の直前（直前は全履歴を対象にする）
- 観点は3つ: 1節「機密情報の流出」、2節「権利侵害」、3節「リンク先が意図どおりか」。各節は「機械点検」と「目視点検」に分ける。機械点検で何も出なくても、目視点検は省かない
- 結果は4節「実施記録」に1行ずつ追記する。判断の経緯は [QA表](qa_log.md) にも書く

## 1. 機密情報の流出

### 1-1. 見る観点

| 観点 | 具体例 | 主な置き場所 |
|---|---|---|
| 認証情報 | APIキー、トークン、パスワード、秘密鍵 | 全ファイル・全履歴 |
| コミットの名義 | author・committer が GitHub の noreply のアドレスか | `git log` のメタデータ |
| 本文の個人情報 | 実名、実メール、アカウント名（意図して載せる著作権者の表示とリポジトリの URL は対象外） | `docs/`、`CLAUDE.md`、本文 |
| PC固有の情報 | ユーザー名を含むパス（手順書では `<ユーザー名>` と伏せる）、ドライブ構成、容量などの実測値 | `setup/`、Notebook の出力 |
| 個人の環境に関する記述 | 個人の生活を推測させる記述、作業環境の詳細 | `docs/idea_origin.md`、`docs/qa_log.md`、`CLAUDE.md` |
| 組み合わせ | 1つずつは無害でも、組み合わせると推測できる情報 | 文書をまたいで |
| 追跡してはいけないもの | `.venv/`・`checkpoints/`・`logs/`・`.env`・鍵・大きなバイナリ | `.gitignore` と `git ls-files` |
| 画像の写り込み | Notebook の出力・`figures/` の画像、SVG の埋め込み画像・外部参照 | `chapters/*/figures/`、`diagrams/` |

### 1-2. 機械点検

PowerShell で、リポジトリの直下で実行する。どれもファイルを読むだけで、変更はしない。日本語で照合するので、最初に文字コードを UTF-8 にする。

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
$OutputEncoding = [System.Text.Encoding]::UTF8

git log --all --format='%an <%ae> | %cn <%ce>' | Group-Object | Select-Object Count, Name

$excl = 'users\.noreply\.github\.com|noreply@anthropic\.com|@example\.(com|org)|git@github\.com'
git grep -nIE '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}' | Select-String -NotMatch $excl
git log --all -p | Select-String -AllMatches '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}' | ForEach-Object { $_.Matches.Value } | Where-Object { $_ -notmatch $excl } | Group-Object | Select-Object Count, Name

git grep -nIiE 'api[_-]?key|secret|token|passw(or)?d|BEGIN [A-Z ]*PRIVATE KEY|ghp_[A-Za-z0-9]|github_pat_|sk-[A-Za-z0-9]{10}'
git grep -nIE '/home/[a-z][a-z0-9_-]*/|[A-Za-z]:\\+Users\\+|/mnt/c/Users/'
git grep -nIE '[0-9]+(\.[0-9]+)? ?(GB|GiB|MB|TB)\b'

git -c core.quotepath=off ls-files | Select-String -Pattern '\.(env|pem|key|p12|pfx|tar|zip|vhdx)$'
git branch -a; git tag; git stash list
git grep -nE '<image|href="https?:|base64,' -- '*.svg'
```

ローカルのユーザー名と、保守する人が決めたキーワードでも、今の版と全履歴（`git log --all -p` の追加行）を検索する。キーワードの一覧は、この文書には書かない（公開される文書のため）。点検のたびに、保守する人の手元の一覧を使う。

Notebook に埋め込んだ画像のデータ（base64）は、検索の語に偶然一致することがある。当たったら、その行が画像のデータかどうかを確かめる。

### 1-3. 目視点検

- `docs/qa_log.md` に新しく足した行に、アカウント名・実メール・個人の環境に関する記述が入っていないか。
- `CLAUDE.md` と `docs/idea_origin.md` に新しく足した記述が、公開してよい書き方か。
- 新しく足した章の Notebook の出力（文字と画像）に、個人のパスや作業環境の情報が入っていないか。

## 2. 権利侵害

### 2-1. 見る観点

| 観点 | 具体例 | 主な置き場所 |
|---|---|---|
| 各文書の出典の注記 | 元にしたもの・逐語の転載でない旨 | 各章の Notebook の末尾、`overview/`・`setup/` の各文書の末尾 |
| ツールの出力の絵 | Gymnasium の描画の出力であること、Pillow で書き込んだこと、フォントのライセンス | 各章の README と Notebook の出典の節、`LICENSE.md` |
| 図 | 自作の図か。第三者の図・ロゴ・埋め込み画像が混ざっていないか | `diagrams/`、`chapters/*/figures/` |
| サンプルコード | 公式のチュートリアルや他のリポジトリのコードを、丸ごと転載していないか | Notebook、Markdown のコードブロック |
| 第三者のファイル | ライセンスが不明なファイル（PDF・フォント・画像等）が追跡されていないか | `git ls-files` |
| リポジトリのライセンス | `LICENSE.md` の範囲と第三者のソフトウェアの一覧が最新か。コピーレフトの依存が加わっていないか | `LICENSE.md` |

### 2-2. 機械点検

```powershell
git -c core.quotepath=off ls-files | Select-String -NotMatch '\.(md|svg|png|gif|ipynb)$|^\.gitignore$'
```

新しく使い始めたパッケージがあれば、導入したパッケージの登録情報（`importlib.metadata`）でライセンスを確かめ、`LICENSE.md` の一覧に足す。

### 2-3. 目視点検

- 前回以降に足した節が、公式の文書や記事の文章をほぼそのまま写していないか。
- 足したサンプルコードが、公式のコードと一致しすぎていないか。
- 出典の注記が、文書の書き換えで消えていないか。

## 3. リンク先が意図どおりか

### 3-1. 見る観点

| 観点 | 具体例 |
|---|---|
| 文書間のリンク | 相対パスのリンクの先が実在するか（Markdown と Notebook の Markdown セルの両方） |
| 節の参照 | 本文の「N節」などの参照が、今の見出しと合っているか |
| 外部リンクの実在 | リンク切れ・移転が無いか |
| 外部リンクの中身 | 版の固定（例: Gymnasium 1.3.0・PyTorch 2.14 の文書）と、リンクの文言と中身が合っているか |

### 3-2. 機械点検

- 文書間のリンク（Markdown）: public-release-review スキルの `check_links.py internal` に、対象の Markdown を `--files` で渡す（既定の対象は `README.md` と `docs/*.md` だけなので、`setup/`・`overview/`・`diagrams/`・`chapters/*/README.md` も渡す）。
- 文書間のリンク（Notebook）: Notebook の Markdown セルの相対リンクは `check_links.py` の対象外なので、nbformat で読んで確かめる。
- 外部リンク: 各文書の出典は、URL をそのまま書いた行が多く、`check_links.py` はリンクの書き方（`[...](URL)`）のものしか拾わない。追跡する Markdown と Notebook から URL をすべて拾い出し、そのドメインの一覧を確かめてから（外部への通信の承認は、この一覧で得る）、HEAD の要求（失敗時だけ GET で先頭の少量）で確かめる。ボット対策で 403 を返すサイト（creativecommons.org・readthedocs.io など）は、ブラウザに近い User-Agent で確かめる（このことも承認を得るときに伝える）。

### 3-3. 目視点検

- 節を足した・繰り下げた文書と、それを参照している文書の「N節」を読み直す。
- 前回以降に足した外部リンクを開いて、文言・版・内容が本文と合っているかを確かめる。

## 4. 実施記録

| 実施日 | 対象（範囲） | 結果の要約 | 対応 |
|---|---|---|---|
| 2026-10-07 | 全履歴を含む公開直前の点検（点検した時点のコミット数 38） | 機械点検: コミットの名義はすべて noreply。実メール・認証情報・ローカルのユーザー名・容量の値・追跡してはいけないファイル・過去にだけあったファイル・SVG の外部参照は無し。目視点検: 記録系の文書の一部に、公開に向けて整えたほうがよい記述があった。リンク: Markdown の文書間リンクの切れが1件。Notebook の相対リンクは切れ無し。外部 URL 26 件はすべて存在を確認。権利: LICENSE.md の範囲と第三者のソフトウェアの一覧（フォントを含む）がそろい、第三者のファイルの追跡は無し。独立したレビュー（静的な確認のみ）は2回で、結論はどちらも「条件付きで公開してよい」 | 記録系の文書の一部の記述を整え、切れたリンクを外した。履歴は書き換えない（ユーザーの判断）。作成環境に由来する値（Notebook の実行時刻、学習の秒数、著者の環境の注記）は残す（ユーザーの判断） |
| 2026-10-09 | 第3章の追加（`chapters/ch03_frozenlake/`）と関連する文書の更新。未 push のコミット 2 件 | 機械点検: コミットの名義は noreply。追加行に実メール・認証情報・個人のパス・容量の値は無し。目視点検: Notebook の出力に個人のパスや作業環境の情報は無し。リンク: 文書間のリンクの切れは無し（点検の文書の書き方の例 `[...](URL)` に当たる誤検知のみ）。新しい外部 URL 1 件（github.com）は存在を確認。権利: 新しいパッケージは無し。FrozenLake の描画の絵は第三者の画像素材を含むため使わず、図はすべて matplotlib で自作。独立したレビュー（静的な確認のみ）を1回行った | レビューの指摘（高1・中2・低6）をすべて直した |
