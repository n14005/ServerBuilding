## 6-0 AWSコマンドラインインターフェイスのインストール

下準備
以下のコマンドを実行

    sudo -s

    export EDITOR=vi

    visudo

Default env_resetをコメントアウト 開いたファイルに以下を追加

    Defaults        env_keep="no_proxy NO_PROXY"
    Defaults        env_keep+="http_proxy https_proxy ftp_proxy"
    Defaults        env_keep+="HTPP_PROXY HTTPS_PROXY FTP_PROXY"

端末再起動。

    sudo pip install awscli

でインストール。


## 6-1 AWS EC2 + Ansible

[ここ](https://ap-northeast-1.console.aws.amazon.com/ec2/)で
左のメニューのインスタンスに行って、インスタンスの作成をする。

イメージはAmazon linuxを使って作成。

インスタンス作成時にダウンロードしたキーペアファイルに

   chmod 400 キーペアファイル.pem

をする。

#　SSH接続設定

端末で

    aws configure

アクセスキーを聞かれるので、よなしろ先生から貰ったのを入力
アクセスキーを入力した後、

　　　　region name は　ap-northeast-1　を入力

　　　　output format は　json　を入力


# SSH接続

     ssh -i キーペアファイル.pem ec2-user@パブリックIP

で接続。

# ansibleを動かす

hostsファイルを書き換える

IPアドレスをEC2インスタンスのパブリックIPに書き換える

次を追記

　　　　ansible_ssh_user=ec2-user

　　　　ansible_ssh_private_key_file=/home/shimoji/Downloads/n14005.pem

でOK。

    ansible-playbook -i hosts u.yml

でプレイブックの実行。

# AMI(Amazon Machine Image)を作る

EC2のコンソール画面に行って、自分のインスタンスを右クリック。
イメージからイメージの作成で終わり。


##6-2 AWS　EC2（AMIMOTO）

[ここ](http://ja.amimoto-ami.com/how-to-use/)見てやろう（


## 6-3 Route53


## 6-4 S3

S3にバケットを作成する

バケットをコマンドラインから作成

    aws s3 mb s3://適当なバケット名

バケットの中にファイルを転送

    aws s3 cp 任意のファイル名 s3://バケット名

##6-5 Cloud Front

AWSコンソールからCloudFrontを選ぶ

CreateDistributionを選択

WebのところのGet Startedを選択

Origin Domain Nameのところに自分のインスタンスのパブリックDNSを入力

Origin Pathは書かなくていいかも

Origin IDは自動的に入力される

後はすべてデフォルトのままで

一番したのCreateDistributionを押す。

作ったCloudFrontのDomainNameをURLに入力してつながったらOK

あとは両方のベンチーマークを取ってどっちが早いか検証する。

EC2 224

CloudFront 235


##6-6  RDS
