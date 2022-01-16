## Почему не работает fetch отправленный из новой вкладки браузера?

Потому что ответ сервера должен включать http заголовок `Access-Control-Allow-Origin: * `  если его нету от запрос на https адреса не пройдет по CORS

**Что делать?** 
Поднимать локальный сервер с https или прокси сервер, который будет добавлять нужные заголовки

**Как поднять локальный сервер в VScode?**
Сначала разбираеся с локальным самоподписанным  сертификатом. Гуглить по запросу `How to create a self-signed SSL Certificate for windows`  . Потом добавляем сертификат в настройки VS code Live Server
https://github.com/ritwickdey/vscode-live-server/blob/master/docs/settings.md
настройка `liveServer.settings.https`