```PowerShell
Get-NetTCPConnection | Where-Object State -eq 'Established' | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State | Format-Table -AutoSize
```

Что  делает команда:
- Показывает только **активные соединения** (те, по которым сейчас идет передача данных).
- Игнорирует системные "спящие" порты.
- Выводит: LocalAddress LocalPort RemoteAddress RemotePort State

После выполнения команды посмотрите на колонку **`LocalAddress`** (Ваш адрес):
1. Если там `10.*.*.*` — это **VPN**. _Пример:_ `10.*.*.* : 52257 -> 10.*.*.* : 443`  - работа во внутреннем портале через VPN
2. Если там `192.168.0.*` — это **Wi-Fi (Интернет)**. _Пример:_ `192.168.0.198 : 49408 -> 98.66.133.186 : 443` - открыт сайт в браузере или синхронизация с облаком.