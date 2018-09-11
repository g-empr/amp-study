# AMPコーディング、またはAMPリプレイスにおけるチェック項目
![ロゴ](/img/amp.jpg)
## AMP(Accelerated Mobile Pages)とは？
GoogleとTwitterで共同開発されている、スマホなどのモバイル端末でウェブページを高速表示するためのプロジェクト、またはそのためのフレームワーク(AMP HTML)を指す。  
  
Googleでの検索において、検索結果の上部に表示され、訪問者またはCVを増やすことに貢献できるモバイルコーディングの新しい基準である。  
  
![検索結果画面](/img/amp-search.png)  
※AMPありの検索結果(左)とAMPなしの検索結果(右)

## TL;DR
以下のようなコードが基礎の土台となる。
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
## コーディングにおける制限
- 独自のJavascriptライブラリを組み込めない
- 一部の広告を使えない
- URLの正規化が必要
- SEOには直接的には関係ない
### 独自のJavascriptライブラリを組み込めない
### 
### 
### 
### 
