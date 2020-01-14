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

## アーキテクチャ
<img width="650" alt="スクリーンショット 2020-01-14 21 07 42" src="https://user-images.githubusercontent.com/8340629/72343322-ed188400-3711-11ea-9a15-a0a60431a2be.png">

## Serverless framework
```bash
# https://serverless.com/framework/docs/getting-started/
# serverless cli インストール
npm install -g serverless

# または、アップグレード
npm update -g serverless

```
## Swagger

## API Gateway

## Lambda にデプロイ

## 実行確認

