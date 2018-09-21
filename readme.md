# AMPまとめ
![ロゴ](/img/amp.jpg)
## AMP(Accelerated Mobile Pages)とは？
GoogleとTwitterで共同開発されている、スマホなどのモバイル端末でウェブページを高速表示するためのプロジェクト、またはそのためのフレームワーク(AMP HTML)。  
  
Googleでの検索において、検索結果の上部に表示され、訪問者またはCVを増やすことに貢献できるモバイルコーディングの新基準である。  
  
![検索結果画面](/img/amp-search.png)  
※AMPありの検索結果(左)とAMPなしの検索結果(右)

## 基本構成
以下のコードが基本の構成。
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
---
## 検証(AMP導入前)
AMP HTML移行対象のソースコードを見ながら以下項目を検証し、AMP HTMLにする際に影響度の高いものをまとめていく。
- [ ] JavaScript/jQueryがどれだけ使われている(読み込まれている)か。(AMP内では専用ライブラリしか使えないため)
  - [ ] そのうち、AMPコンポーネントで代替できるものはどれか。
  - [ ] そのうち、使用されていないもの/AMP化に際して影響範囲の狭そうなものはどれか。
  - [ ] そのうち、広告やアナリティクスに関するものはどれか。
- [ ] 使われているCSSの記述の合計サイズは50kb以下に収まるか。
- [ ] 使用中のCSSプロパティの中に`!important`がどれだけ含まれているか。
- [ ] 仕様が制限されている要素がコード内にどれだけ含まれているか。
---
## チェック(AMP導入後)
AMP HTMLに対して以下項目をチェックする。
### meta部分
- [ ] `html`要素とともにamp、または⚡が宣言されているか。
- [ ] `head`の最初に`<meta charset="utf-8">`が記述されているか。
- [ ] `head`に`<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">`が記述されているか。
- [ ] `canonical`に元となるページ、または固有のURLが指定されているか。
- [ ] 元となるページがある場合、`canonical`とは別に元ページ側の`amphtml`にページURLが指定されているか。
- [ ] `head`内に下記のボイラープレートが記述されているか。  
```html
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```
- [ ] `head`の最後に`<script async src="https://cdn.ampproject.org/v0.js"></script>`が記述されているか。

### コンテンツ部分
- [ ] 下記の要素は使用されていないか。
  - applet
  - base
  - embed
  - frame
  - frameset
  - object
  - option
  - param
  - select
  - textarea
- [ ] 下記の要素は代替タグに変換されているか。
  - img → amp-img
  - video → amp-video
  - audio → amp-audeo
  - iframe → amp-iframe
