# john the ripper

## ハッシュファイルからのクラック

``` shell
    # passwdとshadowをハッシュ化
    sudo unshadow passwod shadow > hash.txt
    john --format=crypt hash.txt
    #一度確認したものは
    cat /home/kali/.john/john/pot
```

## zipのパスワードクラック
  
``` shell
    zip2john <zip_file> > hash.txt
    john hash.txt
```

- zipパスワードクラックのサンプル

``` shell
    # zip password crack tool
    zip2john story.zip
    # これを実行した結果に PKZIP が表示されていた
    zip2john story.zip | awk -F: '{print $2}' > story.hash
    # PKZIPのハッシュタイプのコードを取得
    hashcat -h | grep PKZIP
    # クラック　失敗
    hashcat -m 17200 -a 0 story.hash wordlist
    # ルールファイルを使用してワードリストを変更する
    # password の文字列を入力してを passwordファイルを作成
    echo password > password
    # 作成したpasswordファイルを使用してルールファイルを変更する
    # --stdoutで指定したワードリストを使用する
    hashcat -a 0 --stdout password --rules /usr/share/hashcat/rules/best64.rule
    # 再度クラック 成功する
    hashcat -m 17200 -a 0 --rules /usr/share/hashcat/rules/best64.rule story.hash wordlist
    # 確認
    hashcat -m 17200 --show story.hash
```