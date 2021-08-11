# AWS APP Runner ハンズオンシナリオ

## 1. サンプルアプリケーションのデプロイ
### 1-1. Gitリポジトリのフォーク  
[@hkamedaさんのリポジトリ](https://github.com/harunobukameda/simple-express-app)からサンプルアプリケーションを自分のアカウントにフォークします

 ![フォーク](./img/github_folk.png)

### 1-2. App Runnnerの作成  
 - [App Runner](https://console.aws.amazon.com/apprunner/)にアクセスします
 - **App Runner サービスを作成**をクリックします
 ![](./img/app_runner_create.png)

### 1-3. App Runnerの設定
#### 1-3-1. ソースおよびデプロイ
 - ソース：ソースコードリポジトリを選択し、GitHubに接続の **新規追加** ボタンをクリックします

 ![](./img/app_runner_source.png)

 - 接続名に任意の名前を入力し、GitHubアカウントにログインします
 - ログイン後に、アカウントが自動選択されます

 ![](./img/github_connection.png)

 - 作成した接続名を選択します
 - リポジトリ: 1-1.でフォークしたリポジトリを選択
 - ブランチ: main

 ![](./img/app_runner_github.png)

 - デプロイ設定 自動

 - すべて入力したら **次へ** をクリックします

#### 1-3-2. 構築を設定
 - **ここで全ての設定を構成する** を選択します
 - ランタイム: Node.js 12
 - 構築コマンド: npm install
 - 開始コマンド: node index.js
 - ポート: 3000
 
 ![](./img/app_runner_build_settings.png)

 - **次へ** をクリックします

#### 1-3-3. サービスを設定
 - サービス名に任意の名前を入力して **次へ** をクリックします
 ![](./img/app_runner_service_settings.png)

#### 1-3-4. 確認および作成
 - 一番下までスクロールし、 **作成とデプロイ** をクリックします

```
おめでとうございます！これでApp Runnerの設定が終わりました。
デプロイが終わるまでコーヒーでも飲みながらTwitterにApp Runnerにデビューできたことを書き込んだりしてみてはいかがでしょう？
ツイートの際は、#jawsug #jawsugyokohamaのハッシュタグもご一緒に。
```

 - デプロイされると、ステータスが **Running** に変わります

 ![](./img/app_runner_build_success.png)

 - デフォルトドメインのリンクをクリックすると、アプリケーションが表示されます

## 2. アプリケーションの更新
ソースコードを変更して、自動デプロイの動作を確認していきます
### 2-1. ブランチの作成
 - 新しいブランチを作成して下さい

 ![](./img/create_branch.png)

### 2-2. ソースコードの修正

 - index.jsをクリックします
 - 編集アイコンをクリックします
 - Hello World！をHello World2！へ変更します
 - **Commit Changes** をクリックします

 ![](./img/modify_source.png)

 ```
 mainリポジトリではないので、まだ自動デプロイは動作しません。
 デプロイするために、ブランチをマージしていきましょう！
 ```

### 2-3. ブランチのマージ

  - **Compare & pull request** をクリックします

  ![](./img/pull_request.png)

  - `マージ先` を `自分のリポジトリ` の `main` に変更します
  - **Create pull request** をクリックします

  ![](./img/pull_request2.png)

  - **Merge pull request** をクリックします

  ![](./img/merge_pull_request.png)

  - **Confirm merge** をクリックします

```
これで自動デプロイが動きます
App Runnerの画面に戻って、デプロイが進行中かどうか確認しましょう
```
![](./img/deploy_app_runner.png)

```
Cloud shellから以下のコマンドを実行するとデプロイされる様子が確認できます
App Runnerのデフォルトドメインは書き換えてください

while true; do curl -s https:// **App Runnerのデフォルトドメイン** /; echo $(date); sleep 0.5; done

デプロイ確認後、Ctrl + C で終了します
```

## 3. オートスケール
