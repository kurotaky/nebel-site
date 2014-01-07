---
title: SqaleからAmazonS3にDBをバックアップする
date: 2014-01-05 18:34:38 +0900
---

Sqale で運用しているアプリケーションのDBのdumpファイルを
S3のバケットに保存する方法です。

## はじめに

AWSのAccess Keyを管理画面で閲覧してメモしておいてください。
Security Credentials を選択、Access Keys をクリックするとAccess Key IDが表示されます。

こちらにアクセスキーに関する説明があります。

* http://blogs.aws.amazon.com/security/post/Tx1R9KDN9ISZ0HF/Where-s-my-secret-access-key

## S3にバケット作成する

gateway.sqale.jp にsshログイン。

```
ssh gateway.sqale.jp -p 2222
```

以下のコマンドを入力したあと、AWSのアクセスキーとシークレットキー入力します。

```
s3cmd --configure

```

`s3cmd mb` コマンドでS3にバケットを作成します。

```
s3cmd mb s3://sampleapp-backup
```

以下のようにメッセージが出力されれば、バケットの作成が完了です。

```
Bucket 's3://sampleapp-backup/' created
```

## S3にdumpファイルをアップロードする
`s3cmd put` コマンドでdumpファイルをアップロードします。

```
s3cmd put 20140105-sampleapp-mysql.dump s3://sampleapp-backup/20140105-sampleapp-mysql.dump
```

## 定期的にdumpファイルをS3に保存する
以下のようにrake task を作成してcronで設定すれば、
定期的にdumpファイルを保存することができます。

```ruby
namespace :db do
  desc "mysql dump: db backup to Amazon S3"

  task :backup => :environment do
    system "mysqldump -u #{ENV['SQALE_USERNAME']} -h #{ENV['SQALE_HOST']} -p #{ENV['SQALE_DATABASE']} --password=#{ENV['SQALE_PASSWORD']} > ../tmp/#{Time.now.strftime('%Y%m%d')}-sampleapp-mysql.dump"
    system "s3cmd put ../tmp/#{Time.now.strftime('%Y%m%d')}-sampleapp-mysql.dump s3://sampleapp-backup/#{Time.now.year}/#{Time.now.month}/"
  end
end
```

## 参考URL
* http://blogs.aws.amazon.com/security/post/Tx1R9KDN9ISZ0HF/Where-s-my-secret-access-key
* https://sqale.jp/support/manual/db-backup-restore
