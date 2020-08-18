# Slack bot をローカル開発

## 技術
- MacOS(Mojave)
- Slack Bolt
- node
- https://github.com/seratch/bolt-starter を参考にしています。

## ngrok
`ngrok` は localhost を外部公開することができる素晴らしいサービスです。

https://ngrok.com/
```bash
# http://localhost:3000 を外部公開
$ ./ngrok http 3000

ngrok by @inconshreveable                                                         (Ctrl+C to quit)
                                                                                                  
Session Status                online                                                              
Account                       Slack (Plan: Free)                               
Version                       2.3.35                                                              
Region                        United States (us)                                                  
Web Interface                 http://127.0.0.1:4040                                               
Forwarding                    http://abcabcabcabc.ngrok.io -> http://localhost:3000               
Forwarding                    https://abcabcabcabc.ngrok.io -> http://localhost:3000              
                                                                                                  
Connections                   ttl     opn     rt1     rt5     p50     p90                         
                              0       0       0.00    0.00    0.00    0.00 
```

## node
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
 
# 上記で表示されたコマンド実行
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

# bolt-starter
Slack Bolt を使います。
```bash
$ git clone https://github.com/seratch/bolt-starter.git

$ cd bolt-starter
$ cp _env .env

# edit .env
$ npm i
$ npm run local
```

## リクエストURL
Set https://{your-awesome-subdomain}.ngrok.io/slack/events to all of the followings:


https://abcabcabcabc.ngrok.io/slack/events

- https://api.slack.com/apps/{APP_ID}/slash-commands
- https://api.slack.com/apps/{APP_ID}/event-subscriptions
- https://api.slack.com/apps/{APP_ID}/interactive-messages