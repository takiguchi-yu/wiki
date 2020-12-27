# Firebase RTDB 設定内容

https://firebase.google.com/

```js
const firebaseConfig = {
  apiKey: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  authDomain: "アプリ名.firebaseapp.com",
  projectId: "アプリ名",
  storageBucket: "アプリ名.appspot.com",
  messagingSenderId: "999999999999",
  appId: "1:999999999999:web:XXXXXXXXXXXXXXXXXXXXXX",
  databaseURL: "https://アプリ名-default-rtdb.firebaseio.com/"
};
```

# Yarn インストール

https://classic.yarnpkg.com/en/docs/install/

# React App をビルドする

```bash
$ yarn build
# build が生成されます
$ tree build
# ビルドされたものをサーバーとして実行することもできます
$ cd build
$ npx http-server
```

# Firebase Hosting

Firebase Hosting するためのメモ

```bash
# Firebase CLI をインストール
$ yarn add firebase-tools --dev
# バージョン確認(プロジェクトにしかインストールしていないため npx を付ける必要があることに注意)
$ npx firebase -V
# Google へログイン
$ npx firebase login
# プロジェクト開始
$ npx firebase init

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  /Users/takiguchi-yu/firebase/react-chat-app

? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, th
en Enter to confirm your choices. Hosting: Configure and deploy Firebase Hosting sites

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

? Please select an option: Use an existing project
? Select a default Firebase project for this directory: chatapptk (chatAppTk)
i  Using project chatapptk (chatAppTk)

=== Hosting Setup

Your public directory is the folder (relative to your project directory) that
will contain Hosting assets to be uploaded with firebase deploy. If you
have a build process for your assets, use your build's output directory.

? What do you want to use as your public directory? build
? Configure as a single-page app (rewrite all urls to /index.html)? Yes
? Set up automatic builds and deploys with GitHub? No
? File build/index.html already exists. Overwrite? No
i  Skipping write of build/index.html

i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...

✔  Firebase initialization complete!

$ npx firebase deploy
```

# デプロイをタスク化

```bash
# packege.json
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject",
  "deploy": "yarn run build && firebase deploy" ←追加
},

