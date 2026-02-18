+++
date = '2026-02-17T21:28:22Z'
draft = false
title = 'ブログ構築できたよ！'

categories = ['Hugo']
tags = ['Hugo', 'ブログ構築']
+++

Hugoでブログを構築しました。
簡単に構築手順をまとめてみます。

動作環境

- OS: Ubuntu 24.04
- Hugo: v0.155.3
- Git: 2.43.0

## ブログ構築手順

### 1. Hugoのインストール

色々とインストール方法はありますが、私はsnapを利用してインストールしました。

```bash
$ sudo snap install hugo
```

### 2. 新しいHugoサイトの作成

```bash
$ hugo new site tech-blog
$ cd tech-blog
```

### 3. テーマの追加

今回は、HugoのPaperModテーマを使用しました。
GitHubからテーマを`submodule`で追加します。

```bash
$ git init
$ git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### 4. テーマの設定

`hugo.toml`ファイルを編集して、テーマを指定します。

```toml
theme = 'PaperMod'
```

試しにHugoのサーバーを起動してみましょう。

```bash
$ hugo server
... 省略 ...
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:37809/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

![Hugoのサーバー起動](https://image.blog.pokapy.com/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202026-02-19%20010201.png)

これで、ブラウザで`http://localhost:37809/`にアクセスすると、Hugoのサイトが表示されるはずです。
VSCodeからSSHでサーバーに接続しているので、ありがたいことに勝手にポートフォワーディングしてくれていました。

### 5. ブログ記事の作成

新しいブログ記事を作成するには、以下のコマンドを使用します。

```bash
$ hugo new posts/test-poka.md
```

`content/posts/test-poka.md`に新しいMarkdownファイルが作成されます。
このファイルを編集して、ブログ記事の内容を記述します。

... あとでかく