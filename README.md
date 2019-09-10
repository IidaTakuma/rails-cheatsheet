## ゴール

Rails 6.0.0をデータベースをPostgresqlを設定し、Yay! You’re on Rails! するところまで

## 前提

ローカル環境で
`$ rbenv -v`

`$ node -v`

`$ Yarn --v`

`$ psql --version`

`$ bundle -v`

が実行できる。

## 環境構築
`$ mkdir [proj-name]`

`$ cd [proj-name]`

`$ bundler init`

生成されたGemFileのrailsのコメントアウトを外す。

`$ bundle exec rails -v` 

- プロジェクト環境のrailsのバージョンを確認する。

`$ bundle --path vendor/bundle -j4` 

- 「--path vendor/bundle」を指定することで、railsアプリのルート下のvendor/bundleにインストールされ、そのアプリケーションの中だけにインストールされる。一度上のコマンドを実行すれば、Bundlerはインストール先を記憶するので次回以降は`bundle install`を実行するだけでよい。
- 「-j4」bundlerを並列処理できる「--jobs=4」

`$ bundle exec rails new . -d postgresql -Tr` 

- 「bundle exec」システム共通ではなくプロジェクト毎のgemを使用する。
- 「rails new .」で現在のディレクトリをアプリケーション名にrails newする。
- 「-d postgresql」データベースにPostgresqlを使用することを指定。
- 「-Tr」「--skip-test」Miniテストを生成しないようにする。

proj-name / docker-compose.ymlに以下を記入
```
version: '3.7'
services:
  postgres:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
    hostname: postgres
    ports:
      - 5432:5432
```

` $ docker-compose build`

` $docker-compose up`

` $ bin/rails db:create`

` $ bin/rails server`

参考記事

[bundle, bundle execについて](https://qiita.com/dawn_628/items/1821d4eef22b9f45eea8)

[薄いRailsプロジェクトをRails newする](https://qiita.com/shinkuFencer/items/e6b4e24a92f7b34e9f24)