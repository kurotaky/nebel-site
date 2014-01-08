---
title: ggplot2をインストールして使うまで
date: 2014-01-09 01:45:38 +0900
---

## ggplot とは

## インストール

Rコンソールを開いて以下のコマンドを入力する。

```
install.packages("ggplot2")

```

## グラフを出力する

```
> library(ggplot2)
> data <- read.csv("/Users/yuta/201401-lines-of-code.csv")
> data
  day lines
1   1    53
2   2   100
3   3    64
4   4     0
5   5     8
6   6    34
7   7    79
8   8   206
> ggplot(data, aes(x=day, y=lines)) + geom_line() + geom_point()

```