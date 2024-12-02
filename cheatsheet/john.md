# john the ripper

``` shell
    # passwdとshadowをハッシュ化
    sudo unshadow passwod shadow > hash.txt
    john --format=crypt hash.txt
    #一度確認したものは
    cat /home/kali/.john/john/pot
```
