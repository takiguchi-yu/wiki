# node.js インストール
```bash
# nodebrew インストール
$ brew install nodebrew
$ nodebrew setup
Fetching nodebrew...
Installed nodebrew in $HOME/.nodebrew
 
========================================
Export a path to nodebrew:
 
export PATH=$HOME/.nodebrew/current/bin:$PATH
========================================
 
# 上記で setup したときに表示されたコマンドを .bash_profile に追記
$ echo "export PATH=\$HOME/.nodebrew/current/bin:\$PATH" >> ~/.bash_profile
$ source ~/.bash_profile
 
# インストールしたいバージョンを下記から選択
$ nodebrew ls-remote
 
# node.js インストール
$ nodebrew install-binary v10.15.3
 
# インストール内容確認
$ nodebrew list
v10.15.3
 
current: none
 
# インストールしたバージョンを使用可能にする
$ nodebrew use v10.15.3
 
# 使用可能になったか確認（current のところ）
$ nodebrew list
v10.15.3
 
current: v10.15.3
 
# バージョン確認
$ node -v
$ npm -v
```

# Serverless Framework 
## Serverless Framework インストール
```Bash
$ npm install serverless -g
$ sls -v
1.42.3
 
# アップデートする場合
$ npm update -g serverless
```
## Serverless サービス作成
以下の手順で Serverless サービスのテンプレートを作成できる。
```bash
$ serverless create --template aws-nodejs --path sls-sample
 
# 使用可能なテンプレートは以下で確認
$ sls create --help
```
### ヘルプ
```
--template or -t 利用可能なテンプレートの1つの名前。

--template-urlと--template-pathが存在しない場合は必須です。

--template-url or -u 利用可能なテンプレートの1つの名前。

--templateと--template-pathが存在しない場合は必須です。 

--template-path テンプレートのローカルパス--templateと--template-urlが存在しない場合は必須です。 

--path or -p サービスを作成する場所のパス。 

--name or -n serverless.yml内のサービスの名前。
```

## Serverless デプロイ
AWS にローカルのソースコードをアップロードできる。
```bash
$ cd sls-sample
 
# credentialsを設定
# https://serverless.com/framework/docs/providers/aws/guide/credentials#quick-setup
$ export AWS_ACCESS_KEY_ID=<your-key-here>
$ export AWS_SECRET_ACCESS_KEY=<your-secret-key-here>
 
$ sls deploy -v
デプロイした Lambda Function 実行
$ sls invoke -f hello
```
### ヘルプ
```
$ sls invoke --help

Plugin: Invoke
invoke ........................ Invoke a deployed function
invoke local .................. Invoke function locally
    --function / -f (required) ......... The function name
    --stage / -s ....................... Stage of the service
    --region / -r ...................... Region of the service
    --path / -p ........................ Path to JSON or YAML file holding input data
    --type / -t ........................ Type of invocation
    --log / -l ......................... Trigger logging data output
    --data / -d ........................ Input data
    --raw .............................. Flag to pass input data as a raw string
```

## serverless.yml
設定ファイルについては以下を参照。 

https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/

## Severless サービス削除
```bash
$ sls remove -v
```

# ローカル開発環境を整える
## 初期設定
```bash
$ npm install serverless -g
$ npm install # package.json をもとに依存関係をインストール
以下はただのインストールメモ
$ npm install serverless -g
$ npm install eslint --save-dev
$ npm install aws-sdk --save
$ npm install serverless-dynamodb-local --save-dev
```
## 実行方法
```bash
$ sls invoke local -f { function name }
 
# sample
sls invoke local -f hello -p testdata/test001.json
https://serverless.com/framework/docs/providers/aws/cli-reference/invoke-local/
```