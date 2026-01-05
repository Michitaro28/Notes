# uv
uvはPythonのパッケージ管理ツールで、pipやpoetryと同じように使える。Rustで作れられているためとても早い。

- [公式ドキュメント](https://docs.astral.sh/uv/)

**参考リンク**
- [Pythonパッケージ管理 [uv] 完全入門](https://speakerdeck.com/mickey_kubo/pythonpatukeziguan-li-uv-wan-quan-ru-men)
- [【Python】uvで始めるPythonプロジェクト](https://qiita.com/kissy24/items/0c091bb5f12d697131ae)

## コマンドリスト

|コマンド|処理内容|
| :-- | :-- |
| uv --version| バージョン表示|
| uv venv list|作られている仮想環境のリストを表示|
| uv venv| デフォルトで.venv仮想環境を作成|
| uv venv <特定の名前>|特定の名前で仮想環境を作成|
| source .venv/bin/activate|仮想環境の有効化（Linux/macOS）|
| .venv\Scripts\activate|仮想環境の有効化（Windows）|
| uv pip install <package>|仮想環境にパッケージのインストール|
| uv pip list| インストール済みのパッケージ一覧|