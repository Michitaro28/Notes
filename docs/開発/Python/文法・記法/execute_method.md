#　execute method

Pythonにおいて「execute メソッド」と呼ばれるものは、主に**データベースと連携する際（SQLite、MySQL、PostgreSQLなど）**に使用される、カーソル（Cursor）オブジェクトのメソッドを指します。Pythonの標準の組み込みメソッドではありませんが、データベース操作において非常に重要な役割を果たします。

## 基本的な役割
execute メソッドは、SQL文（データベースに対する命令）をデータベースエンジンに送信し、実行させるためのメソッドです。データの取得（SELECT）、追加（INSERT）、更新（UPDATE）、削除（DELETE）など、あらゆるSQL操作に使用します。

```python
import sqlite3

# 1. データベースに接続
conn = sqlite3.connect('example.db')

# 2. カーソルオブジェクトを作成
cursor = conn.cursor()

# 3. executeメソッドでSQL文を実行 (テーブル作成)
cursor.execute('CREATE TABLE IF NOT EXISTS users (id INTEGER, name TEXT)')

# 4. executeメソッドでSQL文を実行 (データ挿入)
cursor.execute("INSERT INTO users VALUES (1, '太郎')")

# 5. 変更を保存（コミット）して閉じる
conn.commit()
conn.close()
```

## プレースホルダを使った安全な実行（重要）
外部から受け取った値（ユーザーの入力値など）をSQL文に組み込む場合、文字列を直接結合してはいけません（SQLインジェクションというセキュリティの脆弱性に繋がるためです）。
代わりに、execute メソッドの第2引数にタプルや辞書を渡し、**プレースホルダ（? や %s など）**を使って値を安全に埋め込みます。

```python
import sqlite3
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

user_id = 1
# 悪い例（絶対やらない）：文字列結合
# cursor.execute("SELECT * FROM users WHERE id = " + str(user_id))

# 良い例：プレースホルダ（?）を使用
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))

# 結果を取得
result = cursor.fetchone()
print(result)

conn.close()
```


!!! note
    注意点: 変数が1つだけの場合でも、第2引数はタプルにする必要があります。そのため、(user_id,) のように末尾にカンマをつけるのを忘れないようにしてください。

## 関連メソッド
複数のデータを一度にデータベースに挿入したい場合は、`execute` メソッドを何度も呼ぶのではなく、`executemany` メソッドを使うと処理が高速になります。

```python
import sqlite3
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# 挿入したい複数のデータ（タプルのリスト）
users_data = [
    (2, '次郎'),
    (3, '花子'),
    (4, '三郎')
]

# executemanyで一括実行
cursor.executemany("INSERT INTO users VALUES (?, ?)", users_data)

conn.commit()
conn.close()
```

