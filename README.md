<!-- omit in toc -->
Vagrant DynamoDB local With DynamoDB-Admin
==========
[![MIT licensed][shield-license]][mit]

自分用の検証ツールです。  
`vagrant up`コマンド一発で`DynamoDB local`とと`DynamoDB-Admin`を用意できるようにしたものです。  
全て`docker`で実行しています。  


<!-- omit in toc -->
目次
-----------------
<details>
<summary>show</summary>

- [作業環境](#作業環境)
- [ツールのバージョン](#ツールのバージョン)
- [使い方](#使い方)
  - [実行](#実行)
  - [設定ファイルの変更](#設定ファイルの変更)
- [バージョニング](#バージョニング)
- [ライセンス & 作者](#ライセンス--作者)
</details>


作業環境
------------
- Windows 10 64bit
- VirtualBox 7.0.4
- Vagrant 2.3.4


ツールのバージョン
------------
- ubuntu/jammy64 20221219.0.0
- docker-compose 3.7
- [amazon/dynamodb-local](https://hub.docker.com/r/amazon/dynamodb-local) 1.20.0
- [aaronshaf/dynamodb-admin](https://hub.docker.com/r/aaronshaf/dynamodb-admin/) 4.4.1


使い方
-----
### 実行
ポートフォワーディングするなら下記コマンドを実行する。
```pwsh
vagrant up forward-port
```
- dynamodb-local
  - `http://localhost:50000`
- dynamodb-admin
  - `http://localhost:50001`

固定IPにするなら下記コマンドを実行する。
```pwsh
vagrant up private-net
```
- dynamodb-local
  - `http://192.168.33.11:8000`
- dynamodb-admin
  - `http://192.168.33.11:8001`

### 設定ファイルの変更
下記のenvファイルから環境変数を変更できる
- [バージョン等の設定](./docker/.env)
- [dynamodb-localの設定](./docker/.env.dynamodb-local)
- [dynamodb-adminの設定](./docker/.env.dynamodb-admin)


バージョニング
-----
[SemVer][semver]のガイドラインに則ってバージョン管理しています。  
リリースは以下の形式で行われます。
```
<major>.<minor>.<patch>
```
- 大きな変更や後方互換性のない場合は `<major>` (`<minor>` と `<patch>` もリセット) を上げます。
- 後方互換性があり機能性を追加した場合は `<minor>` (`<patch>` もリセット) を上げます。
- 後方互換性を伴うバグ修正をした場合 `<patch>` を上げます。


ライセンス & 作者
-------
[![MIT licensed][shield-license]](LICENSE)  
Copyright &copy; 2022, ClaudiaHeart



[shield-license]: https://img.shields.io/badge/license-MIT-blue.svg
[mit]: https://licenses.opensource.jp/MIT/MIT.html
[semver]: https://semver.org/lang/ja/