- [ ] Class名の先頭が`-amp-`で始まっていないか。
- [ ] CSS部分の合計サイズは50kb以内に収まっているか。
- [ ] CSSは`head`内の`<style amp-custom> ~ </style>`でのみ書き込まれているか。
- [ ] CSS内のプロパティで`!important`が指定されているものはないか。
- [ ] JavaScriptやjQueryを外部から読み込んでいないか。または、それらがHTML内に記述されていないか。
### SEO関連
- [ ] 導入されている広告システムはGoogle AdSenseのみか。
- [ ] 導入されているアナリティクスはGoogle Tag Managerのみか。
---
## AMPコンポーネント
JavaScriptが使用できないため、動的な要素はAMPのライブラリからインクルードして設置することになる。
### [amp-3d-gltf](https://ampbyexample.com/components/amp-3d-gltf/) - glTFフォーマットのアセットを読み込み3Dモデルを表示するためのコンポーネント。
### [amp-access-laterpay](https://ampbyexample.com/components/amp-access-laterpay/) - [Laterpay](https://www.laterpay.net/)と連携するためのコンポーネント。後述の`amp-access`が必要になる。
### [amp-access](https://ampbyexample.com/components/amp-access/) - ログイン機能などユーザー認証に関する動的要素を組み込めるコンポーネント。
### [amp-accordion](https://ampbyexample.com/components/amp-accordion/) - 要素にアコーディオンの動きをつけるためのコンポーネント。
### [amp-ad](https://ampbyexample.com/components/amp-ad/) - AMP内での広告表示に関するコンポーネント。
### [amp-analytics](https://ampbyexample.com/components/amp-analytics/) - AMP内でのアナリティクスに関するコンポーネント。
### [amp-anim](https://ampbyexample.com/components/amp-anim/) - gifやwebPなどのアニメーションのある静止画フォーマットをサポートするためのコンポーネント。該当ファイルはHTTPSで読み込む必要がある。
### [amp-app-banner](https://ampbyexample.com/components/amp-app-banner/) - アプリのCTAを表示するためのコンポーネント。
### [amp-audio](https://ampbyexample.com/components/amp-audio/) - HTML5における`audio`要素を代替するためのコンポーネント。
### [amp-bind](https://ampbyexample.com/components/amp-bind/) - AMPページ内でインタラクティブにコンテンツを操作できるようにするコンポーネント。
### [amp-bodymovin-animation](https://ampbyexample.com/components/amp-bodymovin-animation/) - [Bodymovin](https://github.com/airbnb/lottie-web)アニメーションをサポートするためのコンポーネント。After Effectsから出力されるjsonファイルを読み込んで使う。
### [amp-brid-player](https://ampbyexample.com/components/amp-brid-player/) - [Brid Player](https://www.brid.tv/)をサポートするためのコンポーネント。
### [amp-brightcove](https://ampbyexample.com/components/amp-brightcove/) - [Brightcove](https://www.brightcove.com/en/)をサポートするためのコンポーネント。
### [amp-call-tracking](https://ampbyexample.com/components/amp-call-tracking/) - 電話番号を動的に表示しコールトラッキングを有効にするためのコンポーネント。
### [amp-carousel](https://ampbyexample.com/components/amp-carousel/) - カルーセル表示を実現するためのコンポーネント。
### [amp-dailymotion](https://ampbyexample.com/components/amp-dailymotion/) - [Dailymotion](https://www.dailymotion.com/)をサポートするためのコンポーネント。
### [amp-date-countdown](https://ampbyexample.com/components/amp-date-countdown/) - 設定された日時までのカウントダウンを表示するためのコンポーネント。
### [amp-date-picker](https://ampbyexample.com/components/amp-date-picker/) - 単一の日時や一定範囲の期間を選択表示するために使用するコンポーネント。
### [amp-dynamic-css-classes](https://ampbyexample.com/components/amp-dynamic-css-classes/) - 動的に要素のClassを操作するためのコンポーネント。
### [amp-experiment](https://ampbyexample.com/components/amp-experiment/) - GAと連携しユーザーテストなどの検証を行うためのコンポーネント。
### [amp-facebook-comments](https://ampbyexample.com/components/amp-facebook-comments/) - [Facebook](https://ja-jp.facebook.com/)のコメントモジュールを埋め込むためのコンポーネント。
### [amp-facebook-like](https://ampbyexample.com/components/amp-facebook-like/) - Facebookの「いいね」ボタンを埋め込むためのコンポーネント。
### [amp-facebook-page](https://ampbyexample.com/components/amp-facebook-page/) - Facebookページを埋め込むためのコンポーネント。
### [amp-facebook](https://ampbyexample.com/components/amp-facebook/) - Facebookの投稿や動画などを埋め込むためのコンポーネント。
### [amp-fit-text](https://ampbyexample.com/components/amp-fit-text/) - 該当エリア内のテキストサイズを自動調節してくれるコンポーネント。
### [amp-font](https://ampbyexample.com/components/amp-font/) - フォントの読み込みを制御するためのコンポーネント。
### [amp-form](https://ampbyexample.com/components/amp-form/) - HTML5における`form`要素とそれに付随する各要素を代替するためのコンポーネント。
### [amp-fx-collection](https://ampbyexample.com/components/amp-fx-collection/) - パララックスやフェードインなど各種視覚効果を制御するためのコンポーネント。
### [amp-fx-flying-carpet](https://ampbyexample.com/components/amp-fx-flying-carpet/) - フライングカーペットを設置するためのコンポーネント。
↓ こんなやつ。  
  
