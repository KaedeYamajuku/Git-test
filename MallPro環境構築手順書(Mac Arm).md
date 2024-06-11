
## Eclipseのインストール
1. [ここから](https://willbrains.jp/index.html#/pleiades_distros2024.html) Eclipse2024のMac Arm JavaのFull Editionをダウンロードする。
2. ダウンロードしたdmgファイルでインストールを行う

## marven3のインストール
1. [ここから](http://maven.apache.org/download.cgi) [Binary zip archive](https://dlcdn.apache.org/maven/maven-3/3.9.7/binaries/apache-maven-3.9.7-bin.zip)をダウンロードする。
2. 適当な箇所へZipファイルを展開する。(ここの展開場所を環境変数PATHに登録するので、一時的なディレクトリには展開しないほうがいい)

## 環境変数の登録
terminalを起動し環境変数を登録していく。

- JAVA_HOMEの環境変数にEclipseのjava8パスを追加する。
```console
echo export JAVA_HOME='/Applications/Eclipse_2024-03.app/Contents/java/8' >>  ~/.zshrc
```

- PATHの環境変数にEclipseのjava8パスを追加する。
```console
echo export PATH='$PATH:$JAVA_HOME' >>  ~/.zshrc
```

- PATHの環境変数にmavenのパスを追加する。xxxxの部分はmarven3のzipファイルを展開したフォルダパスを指定してください。
```console
echo export PATH='$PATH:/XXXXXX/apache-maven-3.9.7/bin' >>  ~/.zshrc
```

- .zshrcを再読み込みする
```console
source ~/.zshrc
```

- パスが通っているかを確認する
```console
javac -version

mvn --help
```

## mallproのソースコード配置
1. SharePointからソースコードの[zipファイル](https://east1997.sharepoint.com/sites/JRPJ/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FJRPJ%2FShared%20Documents%2FBacklog%5FPJ%5FEXT%5FJREAST%E7%94%A8%E5%85%B1%E6%9C%89%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%2F91%5F%E5%8F%82%E8%80%83%E8%B3%87%E6%96%99%2F20240129%5Fmallpro%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%2Fmallpro%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%89&viewid=6b981fc6%2Ddda1%2D4d7a%2Dbad1%2D1eb9a0f46269)をダウンロードする。
2. 適当な場所へzipファイルを展開する。
3. Eclipseを起動し、[ファイル] > [ファイル・システムからプロジェクトを開く]よりソースコードをインポートする<br>（インポート後にアラートが表示されますが、「OK」もしくは「はい」で閉じて問題ありません。）
4. [ウインド] > [ビューの表示] > [進行状況]より進行状況のウィンドウを表示する
5. ビルドの進行状況が表示されていることを確認する
6. ビルドが終了したら`~/.m2/repository`ディレクトリが作成されていることを確認する<br>（隠しファイルとしてユーザーディレクトリに生成される）

## mavenライブラリ配備
1.  SharePointから[m2.zip](https://east1997.sharepoint.com/sites/JRPJ/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FJRPJ%2FShared%20Documents%2FBacklog%5FPJ%5FEXT%5FJREAST%E7%94%A8%E5%85%B1%E6%9C%89%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%2F91%5F%E5%8F%82%E8%80%83%E8%B3%87%E6%96%99%2F20240129%5Fmallpro%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%2Fmaven%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB&viewid=6b981fc6%2Ddda1%2D4d7a%2Dbad1%2D1eb9a0f46269)をダウンロードする。
2. 適当な場所へzipファイルを展開する。<br>（隠しファイルになる）
3. mallproのソースコード配置で生成された`~/.m2/repository`ディレクトリを削除する。<br>※Eclipse起動中の場合は閉じてから削除を実施。
4. ダウンロードしたm2フォルダの中のrepositoryフォルダを、`~/.m2`配下にコピー/移動で配備する。
5. Eclipseを起動して、プロジェクトを全選択し右クリック>[Maven] > [プロジェクトの更新]を選択、OKを押下する。
6. [ウィンドウ] > [ビューの表示] > [問題]より、問題ウィンドウを表示してエラー内容を確認する。<br>下記のようなエラーが計7件発生するが、売上管理機能の実行では問題ない。
```console
- GWRS0000DetailControllerを解決できません
- Lombok annotation handler class lombok.eclipse.handlers.HandleData failed - エラー・ログを参照。
- Unable to make field private final java.util.Comparator java.util.TreeMap　~
- 構文エラーがあります。
```

## サーバ設定（Tomcat9）
1. [ウィンドウ] > [ビューの表示] > [サーバー]から、サーバーウィンドウを表示。
2. サーバーウィンドウで右クリック>[新規] > [サーバー]を選択。
3. [Apache] > [Tomcat v9.0 サーバー]を選択して、[追加]をクリック。
4. `Java11`が選択されているので、`Java8`を選択して[完了]を押下する。
5. サーバー名を「Tomcat9_Java8」に変更して[次へ]を押下する。
6. 使用可能から`deploy(ROOT)`を選択して、構成済みに移動して[完了]を押下する。
7. サーバーウィンドウ内に`deploy(ROOT)`が割り当てられたサーバーが存在することを確認する。

## (有料アカウント保持者必須)Docker Desktopのインストール
有料DockerHubアカウント保持者は下記手順にてdockerを使用した構築が実施できる。

- postgresqlのインストール
- Redisインストール

有料DockerHubアカウントを保持しており、Dockerをインストールしていない場合は下記手順で環境構築を実施する。

1. [ここから](https://docs.docker.com/desktop/install/windows-install/)Docker Desktopのインストーラーをダウンロードする。
2. インストーラーを起動し、[OK]を押下する。
3. インストールが完了したらPCを再起動をする。
4. 再起動すると利用規約ウィンドウが表示されるので[Accept]を選択。<br>※起動しなかった場合は検索して実行
5. [Use recommended settings]を選択し[Finish]を選択。
6. [Sign in]を選択すると、ブラウザが起動するのでアカウントログインを実施する。


## postgresql10のインストール
### 有料DockerHubアカウント保持者の場合

1. 下記コマンドよりdockerイメージを取得する。
```console
docker pull postgres:10.9
```

2. 下記コマンドよりdockerコンテナを構築し起動する。
```console
docker run --name postgresql-container -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_DB=postgres -p 5432:5432 -d postgres:10.9
```

3. 下記コマンドよりコンテナの起動状態を確認する。
```console
docker ps
```

### 有料DockerHubアカウントがない場合（macでの動作未確認）
※現在postgresql10のインストーラーが選択できない

1. [ここから](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)postgresql10のインストーラーをダウンロードする。
2. インストーラーを起動し[Next]を押下する。
3. 任意のディレクトリを指定する(デフォルト値推奨)。
4. 全ての項目にチェックをして[Next]を押下する。
5. 任意のディレクトリを指定する(デフォルト値推奨)。
6. passwordに「postgres」を入力する。
7. ポート「5432」を入力後、「Next」を押下する。
8. Cドライブに準ずるディレクトリを選択後、「Next」を押下しインストール開始まで進める。
9. チェックを外して「Finish」を押下する。

## Redisのインストール
### 有料DockerHubアカウント保持者の場合

1. 下記コマンドを実行。
```console
docker run --name redis-container -p 6379:6379 -d redis:5.0.4
```

2. [アクセスを許可する]を選択。

3. 下記コマンドよりコンテナの起動状態を確認する。
```console
docker ps
```

### 有料DockerHubアカウントがない場合（macでの動作未確認）

## Mallproサンプルデータ取込
1.  SharePointから[20230127_mallpro.dump](https://east1997.sharepoint.com/:u:/r/sites/JRPJ/Shared%20Documents/Backlog_PJ_EXT_JREAST%E7%94%A8%E5%85%B1%E6%9C%89%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80/91_%E5%8F%82%E8%80%83%E8%B3%87%E6%96%99/20240129_mallpro%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89/mallpro%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%89/dump/20230127_mallpro.dump?csf=1&web=1&e=FcNSV5)と[20230131_dev07_co00001.dump](https://east1997.sharepoint.com/sites/JRPJ/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FJRPJ%2FShared%20Documents%2FBacklog%5FPJ%5FEXT%5FJREAST%E7%94%A8%E5%85%B1%E6%9C%89%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%2F91%5F%E5%8F%82%E8%80%83%E8%B3%87%E6%96%99%2F20240129%5Fmallpro%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%2Fmallpro%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%89%2Fdump%2F20230131%5Fdev07%5Fco00001%2Edump&parent=%2Fsites%2FJRPJ%2FShared%20Documents%2FBacklog%5FPJ%5FEXT%5FJREAST%E7%94%A8%E5%85%B1%E6%9C%89%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%2F91%5F%E5%8F%82%E8%80%83%E8%B3%87%E6%96%99%2F20240129%5Fmallpro%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%2Fmallpro%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%89%2Fdump)をダウンロードし、任意の場所に保存する。

2. 下記コマンドを実行する。
```console
docker exec -it postgresql-container bash
```

3. 下記コマンドを実行してDBを作成する。<br>パスワード入力が求めれられるので「postgres」（postgresqlインストール時に指定したパスワード）を入力する。
```console
createdb -U postgres -p 5432 -E UTF8 -T template0 co00001
```

※エラーが表示され既にDBが存在する場合はDBを削除します。<br>（エラーが表示されなかった場合はスキップで問題なし。）
```console
dropdb -U postgres -h localhost -p 5432 co00001
```
削除コマンド実行後、再度DB作成コマンドを実行。

4. 下記コマンドでDBが作成されたことを確認する。
- 接続コマンド
```console
psql -U postgres -h localhost -p 5432
```

- DB確認コマンド
```console
\l
```

- 切断コマンド
```console
\q
```

5. 下記コマンドでダミーの暗号化データ型を作成する。<br>データ型の作成はDB「co00001」で実施する。
- 接続コマンド
```console
psql -U postgres -h localhost -p 5432
```

- DB接続コマンド
```console
\c co00001
```

- 暗号化データ型作成コマンド
```console
CREATE DOMAIN encrypt_text AS text;
CREATE DOMAIN encrypt_bytea AS bytea;
```

- 切断コマンド
```console
\q
```

6. 下記コマンドでDBのマイグレーションで使用するユーザーを作成する。
```console
psql -U postgres -p 5432 -c "create user \"east000\" with password 'es-east000-ad1';"
psql -U postgres -p 5432 -c "create user \"east001\" with password 'es-east001-ad1';"
```

7. 下記コマンドでdumpデータをコンテナに移動させる。
- コンテナ外に出る
```console
exit
```

- コンテナ内にdumpファイルをコピー
```console
docker cp 自分のファイルパス/20230127_mallpro.dump postgresql-container:/tmp
docker cp 自分のファイルパス/20230131_dev07_co00001.dump postgresql-container:/tmp
```

- コンテナに入りdumpファイルがコピーされているか確認
```console
docker exec -it postgresql-container bash
```

```console
cd tmp
```

```console
ls
```

```console
exit
```

8. 下記コマンドでローカルにDBをリストアする
- データ流し込みコマンド
```console
psql -U postgres -h localhost -p 5432 <自分のファイルパス/20230127_mallpro.dump
```

```console
psql -U postgres -h localhost -p 5432 -e co00001 <自分のファイルパス/20230131_dev07_co00001.dump
```

※上記でエラーが出る場合は下記コマンドを実行
```console
psql -U postgres -h localhost -p 5432 </tmp/20230127_mallpro.dump
```

```console
psql -U postgres -h localhost -p 5432 -e co00001 </tmp/20230131_dev07_co00001.dump
```

9. テーブルが作成されているか確認
- 接続コマンド
```console
psql -U postgres -h localhost -p 5432
```

- DB接続コマンド
```console
\c mallpro
```

- テーブル確認コマンド
```console
\dt
```

- DB接続コマンド
```console
\c co00001
```

- テーブル確認コマンド
```console
\dt
```

- 切断コマンド
```console
\q
```

mallproテーブル一覧 -> mallproの共通機能に使用されるDB。SC単位のDB接続情報が保存される。
co00001テーブル一覧 -> ディベロッパーにつき1つ作成されるDB。各テナントのトランザクションデータや設定値が保存される。

## DBマイグレーション
###  dbmigrate.mallproの実行
1. [パッケージエクスプローラー]より[dbmigrateプロジェクト]を右クリック > [実行] > [実行の構成]を選択。
2. 左側の一覧から[Mavenビルド] > [dbmigrate.mallpro]を選択。
3. パラメーターの[追加]を選択し、名前に「password」、値に「postgres」を入力し「OK」を押下する。
4. [実行]を押下し、コンソールにBUILD SUCCESSが表示されれば完了。
5. [パッケージエクスプローラー]より[dbmigrateプロジェクト]を右クリック > [実行] > [実行の構成]を選択。

### dbmigrate.sc-shareの実行
[実行の構成]で左側の一覧から[Mavenビルド] > [dbmigrate.mallpro]を選択、以下同様。

### dbmigrate.east000の実行
[実行の構成]で左側の一覧から[Mavenビルド] > [dbmigrate.east000]を選択、追加はせずに実行。

### dbmigrate.east001の実行
[実行の構成]で左側の一覧から[Mavenビルド] > [dbmigrate.east001]を選択、追加はせずに実行。

### マイグレーションの作成
1. mallproフォルダを右クリック > [新規] > [ファイル] を選択。
2. Flywayの命名規則に従ってファイル名を入力。
- 先頭にVを付けてバージョンを指定します。バージョンの数値は実行順になるので任意の値を指定します。
- __(2重アンダースコア)でバージョンの記述を区切り、説明文を入力します。
例）V99__Create_person_table.sql
3. mallproフォルダ内にsqlファイルが作成されていることを確認する。
4. 作成したsqlファイルに下記テーブル作成コマンドを記載する。

```console
CREATE TABLE person (
id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
email VARCHAR(150),
created_at TIMESTAMP WITHOUT TIME ZONE DEFAULT CURRENT_TIMESTAMP
);
```

5. dbmigrateフォルダを右クリック > [実行] > [実行の構成]を選択し、左側の一覧から[dbmigrate.mallpro]を選択して実行。
6. マイグレーションにより`personテーブル`が作成されていることを確認する。
7. `public.shema_versionテーブル`に作成したバージョンのデータが保存されていることを確認する。

## MallPro実行
1. アプリケーション割り当て済みのサーバー（Tomcat9_Java8）をダブルクリックする。
2. [起動構成を開く]を選択。
3. [引数タブ]を選択してTomcatのVM引数に「-Xss20m」を追記し、[適用]を押下し[OK]を押下して閉じる。<br>
※VM引数を追加する際は、前の引数の後に”半角スペース”が必要。
4. さらに[タイムアウト]の開始時間を「120」に変更。その後`Ctrl＋S`で変更を保存。<br>
※デフォルト値は45に設定されているが、mallproの起動には時間がかかるため余裕を持った時間を設定。
5. [ウィンドウ] > [ビューの表示] > [コンソール] から[コンソールウィンドウ]を表示
6. アプリケーション割り当て済みのサーバーを右クリック > [開始] よりサーバーを起動
7. 警告が表示される場合は、[アクセスを許可する]を押下する。
8. コンソールにサーバー起動と表示され、[こちら](http://localhost:8080/ROOT/login)へアクセスしてログインできれば完了。<br>
ユーザーID：000system000<br>
パスワード：Password1<br>
※「警告: web.xmlのabsolute-orderingタグで間違ったフラグメント名[fragment01]を使用しました！」というエラーが出る場合は、[プロジェクト] > [Mavenプロジェクトの更新]を行う
