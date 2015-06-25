# 3-0 Ansibleのインストール

リポジトリ追加してインストール

    sudo apt-get install software-properties-common
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install ansible

# 3-1 ansibleでWordpressを動かす(2)を行なう

sshpassインストール

    sudo apt-get install sshpass

疎通確認

    ansible 192.168.56.193 -i hosts -m ping --private-key ~/.vagrant.d/insecure_private_key -u vagrant -k

# proxyの設定と何かダウンロード

    vagrant plugin install vagrant-proxyconf
    vagrant plugin install vagrant-vbguest

Vagrantfileにproxy設定を書く

    if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://172.16.40.1:8888/"
    config.proxy.https    = "http://172.16.40.1:8888/"
    config.proxy.no_proxy = "localhost,127.0.0.1,.it-college.local"
    end

# playbookを実行

    ansible-playbook -i hosts playbookファイル名 -u vagrant -k 

ymlファイルをコピってくだたい
