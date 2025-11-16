# 卒業論文執筆でGitHubを活用する
卒業論文を複数でバックアップする際に、GitHubとGitHub Actionsを活用する

## 方法
`rclone`という、クラウドストレージを操作できるコマンドラインツールをGitHub上で使用する。これにより、ローカルでpushした際にGitHubとクラウドストレージへ自動でバックアップが取れるようになる。また、pullすれば最新の書きかけファイルを召喚できるので、いろんな環境で論文を書くのが楽になる。

## 手順
### 1. ローカルでTeX環境を作る
今回はWindows PCで設定をするので、[ここ](https://www.tug.org/texlive/windows.html#install)からインストールした。かなり時間がかかるので注意。

### 2. VSCodeのインストール
省略。
拡張機能の"LaTeX Workshop"があると楽なので、入れておくといい。

### 3. リポジトリを作成
GitHubの自分のページから新しいリポジトリを作成。
ローカルでクローン。

PDFなどは追跡すると重くなるので`.gitignore`に入れておく
私が書いた内容
```
*.aux
*.log
*.out
*.toc
*.bbl
*.blg
*.bcf
*.run.xml
*.synctex.gz
*.fdb_latexmk
*.fls
*.pdf
```

### 4. GitHub Actionsのワークフローを作成
作成したリポジトリに`.github\workflow\backup.yml`を作成

### 5. OneDriveをrcloneに接続する
インストールは[この記事](https://qiita.com/mochinoki/items/c0809d75ba9228cb54b6)を参考にした。

<details>
    <summary>個人的に行ったこと<summary>

    `C:\rclone`を作成し、そこに.exeファイルを移動
    環境変数にパスを追加
</details>

Windowsでは以下のコマンドで設定を開始。
```
.\rclone.exe config
```
対話に従って進む。
作成後、`rclone.conf`というものが作成されるので、その全文をコピー。
場所は以下のコマンドで調べられる
```
rclone config file
```

### 6. GitHub Secretsの設定
`rclone.conf`を、作成したリモートリポジトリのSettings - Secretsに追加
全文貼り付けの際に、どうしても改行が入ってしまうせいか、エラーが出た。
`rclone.conf`をBASE64にして、Actionsに復号の処理を挟むことで解決！