![フライングカーペット](/img/flying-carpet-ad.gif)
### [amp-geo](https://ampbyexample.com/components/amp-geo/) - ISOの国コードをベースにユーザーのロケーションを取得できるコンポーネント。
### [amp-gfycat](https://ampbyexample.com/components/amp-gfycat/) - [fycat](https://gfycat.com/)からanimated GIFを読み込むためのコンポーネント。
### [amp-gist](https://ampbyexample.com/components/amp-gist/) - [Gist](https://gist.github.com/)から単一のファイル、またはGist全体を読み込むためのコンポーネント。
### [amp-google-document-embed](https://ampbyexample.com/components/amp-google-document-embed/) - HTML内でPDFなどを表示させるためのコンポーネント。
### [amp-google-vrview-image](https://ampbyexample.com/components/amp-google-vrview-image/) - AMP内で360°のVRメディアを読み込むためのコンポーネント。
### [amp-hulu](https://ampbyexample.com/components/amp-hulu/) - [Hulu](https://www.happyon.jp/)の動画を埋め込むためのコンポーネント。
### [amp-iframe](https://ampbyexample.com/components/amp-iframe/) - HTML5における`iframe`要素を代替するためのコンポーネント。AMP対応していないページを見せる場合に有効。
### [amp-ima-video](https://ampbyexample.com/components/amp-ima-video/) - [IMA SDK](https://developers.google.com/interactive-media-ads/docs/sdks/html5/)によるインストリーム広告を読み込むためのコンポーネント。
### [amp-image-lightbox](https://ampbyexample.com/components/amp-image-lightbox/) - 画像をビューポートいっぱいに表示させるためのコンポーネント。
### [amp-image-slider](https://ampbyexample.com/components/amp-image-slider/) - ふたつの重なったイメージ画像の上で境界線を左右に動かし、比較するような動きをつけるためのコンポーネント。
### [amp-img](https://ampbyexample.com/components/amp-img/) - HTML5における`img`要素を代替するためのコンポーネント。
### [amp-instagram](https://ampbyexample.com/components/amp-instagram/) - [instagram](https://www.instagram.com/?hl=ja)上の写真や動画を読み込むためのコンポーネント。
### [amp-jwplayer](https://ampbyexample.com/components/amp-jwplayer/) - [JW Player](https://www.jwplayer.com/)の動画を読み込むためのコンポーネント。
### [amp-install-serviceworker](https://ampbyexample.com/components/amp-install-serviceworker/) - Google AMPなどからService Workerをインストールするためのコンポーネント。
### [amp-kaltura-player](https://ampbyexample.com/components/amp-kaltura-player/) - [Kaltura](https://corp.kaltura.com/)から動画を読み込むためのコンポーネント。
### [amp-lightbox-gallery](https://ampbyexample.com/components/amp-lightbox-gallery/) - `amp-img`などのコンポーネントに対してlightboxの動きをつけるためのコンポーネント。
### [amp-lightbox](https://ampbyexample.com/components/amp-lightbox/) - 一般的なlightboxの要素を提供するためのコンポーネント。
### [amp-list](https://ampbyexample.com/components/amp-list/) - CORS JSONによる動的なコンテンツ表示をするためのコンポーネント。
### [amp-live-list](https://ampbyexample.com/components/amp-live-list/) - ページ内でライブ更新を行うためのコンポーネント。
### [amp-mustache](https://ampbyexample.com/components/amp-mustache/) - mustache記法を用いて動的な表示をするためのコンポーネント。
### [amp-next-page](https://ampbyexample.com/components/amp-next-page/) - オートページャーを組み込むためのコンポーネント。
### [amp-o2-player](https://ampbyexample.com/components/amp-o2-player/) - [O2](https://www.o2.co.uk/)の動画を読み込むためのコンポーネント。
### [amp-pinterest](https://ampbyexample.com/components/amp-pinterest/) - [Pinterest](https://www.pinterest.jp/)のコンテンツを埋め込むためのコンポーネント。
### [amp-pixel](https://ampbyexample.com/components/amp-pixel/) - GETメソッドのリクエストを送るためのコンポーネント。
### [amp-reach-player](https://ampbyexample.com/components/amp-reach-player/) - [Beachfront Reach](http://beachfrontreach.com/)にホストした動画を読み込むためのコンポーネント。
### [amp-reddit](https://ampbyexample.com/components/amp-reddit/) - [reddit](https://www.reddit.com/)のコンテンツを埋め込むためのコンポーネント。
### [amp-selector](https://ampbyexample.com/components/amp-selector/) - formの選択肢を表示するためのコンポーネント。
### [amp-sidebar](https://ampbyexample.com/components/amp-sidebar/) - サイドバー/メニューを設置するためのコンポーネント。
### [amp-social-share](https://ampbyexample.com/components/amp-social-share/) - ソーシャルボタンを設置するためのコンポーネント。
### [amp-soundcloud](https://ampbyexample.com/components/amp-soundcloud/) - [SOUNDCLOUD](https://soundcloud.com/)の曲を再生するためのコンポーネント。
### [amp-springboard-player](https://ampbyexample.com/components/amp-springboard-player/) - [Springboard](http://www.springboardplatform.com/)にホストした動画を読み込むためのコンポーネント。
### [amp-sticky-ad](https://ampbyexample.com/components/amp-sticky-ad/) - スティッキー広告を表示するためのコンポーネント。
### [amp-timeago](https://ampbyexample.com/components/amp-timeago/) - 経過時間をタイムスタンプ形式で表示するためのコンポーネント。
### [amp-twitter](https://ampbyexample.com/components/amp-twitter/) - [Twitter](https://twitter.com/)のコンテンツを読み込むためのコンポーネント。
### [amp-user-notification](https://ampbyexample.com/components/amp-user-notification/) - ユーザーへの警告を表示するためのコンポーネント。
### [amp-video](https://ampbyexample.com/components/amp-video/) - HTML5における`video`要素を代替するためのコンポーネント。該当ファイルはHTTPSで読み込む必要がある。
### [amp-vimeo](https://ampbyexample.com/components/amp-vimeo/) - [Vimeo](https://vimeo.com/jp)にホストした動画を読み込むためのコンポーネント。
### [amp-vine](https://ampbyexample.com/components/amp-vine/) - Vineの動画を読み込むためのコンポーネントだが、Vineは2017年をもってサービスを終了している。
### [amp-youtube](https://ampbyexample.com/components/amp-youtube/) - [YouTube](https://www.youtube.com/)の動画を読み込むためのコンポーネント。

