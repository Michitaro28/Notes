# FastAPI

## FastAPIのインストール
```
uv pip install fastapi
```

## 必要なライブラリのインストール
- uvicorn
```
uv pip install uvicorn
```

Uvicornは、Python用の非常に高速なASGIサーバーです。ASGI（Asynchronous Server Gateway Interface）は、非同期プログラミングをサポートするために設計されたPythonの標準インターフェイスで、WEBアプリケーションとサーバー間の通信を仲介します。UvicornはFastAPIの「エンジン」です。

## サンプルコード

main.py
```python

from fastapi import FastAPI

# FastAPIのインスタンスを作成
app = FastAPI()

# GETかつエンドポイント「’/’」で呼ばれる関数
@app.get("/")
async def get_hello():
    return {"message": "Hello, YELL for ALL!"}
```

## 実行
このファイルのあるディレクトリに移動し、下記のコマンド

```bash
uv run uvicorn main:app --reload
```

8000番以外を指定する際は、末尾にオプションをつける
```bash
uv run uvicorn main:app --reload --port 8001
```

## デコレータについて

|部分|説明|
| :-- | :-- |
| @app | FastAPIのインスタンスを表し、このインスタンスに対して、WEBアプリケーションの設定やルーティング（特定のアドレスにアクセスがあった時の動作）を行う|
| get | HTTPのGETメソッドを使用して、特定のエンドポイントに対するリクエストを処理します|
| "/"| ここはエンドポイントのアドレスを示します|


## SwaggerUIによるドキュメント生成

ブラウザの起動後、表示されているURLの後ろに「/docs」をつけて、実行
また「/redoc」もある。


