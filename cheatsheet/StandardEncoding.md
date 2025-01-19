# Standard Encoding

* Base64

```powershell
    #Encode
    $Bytes = [System.Text.Encoding]::UTF8.GetBytes($Text)
    $EncodedText = [Convert]::ToBase64String($Bytes)
    #Decode
    $EncodedText = 'SGVsbG8sIFdvcmxkIQ=='
    $Bytes = [Convert]::FromBase64String($EncodedText)
    $DecodedText = [System.Text.Encoding]::UTF8.GetString($Bytes)
```
