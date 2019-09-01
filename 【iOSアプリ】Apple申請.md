# 【iOSアプリ】Apple申請

## Apple Developer Program への登録
1. 以下にアクセスし、Apple ID でログインする  
https://appstoreconnect.apple.com/
1. ログイン後、「App」をクリック  
<img width="500" alt="itunesconnect_top" src="https://user-images.githubusercontent.com/8340629/63302452-0ad6ee00-c318-11e9-84db-8881646b7102.png">
1. 「今すぐ始める」をクリックし、手順に従い、登録を進める 
<img width="500" alt="itunes_top" src="https://user-images.githubusercontent.com/8340629/63302796-03641480-c319-11e9-9a73-668a77b97b72.png">
1. 登録後、Appleの承認が完了するまで２日以上かかることもあるが、気長に待つ  
(今回は土日挟んで5日目に申請が承認された)

## AppStore Connect への登録
### 証明書の取得
1. キーチェーンアクセスを使って、証明書を発行する  
<img width="500" alt="スクリーンショット 2019-09-01 21 53 49" src="https://user-images.githubusercontent.com/8340629/64076724-4fdd2600-cd03-11e9-9893-551638c7ef13.png">  
<img width="500" alt="Certificates_4" src="https://user-images.githubusercontent.com/8340629/64076723-4fdd2600-cd03-11e9-8e09-b5b727619fc0.png">
1. 以下にアクセスし「Account」をクリック  
https://developer.apple.com/jp/programs/  
<img width="500" alt="developerapple_top" src="https://user-images.githubusercontent.com/8340629/63356011-0c4cf880-c3a2-11e9-846a-e8a615da94d0.png">
1. 「Certificates, Identifiers & Profiles」をクリック  
<img width="500" alt="Certificates_2" src="https://user-images.githubusercontent.com/8340629/64076636-2e2f6f00-cd02-11e9-875d-0d572dcb859c.png">
1. 「Certificates」を選択し、「＋」をクリック  
<img width="500" alt="Certificates_1" src="https://user-images.githubusercontent.com/8340629/64076619-02ac8480-cd02-11e9-8ce1-103d73c3ea54.png">
1. 「iOS App Development」を選択し、「Continue」をクリック  
<img width="500" alt="Certificates_3" src="https://user-images.githubusercontent.com/8340629/64076750-a5193780-cd03-11e9-9f6a-6c5bba3ceacd.png">
1. さきほど作成した証明書をアップロードし、「Continue」をクリック
1. 「Download」をクリック、証明書をダウンロードする
証明書をMacにダウンロードし、.cerファイルをダブルクリックしてKeychain Accessにインストールする。  
秘密鍵と公開鍵のバックアップコピーを安全な場所に保存すること。

### App ID を作成
アプリの Bundle ID に紐づく App ID を作成する  
すでにアプリを実機で動作させている場合は自動的に作成されているため、 App ID の作成は不要  
1. Identifiers を選択し、「＋」をクリック  
<img width="500" alt="Certificates_5" src="https://user-images.githubusercontent.com/8340629/64076896-9c296580-cd05-11e9-88c7-240e14508a61.png">
1. 「App IDs」を選択し、「Continue」をクリック
1. 「Description」には任意の説明文を入力し、「Bundle ID」に作成した iOS アプリの Bundle ID を入力する  
入力したら「Continue」をクリック  
<img width="500" alt="Certificates_6" src="https://user-images.githubusercontent.com/8340629/64076949-4903e280-cd06-11e9-835f-b3c3b4797fcf.png">
1. 内容を確認し、「Register」をクリック  

### 「マイ App」を登録 
1. 以下にアクセス
https://appstoreconnect.apple.com/
1. 「マイ App」をクリック
1. 左上の「＋」をクリックしたら手順に従い、自分が作成した iOS アプリを登録する


