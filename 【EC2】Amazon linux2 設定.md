# Amazon linux2 
Amazon linux2 で最初にやること  
Amazon linux とは微妙に設定内容が違うため注意

### SSH ログイン
```
ssh -i "************.pem" ec2-user@IPアドレス
```

### ホスト名の設定
```
sudo hostnamectl set-hostname ホスト名
sudo reboot
```

### タイムゾーンの変更
```
timedatectl status
sudo timedatectl set-timezone Asia/Tokyo
```

### 日本語対応
```
localectl status
sudo localectl set-locale LANG=ja_JP.UTF-8
sudo localectl set-keymap jp106
```

### パッケージ更新
※ private subnet で外部通信が出来ない場合は、下の方の章を参照
```
sudo yum -y update
```

### Docker インストール
```bash
# docker インストール
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user
docker --version

# 自動起動設定
sudo systemctl enable docker

# docker-compose インストール
sudo curl -L https://github.com/docker/compose/releases/download/1.24.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
* docker-compose の最新バージョンは以下で確認  
https://github.com/docker/compose/releases

### private subnet の場合
private subnet の場合は中への通信しかできないため、yum 等が使えない。  
そのため、外部へ出るために `NAT ゲートウェイ` の設定をする必要がある。  
  
NAT ゲートウェイ を作成したら下図のように `ルートテーブル` から紐付け設定をする。  
<img width="500" alt="natgateway" src="https://user-images.githubusercontent.com/8340629/65517244-57b47280-df1d-11e9-99b9-9717bf70fbf4.png">  

### TODO
上記までの設定を `ユーザーデータ` でやりたい
