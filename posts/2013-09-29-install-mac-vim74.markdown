---
title: install-mac-vim74
date: 2013-09-29 01:29:31 +0900
---

Vim7.4 が出ているのでインストールしました。  
http://vim-jp.org/blog/2013/08/10/vim_7.4_released.html

### macにVim7.4をインストールする。
MacVim-KaoriYa を使う場合、ダウンロードはこちらから。  
https://code.google.com/p/macvim-kaoriya/downloads/list

インストール後、Launchpad のMacVim アイコンをクリックすれば、
アプリケーションが起動されます。

コンソールで `vim` を使いたい場合は、alias でパスを指定する。
自分はzsh を使っているので、 `.zshrc` に以下のような設定を追記する。  
``` alias -g vim='/Applications/MacVim.app/Contents/MacOS/vim' ```

コンソールで ``` source ~/.zshrc ``` を入力して、変更を反映させる。

`which vim` を入力して ``` /Applications/MacVim.app/Contents/MacOS/vim ```
が表示されればOK。
