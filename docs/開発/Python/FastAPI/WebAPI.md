# WEB API ハンズオン

## 仮想環境

- 仮想環境
    - uvでの仮想環境作成
    ```bash
    uv venv
    ```

    - 仮想環境をactiveにする
    ```
    source .venv/bin/activate
    ```

- ライブラリの準備

```
uv pip install requests
```

!!! note "requestsライブラリとは？"
    requestsライブラリは、Pythonで最も広く使われているHTTPクライアントライブラリです。
    
    主な特徴:
    
    - 簡潔なAPI: HTTP リクエスト(GET, POST, PUT, DELETE等)を簡単に送信できる
    - 自動処理: JSON のエンコード/デコード、セッション管理、Cookie処理などを自動化
    - 人間向け設計: 標準ライブラリの urllib よりも直感的で読みやすいコード

    **使用例**
    
    ```python
    import requests

    # GETリクエスト
    response = requests.get('https://api.example.com/data')
    print(response.json())  # JSON レスポンスを自動パース

    # POSTリクエスト
    response = requests.post('https://api.example.com/users', 
                            json={'name': 'John', 'age': 30})

    # ステータスコード確認
    if response.status_code == 200:
        print('成功')
    ```
    
    主な用途:

    - 外部APIの呼び出し
    - Webスクレイピング
    - マイクロサービス間の通信
    - データの取得・送信
    
    FastAPIアプリケーションでは、他のAPIと連携する際や、テストコードでエンドポイントを呼び出す際によく使用されます。

## main.pyへの記述

```python
import requests # HTTP リクエストを送信するためのライブラリ
import json # JSON データを扱うためのライブラリ

# 郵便番号APIのURLを指定
# 郵便番号「7830060」で検索する場合
# url = "https://zipcloud.ibsnet.co.jp/api/search?zipcode=7830060"

# APIを変数に格納する
url = "https://zipcloud.ibsnet.co.jp/api/search"

# ユーザーから郵便番号を入力してもらう
zipcode_input = input("郵便番号を入力=>")


# APIに送るパラメータを準備
# ユーザーが入力した郵便番ををパラメータに設定
param =  {"zipcode": zipcode_input}


# requests.get()関数を使用して、APIにGETリクエストを送り、resに格納される
# requests.get()の第2引数は位置引数ではなく、params=というキーワード引数で渡す必要があります。これがないとSyntaxErrorまたは実行時エラーが発生します。
res = requests.get(url, params=param, timeout=10)

# res.textに格納されているJson形式のレスポンスデータをPythonの辞書型に変換
data = json.loads(res.text)

# 変換したデータを出力
print(data)

# 見やすくするために区切りをつける
print('*' * 50)

# レスポンスデータから必要な情報を抽出
if data['results'] is not None:
    # resultsリストの最初の要素から住所情報を取得
    address_info = data['results'][0]

    # 郵便番
    zipcode = address_info['zipcode']

    # 住所を組み立て
    address =  f"{address_info['address1']} {address_info['address2']} {address_info['address3']}"

    # 整形して出力
    print(f"郵便番号: {zipcode} 住所: {address}")

else:
    print("該当する住所が見つかりませんでした。")
```

