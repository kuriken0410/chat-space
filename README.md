# グループチャットアプリchat-space
## :globe_with_meridians: chat-spaceとは
- chat-spaceはグループチャットアプリです。
- 画像とテキストの投稿ができます。
- グループに登録したメンバーのみがチャットを閲覧できます。

![ChatSpace](https://gyazo.com/725d93c9a09f600d3b73124824b88470.png)

## :globe_with_meridians: 使い方
初めにユーザー登録をしてください。
![ChatSpace - Gyazo](https://gyazo.com/f539e78bed2a165f5136f8b5d09d7e26.png)

次に、チャットグループを作成してください。
![キャプチャ動画](https://gyazo.com/13d7536c2c4f033ee000178eb0546de9.gif)

既存のメンバーの名前がわかれば、そのメンバーを検索できます。
グループにメンバーを追加すると、そのメンバーと自分だけがチャットを閲覧できます。
![キャプチャ動画](https://gyazo.com/1d8516a99f4472ba895be17b7959482a.gif)

画像またはテキストを投稿できます。
![キャプチャ動画](https://gyazo.com/a5642f9659736c81588b072d9b9372a9.gif)

グループメンバーのチャットは自動的に同期されます。
![キャプチャ動画](https://gyazo.com/68d10bbaece880b07dd3e5e8fe990ecb.gif)

## :globe_with_meridians: 使用した技術、言語、ツールなど
<a><img src="https://user-images.githubusercontent.com/39142850/71774533-1ddf1780-2fb4-11ea-8560-753bed352838.png" width="70px;" /></a> <!-- rubyのロゴ -->
<a><img src="https://user-images.githubusercontent.com/39142850/71774548-731b2900-2fb4-11ea-99ba-565546c5acb4.png" height="60px;" /></a> <!-- RubyOnRailsのロゴ -->
<a><img src="https://user-images.githubusercontent.com/39142850/71774618-b32edb80-2fb5-11ea-9050-d5929a49e9a5.png" height="60px;" /></a> <!-- Hamlのロゴ -->
<a><<img src="https://user-images.githubusercontent.com/39142850/71774644-115bbe80-2fb6-11ea-822c-568eabde5228.png" height="60px" /></a> <!-- Scssのロゴ -->
<a><img src="https://user-images.githubusercontent.com/39142850/71774768-d064a980-2fb7-11ea-88ad-4562c59470ae.png" height="65px;" /></a> <!-- jQueryのロゴ -->
<a><img src="https://user-images.githubusercontent.com/39142850/71774786-37825e00-2fb8-11ea-8b90-bd652a58f1ad.png" height="60px;" /></a> <!-- AWSのロゴ -->
- 言語
    - サーバーサイド: Ruby
    - フロント: SASS, HTML (HAML), JavaScript (jQuery)
- アプリケーションフレームワーク: Ruby on rails
- インフラ: AWS(EC2, S3)
- ソースコード管理: Github
- 自動デプロイツール: capistrano
- webサーバー: nginx
- アプリケーションサーバー: unicorn
- データベース: MySQL

## :globe_with_meridians: 実装内容
- HAMLとSASSでのフロント実装
- jQueryによるメッセージの非同期通信
- jQueryによるインクリメンタルサーチ機能
- devise (認証用gem)によるユーザー登録・ログイン機能
- carrierwaveによる画像のアップロード
- fogによるAWS S3への画像のアップロード
- capistranoによる自動デプロイ

## :globe_with_meridians: インストール方法
1.このリポジトリを複製<br>
`$ git clone https://github.com/kuriken0410/chat-space`

2.インストールしたリポジトリに移動<br>
`$ cd chat-space.git`

3.gemをアプリケーションに適用<br>
`$ bundle install`<br>

4.DBの作成&反映<br>
`$ rails db:create`<br>
`$ rails db:migrate`<br>

5.カテゴリ一覧の反映<br>
`$ rails db:seed`<br>

6.アプリケーションの起動<br>
`$ rails s`<br>
:point_right:`http://localhost:3000`

# :page_facing_up: DB設計

## :globe_with_meridians: chatspaceのデータベース設計
### messagesテーブル
|Column|Type|Options|
|------|----|-------|
|body|text||
|images|text||
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

#### Association
- belongs_to :group
- belongs_to :user

### usersテーブル
|Column|Type|Options|
|------|----|-------|
|email|string|null: false|
|password|string|null: false|
|name|string|null: false|

#### Association
- has_many :messages
- has_many :groups_users
- has_many :groups, through: :groups_users

### groupsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

#### Association
- has_many :messages
- has_many :groups_users
- has_many :users, through: :groups_users

### groups_usersテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

#### Association
- belongs_to :group
- belongs_to :user
