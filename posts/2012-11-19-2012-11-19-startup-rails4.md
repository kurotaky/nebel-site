---
title: rails4(edge)を動かしてみた。
date: 2012-11-19 03:47:26 +0900
---

rails4(edge)をlocal環境で動かしてみたのでメモ(2012/11/18)。

※ 修正しました。(2012/11/20)

bundler(1.2.2)以上が必要なので、gem updateした。  

    gem update bundler
  
githubからrailsをcloneする。  
  
    cd ~/rails-projects/

    git clone git://github.com/rails/rails.git

rails new --edgeを実行。(test-appを作成する。)

    rails/railties/bin/rails new test-app --edge
 
localで動かしてみる。

        # test-appに移動
        cd test-app

        # scaffold
        rails g scaffold Product title:string description:text image_url:string price:decimal

        # マイグレーションの実行
        rake db:migrate

        # rails server
        rails s

http://localhost:3000/products にアクセスしてアプリケーションが作成されているのを確認できた。

http://localhost:3000/rails/info/properties にアクセスして、
RailsのVersionが4.0.0.betaになっているのを確認した。


## 参考
- [Ruby on Rails Edge Guides](http://edgeguides.rubyonrails.org/)

- [Rails](https://github.com/rails/rails)

- [Rails 4 in 30'](https://speakerdeck.com/spastorino/rails-4-in-30)

- [Rails 4 links compilation](http://blog.wyeworks.com/2012/11/13/rails-4-compilation-links/)