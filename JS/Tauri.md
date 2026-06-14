```
npm create tauri-app@latest
```
только так. Установка как npm пакета у меня не завелась

Как оказалось позже проблема в версии alloc-stdlib
```
alloc-stdlib v0.2.3 (новая) → alloc-no-stdlib v3.0.0
brotli (любая версия)       → alloc-no-stdlib v2.0.4
                                          ↑ конфликт
```
Лечится командой 
```
cargo update -p alloc-stdlib --precise 0.2.2
```
