# GraphQL 入門
GraphQL(グラフ・キューエル)は必要なデータだけを取得することができるインターフェース。

RESTと対になる。

RESTをマクドナルドだとするとGraphQLはサブウェイ。

RESTと違って`エンドポイントは一つ`のみ。

JSONに取得したいプロパティを指定してデータを取得する。

HTTPメソッドは`POST`。

必要なデータのみをやりとりできるため狭い帯域でも高速にレスポンスできる。

## GraphiQL
グラフィクルと読む。

GraphQLのI/Fを確認するための PlayGround。

https://developer.github.com/v4/explorer/

Chrome等ブラウザの開発者ツールで実際のリクエストを確認することができる。

## クエリ(query)、フィールド(Fields)、型(Types)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## 引数(Arguments)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## エイリアス(Aliases)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## フラグメント(Fragments)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## 操作名(Operation Name)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## 変数(Variables)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## ミューテーション(Mutations)
リソースの情報自体を書き換えることができる。  
queryがGETなのに対してPUTやDELETEのようなもの。

リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## インラインフラグメント(Inline Fragments)と型名(__typename)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## 型システム(Type System)、スカラー型(Scalar Types)、オブジェクト型(Object Types)、スキーマ(Schemas)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
## ページネーション(pagination)
リクエスト
```json
{
  "hoge"
}
```
レスポンス
```json
{
  "hoge"
}
```
