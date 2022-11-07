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


dockerを使用してrailsを立ち上げる。
Dockerfile, Gemfile, Gemfile.lock, docker-compose.ymlを作る
イメージをビルドし, コンテナを作り, Rails newする
Gemfileが更新されるのでイメージを作り直す
database.ymlを変更してコンテナを起動する


gemfile

source 'https://rubygems.org'
gem 'rails', '7.0.4'

docker-compose.yml

version: '3'
services:
  db:
    image: postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
  web:
    build: .
    command: bundle exec rails s -p 3000 -b '0.0.0.0'
    volumes:
      - .:/rails-mailer
    ports:
      - "3000:3000"
    depends_on:
      - db



ターミナルで
docker-compose run web rails new . --force --database=postgresql

docker-compose build

docker-compose up

docker-compose run web rake db:create