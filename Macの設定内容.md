## ll コマンドを使えるようにする
```bash
vi ~/.bash_profile

----(.bash_profile)----
alias ll='ls -1G'
```
```bash
source ~/.bash_profile
```

## ターミナルを短縮
```bash
vi ~/.bash_profile

----(.bash_profile)----
PS1="[mac:\W]$ "
```
```bash
source ~/.bash_profile
```

## ssh ログイン毎にターミナルの色を変更
```bash
vi ~/.ssh/ssh-settings

----(ssh-settings)----
#!bin/zsh

set_profile() {
  local profile=$1
  /usr/bin/osascript <<EOF
tell application "Terminal" to set current setting of first window to settings set "$profile"
EOF
}

if [[ "$@" =~ "^dev*" ]]; then
  set_profile "Grass"
elif [[ "$@" =~ "^test*" ]]; then
  set_profile "Ocean"
elif [[ "$@" =~ "^aws*" ]]; then
  set_profile "AwsConsoleTest"
else
  set_profile "Red Sands"
fi

ssh $@

set_profile "Pro"
```
```bash
vi ~/.bash_profile

----(.bash_profile)----
alias ssh='~/.ssh/ssh-settings'
```
```bash
chmod 755 ~/.ssh/ssh-settings
source ~/.bash_profile
```
## SSH のパスフレーズをキーチェーンに保存
```bash
vi ~/.ssh/config

----(config)----
Host *
  AddKeysToAgent yes
  UseKeychain yes
```

## homebrew インストール
公式 https://brew.sh/index_ja.html
```bash
# インストール
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 確認
brew -v 

# 更新
brew update

# formula を再ビルド
brew upgrade

# インストール済みの formula の確認
brew list

# インストール方法
brew install {formula}

# アンインストール方法
brew uninstall {formula}

# 不要な formula の削除
brew cleanup

# formula の情報を見る
brew info {formula}
```

## 複数サーバに一括ログインするツール
```bash
brew install csshx

# 使い方
csshx --login {ログインユーザー} {接続先} {接続先} {接続先} ..
```

## OpenSSH の警告メッセージを出さないようにする
```bash
vi ~/.ssh/config

----(config)----
Host *
  StrictHostKeyChecking no
```

## ssh をタイムアウトしないようにする
```bash
vi ~/.ssh/config

----(config)----
Host *
  ServerAliveInterval 60
```

## ssh の config サンプル
```bash
vi ~/.ssh/config

----(config)----
Host dev
  HostName 127.0.0.1
  User vagrant
  Port 2200
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes
  LogLevel FATAL
```
