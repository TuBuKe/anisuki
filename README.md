# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false, unique: true|
|profile_image|text|
|points|integer|null: false|

### Association
- has_many :posts
- has_many :users_groups
- has_many :groups, through: :users_groups

## groupsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|likes|integer|null: false|
|dislikes|integer|null: false|
|anime_id|references|foreign_key: true|
|voice_actor_id|references|foreign_key: true|

### Association
- has_many :posts
- has_many :users_groups
- has_many :users, through: :users_groups
- has_many :groups_tags
- has_many :tags, through: :groups_tags
- belongs_to :voice_actor
- belongs_to :anime

## users_groupsテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :group

## postsテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|
|image|string|
|likes|integer|null: false|
|dislikes|integer|null: false|
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :group

## tagsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
- has_many :groups_tags
- has_many :groups, through: :groups_tags

## groups_tagsテーブル

|Column|Type|Options|
|------|----|-------|
|group_id|references|null: false, foreign_key: true|
|tag_id|references|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :tag

## voice_actorsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|image|string|
|birthday|date|
|likes|integer|null: false|
|dislikes|integer|null: false|

### Association
- has_many :groups
- has_many :animes_voice_actors
- has_many :animes, through: :animes_voice_actors

## animesテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|image|string|
|airing_time|date|
|likes|integer|null: false|
|dislikes|integer|null: false|

### Association
- has_many :groups
- has_many :animes_voice_actors
- has_many :voice_actors, through: :animes_voice_actors
- has_many :reviews

## animes_voice_actorsテーブル

|Column|Type|Options|
|------|----|-------|
|anime_id|references|null: false, foreign_key: true|
|voice_actor_id|references|null: false, foreign_key: true|

### Association
- belongs_to :anime
- belongs_to :voice_actor

## reviewsテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|likes|integer|null: false|
|dislikes|integer|null: false|
|anime_id|references|null: false, foreign_key: true|

### Association
- belongs_to :anime