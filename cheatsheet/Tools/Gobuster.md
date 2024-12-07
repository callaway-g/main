# Gobuster
  
WebサイトのURLやDNSサブドメイン名を洗い出すツール

## コマンド例

``` bash
   gobuster dir -u WebアプリのIP -w <wordlists> -s '200,204,301,302,307,403,500' -b '' -e

   # ディレクトリブルートフォース
   gobuster dir -u "http://<target_url>" -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt 

   # 拡張子指定でのブルートフォース
   gobuster dir -u "http://<target_url>" -w 
   /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x .php
```

## モード

1. dir: ディレクトリを列挙するモード
2. dns: DNSのサブドメインを列挙するモード
3. vhost: WebサーバのVirtualHostを列挙するモード

## オプション

1. -u: 探索を行う起点のURLを指定する。指定したURLをサブディレクトリを探索させることができる。
2. -w: ワードリスト(wordlist)の指定、ここで指定したファイルにある文字列を-uで指定したURLに一行ずつくっつけて探索
3. -s: どのステータスコードが返ってきたらアクセスしたURLが存在すると判定するかを指定できる。
4. -b: どのステータスコードが返ってきたらアクセスしたURLが存在しないと判定するかを指定できる。(-sを指定した場合は-b ''を指定する必要がある)
5. -x: 検索するファイル拡張子(dirモードのみ有効) php、txt、htmlファイルを検索したい場合のコマンド例:-x 'php,txt,html'
6. -e: 見つかったURLの表示に-uで指定したベースのURLを含めて表示する(expand)
