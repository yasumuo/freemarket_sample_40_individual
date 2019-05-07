# DB設計

## テーブルの種類
* usersテーブル
* creditsテーブル
* itemsテーブル
* categoriesテーブル
* category_itemsテーブル
* commentsテーブル
* dealsテーブル


## usersテーブル

|Column|Type|Options|
|------|----|-------|
|nick_name|string|index: true, null: false|
|email|string|null: false, unique: true|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|auth_number|int|null: true|
|birthday|datetime|null: false|
|tel|string|null: true|
|sippings_name|string|null: true|
|sippings_name_kana|string|null: true|
|zip|string|null: true|
|prefecture|int|null: true|
|city|string|null: true|
|address|string|null: true|
|building|string|null: true|
|sippings_tel|string|null: true|
|profiles_name|string|null: true|
|profiles_intro|text|null: true|
|good|int|null: true|
|normal|int|null: true|
|bad|text|null: true|

### Association
- has_many :deals
- has_many :items
- has_many :comments
- has_one :credit

## creditsテーブル

|Column|Type|Options|
|------|----|-------|
|number|int|null: false|
|expiration|date|null: false|
|code|int|null: false|
|user_id|references||

### Association
- belongs_to :user

## commentsテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|user_id|references||
|item_id|references||

### Association
- belongs_to :user
- belongs_to :item
- validates :body, presence :true

## dealsテーブル

|Column|Type|Options|
|------|----|-------|
|status|text|null: false|
|item_id|references||
|buyer_id|references||
|exhibitor_id|references||

### Association
- belongs_to :user
- belongs_to :item


## itemsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|description|text|null: false|
|brand|string||
|status|int|null: false|
|price|int|null: false|
|likes_count|int||
|shipping_charge||null: false|
|region|string|null: false|
|deliver_days|int|null: false|
|user_id|references||

### Association
- has_one :deal
- belongs_to :user
- has_many :categories, through: category_items
- has_many :category_items

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|parent_id|references||

### Association
- belongs_to :parent, class_name: :Category
- has_many :children, class_name: :Category, foreign_key: :parent_id
- has_many :items, through: category_items
- has_many :category_items

## category_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|integer|null: false, foreign_key: true|
|category_id|integer|null: false, foreign_key: ture|

### Association
- belongs_to :item
- belongs_to :category
