# jawsug-niigata-amazon-bedrock-handson

2023/11/18 (土)
JAWS-UG新潟支部 ハンズオン教材

## 準備 & 利用方法

以下の環境で動作可能です。

- SageMaker Studio
- SageMaker Studio Lab
- Google Colaboratory

### Bedrock 基幹モデル利用申請

- 本ハンズオン資料はオレゴンリージョン (us-west-2) で動作確認しています。
- オレゴンリージョンにて、Bedrock基幹モデルの利用申請をしてください。
    - 参考: [Amazon Bedrock をマネジメントコンソールからちょっと触ってみたいときは Base Models（基盤モデル）へのアクセスを設定しましょう | DevelopersIO](https://dev.classmethod.jp/articles/if-you-want-to-try-out-amazon-bedrock-from-the-management-console-you-can-set-up-access-to-base-models/)

### SageMaker Studio

1. SageMaker Studioを立ち上げる
2. 実行ロールを確認する
3. 対象の実行ロールに対して、以下のBedrockのアクション許可権限を付与する
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "BedrockFullAccess",
                "Effect": "Allow",
                "Action": [
                    "bedrock:*"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
4. ノートブックをSageMaker Studioで開いて実行

### SageMaker Studio Lab

1. IAMユーザを作成し、APIキーを取得する
2. IAMユーザに以下のBedrockのアクション許可権限を付与する
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "BedrockFullAccess",
                "Effect": "Allow",
                "Action": [
                    "bedrock:*"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
3. SageMaker Studio Labを立ち上げる
4. ターミナルを起動する
5. AWS CLIにて認証情報を登録する
    - 1で取得したAPIキーを設定する
6. ノートブックをSageMaker Studio Labで開いて実行

### Google Colaboratory

1. IAMユーザを作成し、APIキーを取得する
2. IAMユーザに以下のBedrockのアクション許可権限を付与する
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "BedrockFullAccess",
                "Effect": "Allow",
                "Action": [
                    "bedrock:*"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
3. `amazon_bedrock_api_key.env` ファイルを作成し、以下の内容を設定する
    - `=` の右辺側の文字列を実際のAPIキーに書き換えてください。
    ```bash
    AWS_ACCESS_KEY_ID=<AWSアクセスキー>
    AWS_SECRET_ACCESS_KEY=<AWSシークレットアクセスキー>
    ```
4. Googleドライブのマイドライブ直下に、 `amazon_bedrock_api_key.env` をアップロードする
5. ノートブックをGoogle Colaboratoryで開く
6. Google Colaboratory上で、Googleドライブをマウントする
7. 各ノートブックの冒頭にて、`python-dotenv` をインストールする
    `!pip install python-dotenv`
8. `python-dotenv` インストール後に追加セルで以下のコードを実行し、環境変数を読み込む
    ```python
    import dotenv
    dotenv.load_dotenv('./drive/MyDrive/amazon_bedrock_api_key.env')
    ```
9. 以降、ノートブックを実行する

## Clean up

### SageMaker Studio

必要な方は、以下のページを参考にリソース削除してください。

[リソース削除](./doc/cleaning.md)

### SageMaker Studio Lab

必要な方は、ターミナルからAWSの認証情報が格納されているフォルダ ( `~/.aws/`) を削除してください。

### Google Colaboratory

必要な方は、Googleドライブに格納されたAWSのAPIキーのファイル ( `amazon_bedrock_api_key.env` ) を削除してください。
