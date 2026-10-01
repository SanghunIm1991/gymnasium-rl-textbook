# QA表

判断・承認のやり取りを記録する。

| 日付 | 工程 | 質問内容 | 回答内容 |
|---|---|---|---|
| 2026-10-01 | アイデアの理解 | 自作と Stable-Baselines3（SB3）の使い分けを、元アイデアにある Claude の解釈どおりにするか（第1部は NumPy で自作／第2部の DQN・REINFORCE は PyTorch で自作して SB3 と比べる／第3部以降は SB3 中心）。まずユーザーから「SB3 中心にできないか」と聞かれたため、SB3 には表形式の手法と REINFORCE が無いことを説明し、改めて3案（第1部だけ最小限自作して第2部以降は SB3 のみ〈推奨〉／すべて SB3〈Toy Text も one-hot の観測で DQN・PPO で解く〉／当初の解釈どおり）を示した | 当初の解釈どおり。第1部は NumPy で自作、第2部の DQN・REINFORCE は PyTorch で自作して SB3 と比べ、第3部以降は SB3 を主に使う。SB3 中心の案を検討した上での選択 |
| 2026-10-01 | Git環境 | GitHub の private リポジトリの名前（`gymnasium-rl-textbook`〈推奨〉／まだ GitHub には作らない） | `gymnasium-rl-textbook`。ローカルのフォルダ名と同じにする |
| 2026-10-01 | Git環境 | `.gitignore` の方針（案どおり〈推奨〉：Notebook の出力とグラフ・GIF はコミットし、venv・`.ipynb_checkpoints/`・学習途中の `checkpoints/`・`logs/`・`runs/`・`.env`・`.vscode/`・OS の生成ファイルは除外する／`.vscode/` は管理対象にする） | 案どおり |
| 2026-10-01 | Git環境 | `git push` の承認の粒度（都度確認〈推奨〉／commit と push を1セットにする） | 都度確認。commit は自動でよいが、push は毎回承認を得る。Notebook の出力に個人のパスが残るおそれがあるため、push の前に点検を挟む |
