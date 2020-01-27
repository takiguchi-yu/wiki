# `React`開発のSPAテンプレート
`React`を使って`SPA`開発するためのテンプレート。

## 技術要素やサービス
* [React](https://ja.wikipedia.org/wiki/React)  
* ~~SSR(サーバーサイドレンダリング)~~  
~~本来JavaScriptで行う画面の書き換え処理などをサーバー側で実行させて、ユーザーの待機時間を短くすること。~~  
→これ、やりたかったけど今回は見送り
* S3  
静的ホスティングとして利用。ビルドした`React`を配置する。
* Amazon API Gateway  
`React`から実行。
* AWS Lambda
* [Serverless framework](https://serverless.com/)  
ローカル開発環境として使用。
* [Swagger](https://swagger.io/)  
APIのドキュメントで`API Gateway`にインポートして使用。
* [AWS CLI](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-welcome.html)

## アーキテクチャ
<img width="780" alt="スクリーンショット 2020-01-20 23 10 55" src="https://user-images.githubusercontent.com/8340629/72732903-22bde100-3bda-11ea-9f87-06a442c14e6f.png">

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
    # S3
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

## github
https://github.com/takiguchi-yu/spa-template-api

# React
```bash
# create-react-app の最新バージョンを確認
npm info create-react-app

# create-react-app をインストール
npm install -g create-react-app@3.3.0

# アプリケーション作成
create-react-app <アプリケーション名>

# アプリケーションの起動を確認
yarn start
```



## github
https://github.com/takiguchi-yu/spa-template
