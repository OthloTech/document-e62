author: ReERishun
summary: Firebaseハンズオン資料
id: docs
categories: codelab,markdown
environments: Web
status: Published
feedback link: A link where users can go to provide feedback (Maybe the git repo)
analytics account: Google Analytics ID

# Firebase×JavaScript 1DAY実践ハンズオン

## Firebaseを学ぼう！
Duration: 0:05:00

今回はFirebaseについて学びますが、まずは「Firebaseとは？」という部分から解説からしていきます。

### Firebaseとは
Firebaseとは、Firebase Incが開発し、現在では買収先のGoogleが提供しているモバイル・Webアプリケーション開発プラットフォームです。


### 今回学ぶ製品
Firebaseには18個以上の製品があります。
今回はその中から3つ利用します。

### Firebase Authentication

Firebase Authenticationは、SNSなどの会員情報を用いた認証をアプリケーションに導入できます。

[Firebase Authentication - Firebase](https://firebase.google.com/docs/auth?hl=ja)

### Firebase Hosting

Firebase Hostingは、作成したWebアプリケーションを簡単にホスティングできるサービスです。

[Firebase Hosting - Firebase](https://firebase.google.com/products/hosting?hl=ja)

### Realtime Database

Realtime Databaseはリアルタイムでデータを共有/同期できるNoSQLのデータベースです。

[Firebase Realtime Database - Firebase](https://firebase.google.com/products/realtime-database?hl=ja)
[NoSQLについて勉強する。 - Qiita](https://qiita.com/t_nakayama0714/items/0ff7644666f0122cfba1)

## 新規プロジェクトの作成（GUIの場合）
Duration: 0:10:00

それでは、最初に新規のプロジェクトを作成します。
まずは下記ボタンからコンソールを開いてください。

<button>
  [Firebaseコンソールへ移動](https://console.firebase.google.com/)
</button>

以下の画面が表示されたかと思いますので、**[プロジェクトの作成]**をクリックしてください。

![](./img/new_project.png)

### プロジェクト名の指定
プロジェクト名を決めます。
基本的に半角英数字で指定してください。

![](./img/setname.png)

尚、「-!'"」の記号は使用できます。


### Googleアナリティク
アナリティクスをOFFにしてください。
その後、[続行]を押して下さい。

![](./img/new_project3.png)

### 作成完了
下の画面のようにプロジェクトの作成が完了したら[続行]を押してください。

![](./img/new_project5.png)

## Webアプリの追加（GUIの場合）
Duration: 0:05:00

Webアプリケーションを追加します。
プロジェクトのホーム画面からWebのロゴをクリックしてください。

![](./img/new_project6.png)

名前を指定して、[このアプリのFirebase Hostingも設定します。]にチェックを入れます。

![](./img/web2.png)

FirebaseSDKを追加します。
表示されているスクリプトをコピーしてください。

![](./img/web3.png)

index.htmlのhead内の「Firebase SDKの追加部分」にペーストしてください。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Welcome to Firebase Hosting</title>

    <!-- Firebase SDKの追加部分 開始 -->
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="/__/firebase/7.23.0/firebase-app.js"></script>

    <!-- TODO: Add SDKs for Firebase products that you want to use
        https://firebase.google.com/docs/web/setup#available-libraries -->

    <!-- Initialize Firebase -->
    <script src="/__/firebase/init.js"></script>
    <!-- Firebase SDKの追加部分 終了 -->

    <link rel="stylesheet" href="./css/style.css">
  </head>
```

続いてFirebaseCLIのインストールについて出てきますが、こちらは事前準備の際に行っていただいた内容になりますので、そのまま次に進んでいただいて大丈夫です。

![](./img/web4.png)

続いてもひとまず飛ばして、コンソールへ進んでください。

![](./img/web5.png)

これで、FirebaseへのWebアプリケーションの追加が完了しました。

## テンプレートのダウンロード
Duration: 0:03:00

今回は、1からCSSやHTMLを書いていくのは大変ですので、こちらで用意したプロジェクトを基に開発していただきます。
GitHub上にコードが置いてあるので、GitHubを利用したことのある方は、cloneをお願い致します。

### GitHubを利用されている方

任意のディレクトリにてクローンしてください。

```console
git clone git@github.com:OthloTech/firebase-hands-on.git
```

### GitHubを利用されていない方

まずは、以下のサイトにアクセスしてください。

[OthloTech/firebase-hands-on - GitHub](https://github.com/OthloTech/firebase-hands-on)

続いて、緑色のcodeボタンを押して、「Download ZIP」を押してZIPファイルをダウンロードしてください。

![](./img/web5.png)

ダウンロードした zipファイルを開き、中のプロジェクトを任意のディレクトリにペーストしてください。

## Firebase CLIでの初期化
Duration: 0:08:00

事前準備の際にインストールしていただいたFirebase CLIを利用していきます。
まずは先程プロジェクトをクローン/ペーストしたディレクトリに移動し、初期化を行います。

```console
$ firebase init
```
以下のような質問が表示された場合は`y`と答えてください。

```
? Are you ready to proceed? (Y/n) y
```

続いて、利用する製品を選択します。
今回は、
- RealtimeDatabase
- Hosting
を利用するので、**Database**と**Hosting**を選択してください。

```console
? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choices.
❯◉ Database: Deploy Firebase Realtime Database Rules
 ◯ Firestore: Deploy rules and create indexes for Firestore
 ◯ Functions: Configure and deploy Cloud Functions
❯◉ Hosting: Configure and deploy Firebase Hosting sites
 ◯ Storage: Deploy Cloud Storage security rules
 ◯ Emulators: Set up local emulators for Firebase features
 ◯ Remote Config: Get, deploy, and rollback configurations for Remote Config
```
選択方法はスペースキーを押すと選択できます。十字キーで移動し、選択完了後はEnterキーを押してください。

続いて、プロジェクトの選択を行います。
実は先程ブラウザ上で行ったプロジェクト作成作業はCLIでもできるのですが、今回は作成してあるので、「Use an existing project」を選択します。

```
? Please select an option:
  Use an existing project
> Create a new project
  Add Firebase to an existing Google Cloud Platform project
  Don't set up a default project
```

プロジェクトのIDを指定してください。
但し、IDは必ず全体で一意のIDである必要があるため、ありふれた名前はお勧めしません。

```
? Please select an option: Create a new project
i  If you want to create a project in a Google Cloud organization or folder, please use "firebase projects:create" instead, and return to this command when you've created the project.
? Please specify a unique project id (warning: cannot be modified afterward) [6-30 characters]:
 () ここにプロジェクトのIDを指定
```

作成するプロジェクトの名前を指定してください。
```
? What would you like to call your project? (defaults to your project ID)
```
ここはエンターキーを押せば先程指定したIDが指定されます。
コンソールでの表示名に使用されたりするので、分かり易い名前を付けてみてはどうでしょうか？


あとはほとんどEnterで大丈夫です。

データベースのルールを記載するファイルの名前を聞いてます。
デフォルトで大丈夫なのでEnter
```
? What file should be used for Database Rules? (database.rules.json)
```

公開するディレクトリを聞いています。
今回こちらで用意したプロジェクトではpublicディレクトリが公開するディレクトリであるため、デフォルトのままでエンターキーを押してください。

```
What do you want to use as your public directory? (public)
```

Noで大丈夫です。

```
? Configure as a single-page app (rewrite all urls to /index.html)? (y/N) 
? File public/404.html already exists. Overwrite? No
? File public/index.html already exists. Overwrite? No
```

## Databaseの設定
Duration: 0:05:00

さて、これで大体の準備が整ったので、早速色々と開発していきたいのですが、その前に更に一つ。
今回利用予定の製品の1つ、RealTimeDatabaseのルールを定義している「database.rules.json」の編集を行います。

```json
{
  /* Visit https://firebase.google.com/docs/database/security to learn more about security rules. */
  "rules": {
    ".read": false,
    ".write": false
  }
}
```

初期状態ではこのようになっているかと思います。
これを、以下のように書き換えてください。

```json
{
  /* Visit https://firebase.google.com/docs/database/security to learn more about security rules. */
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

ここで何を変更したのかというと、
- データベースの読み取りがfalse（誰でも読み取り不可）をtrue（誰でも読み取り可）
- データベースの書き込みがfalse（誰でも書き込み不可）をtrue（誰でも書き込み可）
という風に変更しました。これは誰でも読み書きができるという点では安全性に問題があります。


## サーバとデプロイ
Duration: 0:05:00

今回利用するFirebaseHostingには開発したアプリケーションを簡単にデプロイできるコマンドが用意されています。

```console
$ firebase deploy
```

コマンド実行後、デプロイが完了すると以下のようにURLがコンソールに表示されます。

```
Hosting URL: https://xxxxxxxxxxx.web.app
```

xx～の部分には最初に指定したプロジェクトのIDが入っており、このページにアクセスすると実際に開発したものが確認できます。

しかし、毎回デプロイせずともローカルでもしっかりと確認したいですよね？
その場合は以下のコマンドでローカルでも確認できます。

```console
$ firebase serve
```

今回のハンズオンでは基本的にローカルでの確認を行いながら進めていきます。

## Authenticationの設定
Duration: 0:05:00

Authentication（認証機能）の設定を行います。
今回はGoogleアカウントによる認証のみに対応させます。

左側のナビゲーションから**Authentication**を選択し、**Sign-in method**のタブを開いてください。

![](./img/auth1.png)

認証方法の一覧が表示されますので、Googleをクリックして下さい。

![](./img/auth2.png)

表示されたら、
1. **有効にする**をONに
2. **プロジェクトのサポートメール**を選択
3. **保存**を押してください。

![](./img/auth3.png)

以上で Authentication の設定は完了です。

## Firebaseのスクリプトの読み込み
Duration: 0:02:00

Firebase用のSDKを追加します。
`public/index.html` を開き、以下のように `<!-- FirebaseのSDK追加部分 -->` の部分にSDKを追加してください。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>ChatApp</title>

  <!-- FirebaseのSDK追加部分 開始 -->
  <script defer src="/__/firebase/7.23.0/firebase-app.js"></script>
  <script defer src="/__/firebase/7.23.0/firebase-auth.js"></script>
  <script defer src="/__/firebase/7.23.0/firebase-database.js"></script>
  <script defer src="/__/firebase/init.js"></script>
  <!-- FirebaseのSDK追加部分 終了 -->

  <link rel="stylesheet" href="./css/style.css">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP&display=swap" rel="stylesheet">
</head>
```

`/__/firebase/firebase-app.js` と `/__/firebase/init.js` は必ず必要ですが、`/__/firebase/7.23.0/firebase-auth.js` や `/__/firebase/7.23.0/firebase-database.js` は利用するプロダクトを追加していますので、プロジェクトによって呼び出す製品は変わってきます。

## 認証処理の作成
Duration: 0:10:00

それでは、認証処理を実装していきます。

### 認証処理の作成

`public/js/index.js` へ以下のコードを追加します。

```javascript
// 認証処理作成箇所
function auth() {
  const provider = new firebase.auth.GoogleAuthProvider();
  // Google認証のポップアップ表示
  firebase
    .auth()
    .signInWithPopup(provider)
    .then((result) => {
      // 認証成功
      const user = result.user;
      enableMessages(user);
    })
    .catch(function (error) {
      // 認証失敗
      alert("アカウント連携に失敗しました");
      console.log({ error });
    });
}
```

ここでは、Google認証のポップアップを呼び出し認証を行った結果を受け取ります。

1. Googleプロバイダオブジェクトのインスタンスを作成

```javascript
  const provider = new firebase.auth.GoogleAuthProvider();
```

2. 認証処理

```javascript
firebase
    .auth()
    .signInWithPopup(provider)
    .then((result) => {
      // 認証成功
      const user = result.user;
      enableMessages(user);
    })
    .catch(function (error) {
      // 認証失敗
      alert("アカウント連携に失敗しました");
      console.log({ error });
    });
```

3. 成功した場合、認証結果（ユーザ情報）を受け取る
```javascript
    .then((result) => {
      // 認証成功
      const user = result.user;
      enableMessages(user);
    })
```

4. 失敗した場合、エラーをアラートにて表示

```javascript
    .catch(function (error) {
      // 認証失敗
      alert("アカウント連携に失敗しました");
      console.log({ error });
    });
```

### ページを開いた際に認証を呼び出す

作成した認証処理をページのロード時に呼び出すようにします。
以下のコードを追記してください。

```javascript
// 認証の呼び出し箇所
document.addEventListener("DOMContentLoaded", () => {
  // DOMのリロードが終わったタイミングで認証開始
  auth();
});
```

このコードにより、ページを読み込むたびに認証を行うようになりました。

### テスト

それでは、ローカルで動作チェックしてみましょう。
以下のコマンドを実行してローカルでアプリを起動してください。

```
$ firebase serve
```

続いて、localhost:5000にアクセスしてください。

<button>
  [ローカルでテスト](http://localhost:5000)
</button>

すると、早速ポップアップがブロックされてしまい認証が失敗してしまいます。

![](./img/auth4.png)

リンクバーにあるポップアップブロックのアイコンをクリックし、**http://localhost:5000 のポップアップとリダイレクトを常に許可する**にチェックを入れ、**完了**を押してください。

![](./img/auth5.png)

すると、画像のようにアカウント一覧が表示されるかと思います。

![](./img/auth6.png)

自身のアカウントを選択し、ログインしてください。
以下のようにポップアップが表示されればログイン成功です！

![](./img/auth7.png)


## ユーザ一覧の作成
Duration 00:10:00

左側にユーザ一覧を作成します。

![](./img/user1.png)

### ユーザ情報の登録処理

まずは、ユーザ情報をデータベースに更新します。
先程作成した認証処理はAuthentication側がユーザ情報を持っていますので、現状ではデータベース内は空です。
そのため、ユーザ登録された内容をデータベースへ格納する処理を追加します。

```javascript
// ----- ユーザ情報登録/更新処理 ----- //
function updateUserinfo(user) {
    const userDb = firebase.database().ref("users/" + user.uid);

    userDb.set({
        uid: user.uid,
        displayName: user.displayName,
        photoURL: user.photoURL,
    });
}
```

ここでは、 `set()` メソッドを用いて、値をデータベースへ格納しています。
セットした値は users/XXXXXX(ユーザID) に格納されます。
もし既に同じユーザIDが格納されている場合は上書されます。

また、先程追加したコードも一部修正します。

```javascript
// ----- 認証処理作成箇所 ----- //
function auth() {
  const provider = new firebase.auth.GoogleAuthProvider();
  // Google認証のポップアップ表示
  firebase
      .auth()
      .signInWithPopup(provider)
      .then((result) => {
        // 新規コード追加部分
        console.log({ result });
        updateUserinfo(result.user);
      })
      .catch(function (error) {
        // 認証失敗
        alert("アカウント連携に失敗しました");
        console.log({ error });
      });
}
```

`//新規コード追加部分`と書いてある部分を元々の内容を削除し、2行を追加してください。
追加が完了後、再度 localhost:5000 へアクセスしログインしてみてください。

ログインが完了したら、Firebaseのコンソールへアクセスし、**Realtime Database** を開いてください。
以下のように usersドキュメントが追加されていればOKです。

![](./img/user2.png)


### ユーザ一覧を表示

RealTimeDatabase へ保存したユーザ情報を表示します。
以下のコードを追加してください。

```javascript
// ----- ユーザ一覧表示処理 ----- //
function renderUserslist(user) {
    const usersElm = document.querySelector("#users_list");

    // コールバック関数
    return (snapshot) => {
        const newUsers = [];

        // 自身を追加
        newUsers.push(`
          <div class="users_list__box-me">
            <div class="users_list__icon">
              <img src="${escapeHTML(user.photoURL)}" />
            </div><div class="users_list__status">
              <p class="users_list__name">${escapeHTML(user.displayName)}</p>
            </div>
          </div>
        `);

        // ユーザ情報を一つずつ取得し、表示用HTMLを組み立て
        snapshot.forEach((send_user) => {
            // 自分以外のユーザのみ追加
            if (user.uid !== send_user.val().uid) {
                newUsers.push(`
          <div class="users_list__box">
            <div class="users_list__icon">
              <img src="${escapeHTML(send_user.val().photoURL)}" />
            </div><div class="users_list__status">
              <p class="users_list__name">${escapeHTML(send_user.val().displayName)}</p>
            </div>
          </div>
        `);
            }
        });
        // ユーザ一覧表示エリアに描画
        usersElm.innerHTML = `
      <div>
        ${newUsers.join("")}
      </div>
    `;
        // スクロール最下部へ移動
        usersElm.scrollTop = usersElm.scrollHeight;
    }
}
```

少しコードが長くなってしまいましたが、要はユーザ情報を取得し、HTMLと結合させて描画しています。
自身の情報は必ず一番上に来るようにするため、一番最初に格納しています。
全ユーザ情報を描画する際には自身の情報は飛ばす用に if文を用いて分岐しています。

続いて、ユーザ情報更新処理側にコードを追加します。

```javascript
// ----- ユーザ情報登録/更新処理 ----- //
function updateUserinfo(user) {
    const userDb = firebase.database().ref("users/" + user.uid);

    userDb.set({
        uid: user.uid,
        displayName: user.displayName,
        photoURL: user.photoURL,
    });

    // 新規コード追加部分
    const usersDb = firebase.database().ref("users");
    usersDb.on("value", renderUserslist(user));
}
```

末尾2行が新たに追加した部分です。
使用している `on()` メソッドによりデータベースの変更を監視することが出来ます。
そのため、新しくユーザが追加された場合もページをリロードすることなく追加されるようになります。

### 実際に表示してみる

さて、再びログインしてみてください。
ログイン後、左側に自分のアイコンと名前が表示されていれば完了です。


## メッセージの送信処理作成
Duration 00:10:00

続いてメッセージの送信処理を作成します。

### 送信処理部分作成

以下のコードを追加してください。

```javascript
// ----- メッセージ送信処理箇所 ----- //
function enableMessages(user) {
    const messagesDb = firebase.database().ref("messages");

    // メッセージ送信イベント登録
    const messageTextInput = document.querySelector("#message-text");
    const messageButton = document.querySelector("#message-submit-button");

    // 送信ボタンが押された場合
    messageButton.addEventListener("click", () => {
        // DBへ新規メッセージの登録
        messagesDb.push({
            userId: user.uid,
            date: new Date().getTime(), // タイムスタンプをセット (例：1602862031298)
            text: messageTextInput.value,
        });
        // フォームの内容をリセット
        messageTextInput.value = "";
    });
}
```

ここでは、送信ボタンが押された際にテキストエリア内の文字列をデータベースへメッセージとして保存する処理を行っています。
`push()` メソッドを使うことでデータベース内の message 直下に

- ユーザID
- 送信日時
- 送信内容

が格納されます。
尚、 `push()` メソッドを利用した場合のメッセージ毎のIDはユニークなIDをランダムに振り分けられます。


### 呼び出し部分の追加

送信処理部分を作成しましたので、続いて送信処理を呼び出す部分を追記したいと思います。

```javascript
// ----- 認証処理作成箇所 ----- //
function auth() {
  const provider = new firebase.auth.GoogleAuthProvider();
  // Google認証のポップアップ表示
  firebase
      .auth()
      .signInWithPopup(provider)
      .then((result) => {
        console.log({ result });
        updateUserinfo(result.user);

        // 新規コード追加部分
        enableMessages(result.user);
      })
      .catch(function (error) {
        // 認証失敗
        alert("アカウント連携に失敗しました");
        console.log({ error });
      });
}
```

`// 新規コード追加部分` の後ろの1行を追加してください。


### データベースへメッセージが格納されることを確認

ここまで完了したら、一度メッセージを送信してみてください。
送信しても何も表示されないかと思います。
しかし、データベースを再度開いてもらうと messages が新たに追加されており、内容が確認できるかと思います。

![](./img/message1.png)

これで送信処理の完成です。


## メッセージの表示処理
Duration 00:10:00

先程追加した送信処理で送信した内容、他のユーザから送信された内容を表示できるように処理を追加します。

### ユーザ一覧をグローバル変数で管理

メッセージには送信したユーザに関する情報が、ユニークなIDしかありません。
そのため、ユーザ名やアイコンを取得するにはユーザの情報が必要になります。
まずは、ユーザ情報を格納する変数を用意します。

```javascript
// ----- グローバル変数 ----- //
let usersList = []; // ユーザ一覧
```

続いて、ユーザ一覧表示処理 に `// 新規コード追加部分` の1行処理を追加します。

```javascript
// ----- ユーザ一覧表示処理 ----- //
function renderUserslist(user) {
    const usersElm = document.querySelector("#users_list");

    // コールバック関数
    return (snapshot) => {
        const newUsers = [];

        // 新規コード追加部分
        usersList = snapshot.val();

        // 自身を追加
        newUsers.push(`
          <div class="users_list__box-me">
            <div class="users_list__icon">
              <img src="${escapeHTML(user.photoURL)}" />
            </div><div class="users_list__status">
              <p class="users_list__name">${escapeHTML(user.displayName)}</p>
            </div>
          </div>
        `);

        // ユーザ情報を一つずつ取得し、表示用HTMLを組み立て
        snapshot.forEach((send_user) => {
            // 自分以外のユーザのみ追加
            if (user.uid !== send_user.val().uid) {
                newUsers.push(`
          <div class="users_list__box">
            <div class="users_list__icon">
              <img src="${escapeHTML(send_user.val().photoURL)}" />
            </div><div class="users_list__status">
              <p class="users_list__name">${escapeHTML(send_user.val().displayName)}</p>
            </div>
          </div>
        `);
            }
        });
        // ユーザ一覧表示エリアに描画
        usersElm.innerHTML = `
      <div>
        ${newUsers.join("")}
      </div>
    `;
        // スクロール最下部へ移動
        usersElm.scrollTop = usersElm.scrollHeight;
    }
}
```

これで、ユーザ情報一覧の取得が可能になりました。


### 表示処理部分の追加

以下のコードを追加してください。

``` javascript
// ----- メッセージ表示処理箇所 ----- //
function renderMessages(user) {
    const messagesElm = document.querySelector("#chat-messages");
    // コールバック関数
    return (snapshot) => {
        const newMessages = [];
        // messageを一つずつ取得し、表示用HTMLを組み立て
        snapshot.forEach((message) => {

            if (user.uid === message.val().userId) {
                // メッセージの送信者が自分の場合
                newMessages.push(`
          <div class="chat-message-me">
            <div class="chat-message__text">
              <div class="chat-message__text-message">
                ${escapeHTML(message.val().text)}
              </div>
              <div class="chat-message__text-date">
                ${escapeHTML(formatDate(new Date(message.val().date)))}
              </div>
            </div>
          </div>
        `);
            } else {
                // 自分以外が送信したメッセージの場合
                newMessages.push(`
          <div class="chat-message-you">
            <div class="chat-message__icon">
              <img src="${escapeHTML(usersList[message.val().userId].photoURL)}" />
            </div>
            <div class="chat-message__text">
              <div class="chat-message__text-user-name">
                ${escapeHTML(usersList[message.val().userId].displayName)}
              </div>
              <div class="chat-message__text-message">
                ${escapeHTML(message.val().text)}
              </div>
              <div class="chat-message__text-date">
                ${escapeHTML(formatDate(new Date(message.val().date)))}
              </div>
            </div>
          </div>
        `);
            }
        });
        // メッセージ表示エリアに描画
        messagesElm.innerHTML = `
      <div>
        ${newMessages.join("")}
      </div>
    `;
        // スクロール最下部へ移動
        messagesElm.scrollTop = messagesElm.scrollHeight;
    }
}
```

こちらの処理は、先程ユーザ一覧を表示した際の処理内容とおおまかな流れは同じです。

### 呼び出し部分の追加

以下の `// 新規コード追加部分` を追加してください。

```javascript
// ----- メッセージ送信処理箇所 ----- //
function enableMessages(user) {
    const messagesDb = firebase.database().ref("messages");

    // 新規コード追加部分
    messagesDb.on("value", renderMessages(user));

    // メッセージ送信イベント登録
    const messageTextInput = document.querySelector("#message-text");
    const messageButton = document.querySelector("#message-submit-button");

    // 送信ボタンが押された場合
    messageButton.addEventListener("click", () => {
        // DBへ新規メッセージの登録
        messagesDb.push({
            userId: user.uid,
            date: new Date().getTime(), // タイムスタンプをセット (例：1602862031298)
            text: messageTextInput.value,
        });
        // フォームの内容をリセット
        messageTextInput.value = "";
    });
}
```

こちらもユーザ一覧を表示した際と同じく、`on()` メソッドを利用して、変更があった際に `renderMessages()` を呼び出すようにしています。

### 動作確認をしてみる

それでは、実際にメッセージを送ってみます。

![](./img/message2.png)

別のタブで新しく開いて、別のアカウントでログインするか、デプロイして他の人に共有することで他のアカウントともチャットできます。

## まとめ
Duration 00:05:00

ハンズオンお疲れ様でした。

今回のハンズオンでは、Firebaseの機能としては、

- Firebase CLI
  - Firebaseをコマンドラインで作成 / 編集 / 操作できるツール
- Firebase Hosting
  - Webアプリをデプロイできる
- Firebase Authentication
  - 認証を導入できる
- Realtime Database
  - NoSQLのデータベースを導入できる
  - 同期させることができる

を実際に使用しました。

また、RealTimeDatabaseでは以下の3つのメソッドを使用しました。

- `on()` : データベースを監視し変更等を同期できる
- `set()` : データベースへの新規追加 / 更新が可能
- `push()` : データベースへの新規追加が可能（IDはランダム）

Firebaseの機能は勿論これだけではありません。
ただ、一部分を触っただけでもわかる通り、簡単に実装でき、高品質のアプリケーションを開発することが可能です。
趣味の開発やハッカソンやコンテスト等で導入してみてはいかがでしょうか？

