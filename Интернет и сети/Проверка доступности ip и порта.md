#сети #devops 

Из linux/wsl
```bash
telnet 192.168.11.173 5432
```

Из windows, если включен системный компонент telnet
```cmd
telnet 192.168.11.173 5432 
```

Если выключен можно проверить через PowerShell
```PowerShell
TNC 192.168.11.173 -Port 5432
```
Остальные параметры [в доке](https://learn.microsoft.com/en-us/powershell/module/nettcpip/test-netconnection?view=windowsserver2022-ps)
