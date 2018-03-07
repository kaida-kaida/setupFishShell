# nodeを使えるようにできるまで

node.jsのセットアップには、nodebrewかnvmを使う（fishshellも使うならhomebrewが良い）

## homebrew経由

1.1 homebrewのインストール

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

1.2 homebrewのセッティング

```
brew doctor
```

`Your system is ready to brew`が表示されればOK
エラーないしワーニングが出る時は、メッセージに従って直す

```
brew update
```

`Already up-to-date.`が表示されれば最新の状態になっている。

1.2.1 セッティングができない時
Xcodeのライセンス周りでセッティングできない時がある
コマンドラインには

```
Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo.
```

というメッセージがでてきて、ライセンス認証よろしくと言われる

```
sudo xcrun cc
```

もしくは

```
sudo xcodebuild -license
```

Password入力後、Enter押下でライセンス情報が表示され

```
agree
```

入力でライセンス認証が降りる。

```
sudo xocde-select --install
```

入力で、Xcodeが入る
それでもbrew doctorでワーニング出るようであれば、
App Storeから直接インストールする。

1.3.nodebrewのインストール

```
brew install nodebrew
```

```
nodebrew -v
```

でバージョンが表示されれば正常にインストールされている

```
nodebrew install-binary latest
```

installでもできるが、ビルドされるので時間がかかることがある。
install-binary推奨。
バージョンを変えたい場合は、latestの部分をv5.12.1とかみたいにバージョン指定する

1.3.1.エラーが出てインストールできない時
nodebrewをインストールした直後だと、ディレクトリがないとエラーがでる場合がある。
`Warning: such file or directory`と出た場合、ディレクトリを作る必要がある。

```
mkdir -p ~/.nodebrew/src
```

1.4.インストールされたNode.jsのバージョン確認

```
nodebrew list
```

latestで入れた時に、インストールされたlistを表示すると

```
v7.10.0

current: none
```

となっていればOK。

1.5.Node.jsのバージョンを通す

```
nodebrew use v7.10.0
```

を実行して、もう一度nodebrew listを実行
`current: v7.10.0`と表示されていればOK

1.6.実行パスを通す
node,npmコマンドを実行できるようにパスを通す。

### fishshellを使う場合はここからの設定は必要なし
fishshellではなく、普通のbashの場合は以下の設定をする


```
node -v
```

と入力すると

```
Unknown command 'node'
```

表示されてまだnodeコマンドが通らない。
nodeとnpmコマンドを実行できるようにパスを通す。

```
echo 'export PATH=$PATH:/Users/xxxxx/.nodebrew/current/bin' >> ~/.bashrc

```

xxxxxはホームディレクトリ名

1.6.1.ホームディレクトリ名の確認
ホームディレクトリ名がわからない時は、ターミナルから確認する。
ターミナルのルート（初期起動時）に

```
pwd
```

コマンドを実行すると

```
/Users/xxxxx
```

と表示され、このxxxxxがホームディレクトリ名となる。

1.7.Node.jsのバージョンを確認する
ターミナルを再起動し、作成した.bashrcを実行する

```
source ~/.bashrc
```

これでbashrcに記述したものが実行されてパスが通るようになる。

```
node -v
```

`v7.10.0`が表示されればOK

```
npm -v
```

`v4.2.0`が表示されればOK

1.8. .bash_profileの作成
.bashrcは対話モードの bash を起動する時に毎回実行される。
ターミナルで一度パスを通しても、再度ターミナルを開き直すとパスが通らなくなっている。
ターミナル起動時に.bashrcが実行されるように.bash_profileを作成する。
.bash_profileはログイン時にのみ実行される。

```
vi ~/.bash_profile
```

を実行すると、vi画面が表示される。
起動時に「a」と入力するとINSERTモードに移行し、文字入力できるようになる。

```
~/.bashrc_profile
test -r ~/.bashrc && . ~/.bashrc
```
入力が完了したら「esc」ボタンを押下し、入力モードを解除しコマンド入力モードに移行する。

```
:wq
```

入力で保存される。（:を入力する時はshiftボタンの入力を忘れないように）
wqコマンドの意味は
w : 書き込み
q : 終了

これで、ターミナル起動時からnode,npmコマンドが最初から使えるようになっている。
