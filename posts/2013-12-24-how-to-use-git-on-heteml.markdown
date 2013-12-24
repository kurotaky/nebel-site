---
title: hetemlレンタルサーバーでgitを使う
date: 2013-12-24 08:45:47 +0900
---

## gitの初期設定

ターミナルを使ってsshでログインします。

```
ssh username@ssh***.heteml.jp -p 2222
```

2013/12/24現在gitのバージョンは1.7.3.4でした。

```
-bash-3.00$ pwd
/home/sites/heteml/users***/u/s/e/username

-bash-3.00$ git --version
git version 1.7.3.4
```

ログイン後、ユーザー名とメールアドレス等の設定をします。

```
# ユーザー名とメールアドレスの設定
git config --global user.email "username@example.com"  
git config --global user.name "username"

# 端末に色つきの文字を出力する
git config --global color.ui auto
```

設定を確認します。

```
git config --global --list
```

## heteml上にリポジトリを作成する

ディレクトリを作成して、移動します。

```
mkdir myproject
cd myproject
```

git init コマンドでリポジトリを作成します。

```
git init
```

```
Initialized empty Git repository in /home/sites/heteml/users***/u/s/e/username/myproject/.git/
```

index.html を作成します。

```
touch index.html
```

git status コマンドで変更内容を確認します。

```
git status
```

コマンドを実行すると、以下のように表示されます。

```
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	index.html
nothing added to commit but untracked files present (use "git add" to track)
```

git add コマンドを実行します。

```
git add index.html
```

git add した後に git status コマンドを実行すると、以下のように表示されます。

```
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   index.html
#

```

git commit コマンドでコミットします。

```
git commit -m 'first commit'
```

tig や git log で確認するとコミット履歴を見ることが出来ます。

## hetemlにリポジトリを作成してローカルPCからpushする
heteml に sshログインして、ディレクトリを作成します。

```
mkdir repos
cd repos
mkdir myproject.git
cd myproject.git
```

git init コマンドでリポジトリを作成します。
この時に `--bare` オプションを指定すると変更のみを管理するリポジトリを作成することができます。
また、 `--shared` オプションを指定すると共同リポジトリとして作成することが出来ます。

```
git init --bare --shared
```

ローカルPCでmyprojectのリポジトリを作成します。

```
mkdir myproject
cd myproject
git init
```

hetemlに作成したリポジトリのURLを git remote コマンドで登録します。

```
git remote add origin ssh://username@ssh***.heteml.jp:2222/home/sites/heteml/users***/u/s/e/username/repos/myproject.git
```

git remote -v で登録情報を確認できます。

```
git remote -v
```

ファイルを作成します。

```
touch a.txt
```

add して commit します。

```
git add .
git commit -m 'inital import'
```

hetemlのリポジトリにpushして変更内容を反映させます。

```
git push origin master
```

sshログインのためのパスワードを聞かれるので、入力して下さい。

```
-----------------------------------------------------
--***-------------------------------------------***--
--***---------------***-------------------------***--
--***---------------******----------------------***--
--********-********-******-********-***********-***--
--********-***--***-***----***--***-***********-***--
--***--***-********-***----********-***-***-***-***--
--***--***-***------******-***------***-***-***-***--
--***--***-********-******-********-***-***-***-***--
-----------------------------------------------------

username@ssh***.heteml.jp's password:
```

パスワードを入力すると、以下のようにhetemlのリポジトリに変更内容が反映されます。

```
Counting objects: 3, done.
Writing objects: 100% (3/3), 215 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ssh://kuro96@ssh160.heteml.jp:2222/home/sites/heteml/users160/k/u/r/kuro96/repos/myproject.git
 * [new branch]      master -> master
```

hetemlにsshログイン後、myproject.git に移動して、`git log -p` コマンドで変更内容を確認します。

```
cd repos/myproject.git
git log -p
```

以下のように変更が反映されていることを確認できます。

```
commit 522111a8845c66aebb95de63bb6a65d405d33c2c
Author: kurotaky <username@example.com>
Date:   Tue Dec 24 09:43:43 2013 +0900

    inital import

diff --git a/a.txt b/a.txt
new file mode 100644
index 0000000..e69de29
```


## 参考URL
* http://d.hatena.ne.jp/bannyan/20100308/1268066849
* http://git-scm.com/book/ja/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-Git-%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E5%8F%96%E5%BE%97

## 参考文献
* http://www.amazon.co.jp/dp/4274068641
