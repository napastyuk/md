Браузер "закешировал" https. При попытке открыть через http, совершается редирект на https. Это происходит из-за HSTS.

### Как заставить браузер использовать HTTP вместо HTTPS?
Очистка кэша HSTS (HTTP Strict Transport Security). Способ исправляет проблему на отдельно взятом браузере. Почистить кэш своим пользователем не получится.

Требуется зайти на специальную страницу браузера:

Для Google Chrome, Opera: chrome://net-internals/#hsts. «Delete domain security policies», ввести домен и нажать «Delete domain»
Для Яндекс.Браузер: about:net-internals#hsts
Для Mozilla Firefox: about:permissions. «Forget About This Site»
Для Safari: Удалить файл ~/Library/Cookies/HSTS.plist

После этого сайт должен открываться через http://

#anykey #сети 