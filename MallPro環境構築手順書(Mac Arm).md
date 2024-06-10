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
3. Eclipseを起動し、[ファイル] > [ファイル・システムからプロジェクトを開く]よりソースコードをインポートする
4. [ウインド] > [ビューの表示] > [進行状況]より進行状況のウィンドウを表示する
5. ビルドの進行状況が表示されていることを確認する
6. ビルドが終了したら`~/.m2/repository`ディレクトリが作成されていることを確認する
