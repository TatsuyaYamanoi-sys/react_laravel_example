# dockerを用いた環境構築

## コード使用者側
### 【Backend】
1. 
 - 

### 【Frontend】
1. 
 - 


## コード作成者側手順
### 【Backend】
1. $ docker exec -it example-be sh
 - backendコンテナに接続

2. $ composer create-project laravel/laravel example_backend
 - コンテナ内でLaravelプロジェクトの作成

3. $ cd example_backend
   $ php artisan serve --host 0.0.0.0
 - 動作確認。http://localhost:8000 へアクセスしてください。

4. $ composer require laravel/breeze --dev
   $ php artisan breeze:install api
   Which stack would you like to install?
    -> react
   Would you like to install dark mode support? (yes/no) [no]
    -> yes
   Would you prefer Pest tests instead of PHPUnit? (yes/no) [no]
    -> no
 - LaravelBreeze インストール
 - artisanコマンドを実行すると.envファイルに環境変数のFRONTEND_URLが設定されます。
 - フロントエンドとバックエンドのオリジンが異なっていても通信が行えるようにCORS(Cross-Origin Resource Sharing)の設定も行われます。
 - configフォルダのcors.phpファイルを確認すると.envファイルに設定したFRONTEND_URLがallowed_originsの配列に含まれていることが確認できます。
5. $ php artisan migrate
 - 再度マイグレート

6. $ docker cp example-app:var/www/html/ src
 - コンテナのファイル群をホスト側で編集できるようにコピーします。


### 【Frontend】
1. $ docker exec -it example-fe Bash
 - frontendコンテナに接続

2. $ npx create-react-app
   $ npx create-next-app
   $ git clone https://github.com/laravel/breeze-next.git app
 - 必要に応じてReactプロジェクト・Nextプロジェクトの作成。もしくはbreeze-nextのクローン。

3. $ cd app
   $ npm install
 - package.jsonが作成されるので依存関係ライブラリをインストール

4. $ npm run dev
 - 動作確認

 