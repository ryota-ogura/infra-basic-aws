■WordPressのインストール
===

[WordPressについて](https://ja.wordpress.org/)

### DBサーバーへMySQLをインストールする

* DBサーバーへSSH ※手順省略
* MySQLをyumでインストール
```bash:
sudo yum -y install mysql-server
```
* MySQLサーバーを起動
```bash:
sudo service mysqld start
```
* MySQLのrootユーザのパスワードを変更
```bash:
mysqladmin -u root password
-> 新しいパスワードを入力（確認入力あり）
```
* MySQLコンソールにログインし、WordPress用のDBとwordpressユーザを作成。権限を付与。
```bash:
mysql -u root -p
(パスワードを入力)
mysql> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
mysql> grant all on wordpress.* to wordpress@"%" identified by 'wordpresspasswd';
mysql> flush privileges;
mysql> select user, host from mysql.user;
(wordpressユーザが居ることを確認)
mysql> exit
```
* MySQLサーバーの自動起動設定
```bash:
sudo /sbin/chkconfig mysqld on
```

### WebサーバーへWordPressをインストールする

* WebサーバーへSSH ※手順省略
* PHP, MySQL用ライブラリをyumインストール
```bash:
sudo yum -y install php php-mysql php-mbstring
```
* DB接続用にMySQLコマンドもyumインストール
```bash:
sudo yum -y install mysql
```
* DBサーバー上のMySQLへのログイン確認
```bash:
mysql -h 10.0.2.10 -u wordpress -p
(パスワードを入力)※「wordpresspasswd」の方
(ログイン出来たことを確認)
mysql> exit
```
* WordPressのダウンロード
```bash:
wget http://ja.wordpress.org/latest-ja.tar.gz
```
* アーカイブ展開、ファイル移動、所有者の変更
```bash:
tar xzvf latest-ja.tar.gz
cd wordpress/
sudo cp -r * /var/www/html/
sudo chown -R apache:apache /var/www/html
```

### WordPressの初期設定

* apacheを再起動（起動）する
```bash:
sudo /sbin/service httpd restart
```
* ブラウザでWebサーバーのパブリックIPを入力してアクセス
* WordPressの初期設定画面が表示されること
  1. 「さぁ、始めましょう！」
  2. 設定項目を入力して「送信」
    * データベース名：**wordpress** （デフォルト）
    * ユーザー名：**wordpress**
    * パスワード：**wordpresspasswd**
    * データベースのホスト名：**10.0.2.10**
    * テーブル接頭辞：wp_（デフォルト）
  3. 「インストール実行」
* ようこそ画面が表示されること
  * サイトのタイトル：好きなものを設定
  * ユーザー名：好きなものを設定（ブログへのログイン時必要）
  * パスワード：好きなものを設定（ブログへのログイン時必要）
  * メールアドレス：受信出来るアドレスを設定
  * 「WordPressをインストール」
* ログイン画面が表示されるので、直前に作成したユーザー名、パスワードでログイン
* WordPressダッシュボードが表示されること

**完成！**
記念に記事を投稿しましょう。
