# fishshellのインストール

## fishshellのインストール

```
$ brew install fish
$ fish
fish, version 2.5.0
```

バージョンが出たらインストール完了

## デフォルトのターミナルをfishshellに変更する

```
$ which fish
/usr/local/bin/fish
$ chsh -s /usr/local/bin/fish
```

ターミナルを開き直すと、fishになっている。

### chshできない時
権限が原因でchshできない時は

```
chsh: /usr/local/bin/fish: non-standard shell
```


と怒られる。
shellsにfishのパスを書き加えることで通るようになる。

```
sudo vi /etc/shells
```

ファイルの末尾に

```
/usr/local/bin/fish
```

と入力して保存して再度chshコマンドを実行。
何もエラーがでなければOK。

## fishshellのセットアップ

### fishermanのインストール
fish用のパッケージマネージャー。

```
$ curl -Lo ~/.config/fish/functions/fisher.fish --create-dirs git.io/fisherman
$ fisher -v
fisherman version 2.12.0 ~/.config/fish/functions/fisher.fish
```

インストール後、下記コマンド実行

```
fish_update_completions
```

色々なオートコンプリートを追加するコマンドを実行しておく

### プラグインをセットアップ
インストールしたプラグインはfishfileに記述される

```
$ vi ~/.config/fish/fishfile
```

fishfileの中にインストールしたいプラグインを記述

```
# ~/.config/fish/fishfile

oh-my-fish/theme-agnoster
fisherman/await
oh-my-fish/plugin-extract
oh-my-fish/plugin-balias
fisherman/fzf
fisherman/get
fisherman/getopts
fisherman/imgcat
fisherman/last_job_id
fisherman/spin
fisherman/z
```

`agnoster` : カラーテーマ
`extract` : どんなファイル形式でも解答できる
`getops` : shell上からスクリプト実行をサポート（引数を与えることができる）
`spin` : 長いロードを挟む時にグルグル回るアイコンを表示する
`z` : フォルダ間を移動する（cd ../../../しなくても直接フォルダ名指定で移動できる）
`fzf` : ファイル検索や実行コマンド検索(先にbrew install fzf必須)

### プラグインのインストール
fishfileに記述したプラグインを実行するためにはコマンドを打つ必要がある。
下記コマンドを実行

```
fisher
```

fishfileに記述しているものをインストールする

3.configの設定
fishshellのコンフィグを設定する

```
vi ~/.config/fish/config.fish
```

config.fishがコンフィグファイルになり、fishshell起動時に読み込まれる。
path,aliasはここに記述する。

```
# ~/.config/fish/config.fish

# Node.js
set -x PATH $HOME/.nodebrew/node/v9.5.0/bin $PATH

# AWS-CLI
set -x PATH $HOME/Library/Python/2.7/bin $PATH

# Alias
## global
alias rm='rmtrash'

# git
alias g='git'
alias gb='git branch'
alias gd='git diff'
alias go='git checkout'
alias gob='git checkout -b'
alias ga='git add'
alias gc='git commit'
alias gcm='git commit -m'
alias gpu='git push -u origin'
alias gpf='git push --force-with-lease'
alias gp='git push'
alias gpick='git cherry-pick'
alias gs='git status'
alias gl='git log'
alias gr='git reset'

source {$HOME}/.iterm2_shell_integration.fish

# functions
function cd
  builtin cd $argv
  ls -a
end
```

fishshellのパスは
`set -x PATH [ルーティングパス] $PATH`
このようにしてパスを通していく。

#### 便利なコマンド
- fish_config
ブラウザからfishshellの見た目をカスタマイズできる（colorsはなぜか効かない・・・）
ここで設定したものは ~/.config/fish/fishd.****** に保存される


## テーマの変更
元のbashでは心許ないので、iTerm2に変更する。
先ずは公式サイトからiTerm2をインストールしてくる。

`http://iterm2.com/`

```
$ fisher install omf/theme-bobthefish
$ mkdir powerline
$ cd powerline
$ git clone git@github.com:powerline/fonts.git
$ cd fonts
$ ./install.sh
```
shファイルを実行すること
で`D2Codling for Powerline`フォントがインストールされる。

後はこれをiTerm2のpreferenceから設定する
カラーテーマは`solarized dark`にする。
