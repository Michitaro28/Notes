# uv
uvはPythonのパッケージ管理ツールで、pipやpoetryと同じように使える。Rustで作れられているためとても早い。

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