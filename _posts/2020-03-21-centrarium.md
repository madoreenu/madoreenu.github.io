---
layout: post
title: JekyllのテーマをCentrariumにしたい人へ
date: 2020-03-21 21:35
tags: Jekyll
---

今月頭からこのサイトは[minima](https://github.com/jekyll/minima/)というテーマを使っていたのですが、見た目が単調すぎるので、いつかググって見つけた記事、[Jekyll themeをCentrariumに変更する](https://haltaro.github.io/2018/02/11/theme-change)を参考にさせていただいてこの方と同じようなかっこいいブログサイトにしたい、[Centrarium](https://github.com/bencentra/centrarium)テーマを使いたいな〜と思ったりしていました。

最初はよくわかっていなかったターミナルからGitHubにコミットする方法もだんだんわかるようになってきたところで（それから半月後）、参考にして同じことをやってみることにしました！

## ぶち当たった壁

この記事を参考にしながら個人設定を自分用に設定してローカルテストも終えいざコミット。

そこで自分のサイトhttps://madoreenu.github.io にアクセスしてみると、

![失敗](/assets/miss.png)

このような感じになり、ページ一覧が見えなくなってしまいました。

それから困って自分で色々なファイルをのぞいたりいろんな人に見てもらったりしても一向に原因が見つからなかったので、https://talk.jekyllrb.com/ で頑張って英語で質問したところ、**「使っているプラグイン`jekyll-paginate-v2`が新しすぎてGitHub Pagesで対応していない。」** という返事が返ってきました。
（参考にさせていただいていたサイトはもともと2017年あたりのものだったようで、初めから旧版が使われていたようです）

プラグインって何？レベルに無知だったのでどうすればいいのか全くわからず途方に暮れていたところ、[Poteto143](https://twitter.com/Poteto143)さんがものすごく時間をかけて見てくれて、

- `_config.yml` に
- `plugins` に `jekyll-paginate` を追記
- `paginate: 数値` を追記
- `Gemfile` に`gem "jekyll-paginate"` を追記

すればよいということを教えてくれました。

ようするに、`jekyll-paginate-v2`を旧版の`jekyll-paginate`に書き換えるということです。
`_config.yml`と`Gemfile`の中身の`jekyll-paginate-v2`を旧版に書き換えれば良いということですね。

よってyamlファイルは

```yaml
plugins:
  - jekyll-archives
  - jekyll-sitemap
  - jekyll-paginate
exclude:
  - "/vendor/"
```

こうなります。

実はこれだと**まだ何も変わりません。**

**`paginate: 数値` の追記が必要** らしいです。
ここでは`5`としましょう。

```yaml
plugins:
  - jekyll-archives
  - jekyll-sitemap
  - jekyll-paginate
exclude:
  - "/vendor/"
paginate: 5
```

こういうことですね。これは、トップページの目次に載せる投稿をいくつずつにするか？という指定です。

つまり、目次が縦に5投稿ずつになるということですね。矢印を押せばまたそれより前の5投稿が見えるというわけです。

この指定が旧版だと必須だったみたいです。

## まとめ

ここまで書いていて今やっと気がついたのですが、動かなかった元のyamlファイル、

```yaml
plugins:
  - jekyll-archives-v2 #Sorry, not GitHub Pages friendly!
```

ってご丁寧にコメントで注釈ついてました。。優しかった。。。コメント大事。。。

**皆さんもGitHub Pagesのサイトがなぜか違う挙動をするということがあったら、プラグインのバージョンが対応しているか確認してみてください。**

読んでくださりありがとうございました。きれいなサイトがやっとできて、超嬉しい。
半月でこんなに見た目のちゃんとしたサイトが作れると思っていませんでした。

やっぱチャレンジするって大事ですね。（）

先月まではターミナルからGitHubにコミットなんて絶対にできなかったので、成長しました！今では何も見なくてもできます。今まで知らなかったAtomの便利さもわかるようになりました。（ファイル内の変更点がわかります。）

これからはサイトの色を工夫したり色々したりしてみようと思います。広告入れるか迷い中。（収益が欲しいっていうより、やってみたいので）

トップページの綺麗な海と船とビルの写真は、私がカナダのビクトリアのダウンタウンで撮ったものです。カナダに帰りてえ〜〜

最後に、最初にあげた記事の作成者であるhaltaroさん、[Poteto143](https://twitter.com/Poteto143)さんありがとうございました。
