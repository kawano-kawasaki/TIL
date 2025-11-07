# SSH

## SSHとは？
- Secure Shell
- ネットワークを介して他コンピュータへログインするためのプロトコル
- アプリケーション層

### 他プロトコルとの比較
- telnet
  - telnetは暗号化せず送信するが、SSHは通信内容を暗号化

## 接続コマンド
~~~
ssh [username]@[hostname]
~~~

### ポート指定 -p
~~~
ssh [username]@[ip] -p [portnum]
~~~

## 鍵の生成
ssh-keygenコマンドで秘密鍵と公開鍵を作る
~~~
ssh-keygen
~~~

### アルゴリズムの指定`-t`
~~~
ssh-keygen -t [algorithm]
~~~
アルゴリズムとして利用できるのは以下
- RSA(デフォルト)
  - `RSA1`のようにバージョンを指定することも可能
- ECDSA(?)
- ED25519

### 鍵の長さを指定`-b`
~~~
ssh-keygen -b [length]
~~~
RSAを選択すると、デフォルトで2048bit。最大は4096bit

### 名前の指定`-f`
~~~
ssh-keygen -f [filename]
~~~
- 個人的に、昔作った鍵のパスフレーズを忘れたときによく使う
パスフレーズの変更は以下
~~~
ssh-keygen -f [filename] -p
~~~
古いパスフレーズが必要なので、忘れた場合は新しく作り直さないといけない？

### コメント`-C`
~~~
ssh-keygen -C "[comment]"
~~~
- 公開鍵の末尾に付与される
- オプションを使用しない場合は、ssh-keygenを実行した環境でのユーザ名とホスト名が書かれる

## SSH鍵の登録方法
~~~
ssh-copy-id -i [path/to/key.pub] [username]@[hostname]
~~~

## 参考文献
- [SSH接続とは？仕組みやSSHサーバーの設定、認証方法をわかりやすく解説](https://www.value-domain.com/media/ssh/)
- [SSHとは](https://www.ntt.com/bizon/glossary/e-s/ssh.html)
- [【Linux】sshコマンドで別のサーバにSSH接続する](https://qiita.com/Aichi_Lover/items/6d2b04a851ec7e435edf)
- [ssh-keygenについて](https://qiita.com/pyon_kiti_jp/items/aa5b01fbd1132dc99abf)
- [SSH鍵の作成方法と -t -C オプションのすすめ](https://qiita.com/ryemug1/items/bacf6e6583656f3cf0d1)
- [【SSH】ssh-keygenでファイル名を指定して作成（などアレコレ）](https://qiita.com/c_tomioka/items/379a9288d44634ca1daa)
- [sshの秘密鍵パスフレーズの確認と変更](https://qiita.com/syukan723/items/e654953c89aab6f847a4)