---
## AMPとCORS
### Same-Origin Policy
Same-Origin Policyとは、URLの
1. スキーム = `http://`, `https://`
2. ホスト = `www.hogehoge.com`
3. ポート = `80`

をもとに固有のオリジン(Webページ)を定義し、同一のオリジン以外からのJavaScript等のリソースに対してのアクセスを制限するための仕組みのことである。  
これによりセキュリティの強化が図られ、Webページの信頼性が保たれる。

### CORS(Cross-Origin Resource Sharing)
Same-Origin Policyの制約を緩和する役割を持つのがCORS(Cross-Origin Resource Sharing)である。  
通常XMLHttpRequestオブジェクトはSame-Origin Policyの制約を受けるが、アクセス先ページのHTTPレスポンスヘッダで許可しておけば、ブラウザでデータを取得することができる。

### XMLHttpRequest(XHR)
JavaScriptを使用してサーバーにHTTPリクエストを行うためのAPIの一種で、すでに読み込みが完了したWebページからHTTPリクエストを送り、HTMLやXMLのデータを受信することができる。この際ページ遷移を伴う必要がなく、非同期に通信を行うことができる。

### AMPにおけるCORSの設定など
フロント側ではなくサーバ側での対応になるため割愛。以下参考ページ。
- [CORS in AMP](https://www.ampproject.org/docs/fundamentals/amp-cors-requests)


