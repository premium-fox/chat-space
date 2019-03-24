# サービス名

### Chatspace

# サービスの機能

- 新規登録機能（ログアウトは割愛）
- 1対1のチャット機能
- 複数人によるグループチャット機能
- チャット相手の検索機能
- グループへの招待機能
- チャットの履歴表示機能
- 画像送信機能
- チャットの自動更新（10秒に一回更新）

# データベース設計

## messagesテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|
|image|string|
|user_id|references :user|foreign_key: true|
|group_id|references :group|foreign_key: true|

### Association
- belongs_to :user
- belongs_to :group

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false,add_index :users,:name, unique: true|
|email|string|null: false,add_index :users.:email, unique: true|
|password|integer|null: false.add_index :users, :password|

### Association
- has_many :messages
- has_many :user_groups
- has_many :groups, through: :user_groups

## groupsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
- has_many :messages
- has_many :user_groups
- has_many :users, through: :user_groups

## user_groupテーブル

|Column|Type|Option|
|------|----|------|
|user_id|references :user|foreign_key: true|
|group_id|references :group|foreign_key: true|

### Association
- belongs_to :user
- belongs_to :group
