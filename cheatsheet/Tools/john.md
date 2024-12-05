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
