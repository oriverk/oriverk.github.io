---
layout: blog
title: Github Pagesのメージャーアップデートをした。
categories: [blog]
tags: [update]
permalink: blog/:title
---

# {{ page.title }}
<span>{% include svg/tag.svg %}{% for tag in site.tags %}{{ tag[0] }},&nbsp;{% endfor %}&nbsp;Updated at&nbsp;{{ "now" | date: "%Y.%m.%d" }}</span>

## What I did
- Introduce IE Buster
- Update Ruby version from 2.5.1
- Make Dark-theme better
- Add top-image and githubpage-svg

## IE Buster
リンク:[https://ie-buster.qranoko.jp/](IE BUSTER)
IE環境下ではSVG周辺でデザインが崩れることが確認されたが、Chrome使用を促すJSを追加した。

## Update Ruby-version to 2.7.0
Ruby用に作成している仮想環境のアップデートの序にRubyのバージョンを最新版に上げた。

- 参考
  - [永久保存版！？伊藤さん式・Railsアプリのアップグレード手順](https://qiita.com/jnchito/items/0ee47108972a0e302caf)

- エラー内容
  - 他のgemやミドルウェアとの依存関係に由来するもの
  - rubyのキーワード因数に関する非推奨警告

## Dark theme
前回までは、基本グレーで背景に青、差し色でオレンジを使用していた。

- 参考
  - [Material Design Dark theme](https://material.io/design/color/dark-theme.html)
  - [Color Tool](https://material.io/resources/color/#!/?view.left=0&view.right=1&primary.color=121212&secondary.color=7bd0e7)
  - [DarkModeのデザインを中心とした色彩設計の考え方](https://kudakurage.hatenadiary.com/entry/2019/07/29/083000)

## Add top-image and others
トップ画面にプロフィール画像を追加し、またサイトリンクQRコードを表示されるように、javascriptを作成した。

```javascript
<script>
  'use script';
  {
    const githubpage = document.getElementById('githubpage-svg');
    const profile = document.getElementById('profile-img');

    profile.addEventListener('click', ()=>{
      profile.classList.remove('active');
      githubpage.classList.add('active');
    });

    githubpage.addEventListener('click', ()=>{
      githubpage.classList.remove('active');
      profile.classList.add('active');
    });
  }
</script>
```
## 残す改修予定
- add Tags
- AMPの導入。興味があるだけ