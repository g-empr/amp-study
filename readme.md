# AMPコーディング、またはAMPリプレイスにおけるチェック項目
## AMP(Accelerated Mobile Pages)とは？
GoogleとTwitterで共同開発されている、スマホなどのモバイル端末でウェブページを高速表示するためのプロジェクト、またはそのためのフレームワーク(AMP HTML)を指す。

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
### 
### 
### 
### 
### 
