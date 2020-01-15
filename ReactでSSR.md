# React で SSR を AWS Lambda で実行
`SSR`であればサーバ不要で動的な画面が構築できるじゃん、ということで早速構築。  
さらに`AWS Lambda`のようにサーバレスであれば、`AWS EC2`のように起動時間でお金がかかるわけでもないので、  
スタートアップでアクセスが少ないサービスであれば、とっても節約になる。

## 技術要素やサービス
* [React](https://ja.wikipedia.org/wiki/React)  
* SSR(サーバーサイドレンダリング)  
本来JavaScriptで行う画面の書き換え処理などをサーバー側で実行させて、ユーザーの待機時間を短くすること。
* Amazon API Gateway
* AWS Lambda
* [Serverless framework](https://serverless.com/)  
ローカル開発環境として使用。
* [Swagger](https://swagger.io/)  
APIのドキュメントでAPI Gatewayにインポートして使用。
* [AWS CLI](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-welcome.html)

## アーキテクチャ
<img width="650" src="https://user-images.githubusercontent.com/8340629/72343322-ed188400-3711-11ea-9a15-a0a60431a2be.png">

## AWS CLI
インストールは、[公式](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-welcome.html)を参照のこと  
Access Key と Secret を設定  
※ AWS IAM で発行
```bash
$ aws configure
AWS Access Key ID [None]: XXXXXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ
Default region name [None]: ap-northeast-1
Default output format [None]: json
```

# Serverless Framework
[SLS CLI](https://serverless.com/framework/docs/getting-started/) インストール
```bash
# serverless cli インストール
$ npm install -g serverless

# または、アップグレード
$ npm update -g serverless
```
Serverless プロジェクトを作成
```bash
# 現在のディレクトリにプロジェクトを作成
$ sls create --template aws-nodejs --name my-react-template

# ヘルプ
$ sls create --help
```
実行確認
```bash
# ローカル実行
$ sls invoke local -f hello

# ローカル実行（パラメータ渡し）
$ sls invoke local -f hello -p test.json

# ヘルプ
$ sls invoke --help
```
Lambda にデプロイ
```bash
# デプロイ
$ sls deploy -v

# 削除
$ sls remove
```

# serverless.yml
## 公式
https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/
## 編集
```yml
service: my-react-template

frameworkVersion: '>=1.0.0 <2.0.0'

provider:
  name: aws
  # Lambda の設定
  runtime: nodejs12.x
  stage: ${opt:stage, 'dev'} # Set the default stage used. Default is dev
  region: ${opt:region, 'ap-northeast-1'} # Overwrite the default region used. Default is ap-northeast-1
  memorySize: 512
  timeout: 3
  # Lambda の IAM Role
  iamRoleStatements:
    - Effect: "Allow"
      Action:
        - "s3:GetObject"
        - "dynamodb:Scan"
        - "dynamodb:Query"
      Resource: 
        - "arn:aws:s3:::*/*"
        - "arn:aws:dynamodb:*:*:table/*/index/*"
    - Effect: "Allow"
      Action:
        - "s3:ListBucket"
        - "dynamodb:Scan"
        - "dynamodb:Query"
      Resource:
        - "arn:aws:s3:::*"
        - "arn:aws:dynamodb:*:*:table/*"

# Lambda
functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: /
          method: get
          cors: true
    environment:
      NODE_ENV: ${opt:stage, 'dev'}

# CloudFormation の記法で定義
resources:
  Resources:
    S3ImageBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: s3-image-bucket-${opt:state, 'dev'}-${self:service}
  Outputs:
    ApiGatewayRestApiId:
      Value:
        Ref: ApiGatewayRestApi
      Export:
        Name: ${opt:stage, 'dev'}-ApiGatewayRestApiId

    ApiGatewayRestApiRootResourceId:
      Value:
        Fn::GetAtt:
          - ApiGatewayRestApi
          - RootResourceId
      Export:
        Name: ${opt:stage, 'dev'}-ApiGatewayRestApiRootResourceId
```
