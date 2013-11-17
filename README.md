packer_ubuntu
=============

packer
-------------
http://dev.classmethod.jp/cloud/aws/create_amazon-ami_by_packer/

> 一つの設定ファイルから複数の環境に同時にマシンイメージを作成する
複数環境ではなくAWS EC2/AMIを管理するケースでも、AMIを自動作成し、その構成内容をコード(設定ファイル)で管理できるというEC2/AMIの新しい管理手法として非常に有用
AMIは他人が作ったものはもとより、開発者が自分で作ったものであっても、作成したあとからAMIの内容を正確に把握することが難しいブラックボックスになりがち
Packerを使用すれば、設定ファイル(後述のTemplate)をGitなどのVCSで管理することで、AMIの構成をコードで管理することが可能

準備するもの
-------------
- AWSのアクセスキーとシークレットキー
AWSのコンソール画面のアカウント
My Account
セキュリティ証明書
アクセスキー

- AMI ID
AWSのコンソール画面より、選択可能なAMI IDを確認する
https://console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchInstanceWizard:

ex.)
`Ubuntu Server 13.10 - ami-b945ddb8 (64-bit) / ami-ad45ddac (32-bit)`


template 作り
==============
アクセスキーを外だしする
--------------
http://dev.classmethod.jp/cloud/packer-tips-for-ci-tools/
アクセスキーとシークレットキーは環境変数として外だしすべき

    
    time packer build -var 'aws_access_key=...' -var 'aws_secret_key=...' ubuntu-key-valiables.json
    


chef-soloでプロビジョニング
-------------
http://dev.classmethod.jp/cloud/use_chef-solo-provisioner_to_make_ami_by_packer/


    
    time packer build -var 'aws_access_key=...' -var 'aws_secret_key=...' ubuntu-chef-solo.json
    

