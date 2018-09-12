# AMPコーディング、またはAMPリプレイス準備
![ロゴ](/img/amp.jpg)
## AMP(Accelerated Mobile Pages)とは？
GoogleとTwitterで共同開発されている、スマホなどのモバイル端末でウェブページを高速表示するためのプロジェクト、またはそのためのフレームワーク(AMP HTML)。  
  
Googleでの検索において、検索結果の上部に表示され、訪問者またはCVを増やすことに貢献できるモバイルコーディングの新基準である。  
  
![検索結果画面](/img/amp-search.png)  
※AMPありの検索結果(左)とAMPなしの検索結果(右)

## TL;DR
以下のようなコードが基本の構成。
```HTML
<!doctype html>
<html ⚡>
  <head>
    <meta charset="utf-8">
    <title>Title</title>
    <link rel="canonical" href="https://target-url.com">
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
    <script async src="https://cdn.ampproject.org/v0.js"></script>
  </head>
  <body>
    ここにコンテンツ
  </body>
</html>
```
## AMP化チェックリスト
### meta部分
- [ ] `html`要素とともにamp、または⚡が宣言されているか。
- [ ] `head`の最初に`<meta charset="utf-8">`が記述されているか。
- [ ] `head`に`<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">`が記述されているか。
- [ ] `canonical`に元となるページ、または固有のURLが指定されているか。
- [ ] 元となるページがある場合、`canonical`とは別に元ページ側に`amphtml`にページURLが指定されているか。
- [ ] `head`内に下記のボイラープレートが記述されているか。  
```html
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```
- [ ] `head`の最後に`<script async src="https://cdn.ampproject.org/v0.js"></script>`が記述されているか。

### コンテンツ部分
- [ ] 