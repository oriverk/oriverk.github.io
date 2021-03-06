---
layout: blog
title: Postページを中心に改修した（N度目
categories: [blog]
tags: [update]
permalink: blog/:title
---

# {{ page.title }}
<span>{% include svg/tag.svg %}{% for tag in site.tags %}{{ tag[0] }},&nbsp;{% endfor %}&nbsp;Updated at&nbsp;{{ "now" | date: "%Y.%m.%d" }}</span>

まず始めに、改修後のデザイン(色)は完全に自分好みに仕上げた。

- ダークテーマ（目に優しい
- 青と黒
- モバイルファーストスタイル

## 改修内容
- デザインの変更
	- Bootstrapの排除
- Posts.indexページの追加
- Post.showページの追加
  - Syntax-highlighter Rougeの導入

## デザイン変更
[ページ表示速度](https://developers.google.com/speed/pagespeed/insights/?hl=JA&url=https%3A%2F%2Foriverk.github.io%2F&tab=mobile)を向上させるため、メニュータブにしか使っていないBootstrap由来のJSとCSSを排除し、自作のjsスクリプトを追加した。

```javascript
<script>
  'use strict';
    {
      const menuItems = document.querySelectorAll('.menu li a');
      const contents = document.querySelectorAll('.content');

      menuItems.forEach(clickedItem => {
        clickedItem.addEventListener('click', e => {
          e.preventDefault();

          menuItems.forEach(item => {
            item.classList.remove('active');
          });
          clickedItem.classList.add('active');

          contents.forEach(content => {
            content.classList.remove('active');
          });
          document.getElementById(clickedItem.dataset.id).classList.add('active');
        });
      });
    }
</script>
```

## Syntax-highlighter Rougeの導入
Posts.indexとPost.showページはjekyll通りなので割愛。
コードのハイライトを有効化する為、Rougeを導入した。

```ruby
gem 'rouge'
```

```yml
_config.yml
markdown: kramdown
highlighter: rouge
```
この場合だと通常通りの`highlight`と`endhighlight`を用いるが、Qiitaの様なコードブロックの記法にしたかったので、kramdownのオプション等を指定した。(下)

```yml
_config.yml
markdown: kramdown
kramdown:
   input: GFM
   hard_wrap: false
highlighter: rouge
```

あとは`rougify style [<theme-name>]`でシンタックスハイライト用のcss、今回はmolokaiを生成し、一部修正、適用させた。

## 改修予定
- IE, Edge対応（IE対応は見送りました。)
  - picture属性、svg属性など
  - 他全部
- Postページの運用方法を考える
  - Qiitaに投稿するのか、こちらに書くか、別にはてぶを用意するのか。
- AMPの導入。興味があるだけ