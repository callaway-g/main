# ffuf

webファジングツール

## コマンドサンプル

動作中`Enter`でインタラクティブモードでオプションを受付
`restart`で再開

* 普通

``` shell
    #出力をカラー化
    ffuf -c -u http://victim.com/FUZZ  -w wordlists.txt
```

* 仮想ホストの検出

``` shell
    ffuf -c -u http://victim.com  -w wordlists.txt -H "Host: FUZZ.victim.com"
```

* オプション付き

``` shell
    # 403非表示でphpファイルを検出
    ffuf -u "http:/victim.com/FUZZ" -w /your/wordlist.txt -e .php -fc 403
```

* LFI

``` shell
    # ローカルファイルインクルージョンチェック
    ffuf -u "http:/victim.com/upload.php?file=FUZZ" -w /your/wordlist.txt 
```
