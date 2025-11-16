---
pubDatetime: 2020-01-09T18:00:00.000Z
title: GASを使ってTwitter自動いいねbotを作ってみた
featured: true
tags:
  - Google Apps Script
  - X (ex-Twitter)
  - 個人開発
  - 雑記
category: 技術関連
description: GASを使ってTwitter自動いいねbotを作ってみた
---

> [!note] **この記事は [`steins.gg`](<https://twitter.com/search?q=(steinsgg%20OR%20steins.gg%20OR%20%40SteinsGG)%20until%3A2021-01-01&f=live&src=typed_query>) から移行した記事です。**
>
> `.gg` ドメインの維持費が高いため `steins.gg` は閉鎖しました。

おはこんばんちは！
今回は、GASを使ってTwitter自動いいねbotを作ってみました。  
コピペで誰でも使えるので、ぜひ使ってみてください。

## 目次

## 挙動
- 自身のタイムラインに流れているツイートをいいねする。
  - ※1 引用RTのみ、画像のみ、リンクのみのツイートはいいねしない。
    - 危険な内容やスパムリンクだけのツイートの可能性があるため
  - ※2 URL（`https://〜`）やハッシュタグ（`#〜`）は「本文」とは見なさない。
  - ※3 「本文」が 6 文字以下のツイートはいいねしない。
    - そのユーザーの意志・意図が無いツイートの可能性が高いため
    - ※1 ※2 のとおり、リンクやハッシュタグは文字数としてカウントしない
  - ※4 1回の実行で同じユーザーのツイートを2回以上いいねしない。
    - 連投していた場合、何度もいいね通知が飛んで不快にさせてしまう可能性があるため
  - ※5 自身のツイートはいいねしない。

## 運用
実運用としては、getTimeLine() を手動実行するか、時間主導トリガー（例：30分に1回）を設定して自動実行する想定です。

## コード

### 使うGASライブラリ
- TwitterWebService

### main.gs
```javascript
// 認可用のインスタンス
var twitter = TwitterWebService.getInstance(
  "{consumerKey}",   // Twitter Apps で作成した API key
  "{consumerSecret}" // Twitter Apps で作成した API Secret key
);

var userList = [];

// 認可
function authorize(){
  twitter.authorize();
}

// 認可解除
function reset(){
  twitter.reset();
}

// 認可後のコールバック
function authCallback(request){
  return twitter.authCallback(request);
}


function getTimeLine() {
  var service  = twitter.getService();
  var json = service.fetch("https://api.twitter.com/1.1/statuses/home_timeline.json?exclude_replies=true&count=200&include_rts=false");
  var array = JSON.parse(json);

  array.map(function(tweet){
    fav(tweet);
  });

  Logger.log(userList)
  userList = [];
}

function fav(tweet) {
    var service = twitter.getService();

    // URL より前の文章だけ残す ※1
    var urlIndex = twiStr.indexOf("https://");
    if (urlIndex >= 0) {
      twiStr = twiStr.slice(0, urlIndex);
    }

    // ハッシュタグより前の文章だけ残す ※2
    var hashIndex = twiStr.indexOf("#");
    if (hashIndex >= 0) {
      twiStr = twiStr.slice(0, hashIndex);
    }

    if (twiStr.length > 6) { // 6 文字以上あるかどうか ※3
        Logger.log(tweet.user.screen_name + " : " + twiStr)
        if(userList.indexOf(tweet.user.screen_name) == -1){ // ※4
          if(tweet.user.screen_name != "{あなたのユーザーID}"){ // 例えば @steinsgg だったら "steinsgg" ※5
            try {
              service.fetch('https://api.twitter.com/1.1/favorites/create.json?id=' + tweet.id_str, {method: 'post'});
              userList.push(tweet.user.screen_name);
            } catch (error) { Logger.log(error) }
          }
        }
        Utilities.sleep(1500); // 最速で回すと API の RateLimit 制限に引っかかるため
    }
}
```

### appscript.json
```json
{
  "timeZone": "Asia/Tokyo",
  "dependencies": {
    "libraries": [{
      "userSymbol": "TwitterWebService",
      "libraryId": "1rgo8rXsxi1DxI_5Xgo_t3irTw1Y5cxl2mGSkbozKsSXf2E_KBBPC3xTF",
      "version": "2"
    }]
  },
  "webapp": {
    "access": "MYSELF",
    "executeAs": "USER_DEPLOYING"
  },
  "exceptionLogging": "STACKDRIVER",
  "oauthScopes": ["https://www.googleapis.com/auth/script.external_request", "https://www.googleapis.com/auth/datastore"]
}
```

## 応用編（2021/4/20 追記）

### 全てのツイートから特定の文字列を含んだツイートをいいねする

### 運用例
例えばゲーム一緒にするフレンドを増やしたい場合、`#〇〇フレンド募集` や `#いいねした人フォローする` を含んだツイートを検索していいねします。

```javascript
var userList = [];

// 追加: ターゲットのハッシュタグ
var TARGET_HASHTAGS = ['#PUBGフレンド募集', '#VALORANTフレンド募集'];

// 追加: 「いいねした人フォローする」系のキーワード
var LIKE_FOLLOW_KEYWORDS = [
  '#いいねした人フォローする',
  '#いいねした人全員フォローする '
];
```

```javascript
function fav(tweet) {
    var service = twitter.getService();

```

### 実際に運用してみた感想

私はPUBGやvalorantなどPCゲームをプレイすることが多いので、「#PUBGフレンド募集」「#VALORANTフレンド募集」などのタグが付いていて、「#いいねした人フォローする」などのいいねでフォローする系のツイートを自動でいいねする運用を1年ほど続けてみた。

なんとフォロワーが1万を突破した。しかし、こんなことで増やしたフォロワーは意味が無いことに気が付いた。
実際に遊ぶフレンドは数える程度だし、フォロワーが多いことで得することより損することの方が多い。初見で警戒されることも多々ある。

ただ、見た目上でもフォロワーを増やすことが具体的なビジネス戦略であったり、明確な目的があるアカウントであれば真似してみても良いかと思った。

~~また、グレーな話なのでにごすが、一定数フォロワーを増やしたアカウントをごにょごにょごにょ。~~
おっと誰か来たようだ
