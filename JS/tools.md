### Русский lorem api
https://fish-text.ru/get?type=paragraph&number=5&format=html

дока
https://fish-text.ru/api


### Ссылки для тестирования AMP/Turbo
Проверка AMP(в режиме эмуляции мобилки)
https://www.google.com/amp/s/nevnov.ru/amp/{slug}
например
https://www.google.com/amp/s/nevnov.ru/amp/822193-nevskie-novosti-pokazyvayut-prolet-aviacii-nad-peterburgom-vo-vremya-trenirovki-ko-dnyu-vmf


Проверка Turbo(в режиме эмуляции мобилки)
https://yandex.ru/turbo/s/nevnov.ru/{slug}
например
https://yandex.ru/turbo/s/nevnov.ru/822193-nevskie-novosti-pokazyvayut-prolet-aviacii-nad-peterburgom-vo-vremya-trenirovki-ko-dnyu-vmf


### Сброс https кеша
Браузер "закешировал" https. При попытке открыть через http, совершается редирект на https. Это происходит из-за HSTS.

Как заставить браузер использовать HTTP вместо HTTPS?
Очистка кэша HSTS (HTTP Strict Transport Security). Способ исправляет проблему на отдельно взятом браузере. Почистить кэш своим пользователем не получится.

Требуется зайти на специальную страницу браузера:

Для Google Chrome, Opera: chrome://net-internals/#hsts. «Delete domain security policies», ввести домен и нажать «Delete domain»
Для Яндекс.Браузер: about:net-internals#hsts
Для Mozilla Firefox: about:permissions. «Forget About This Site»
Для Safari: Удалить файл ~/Library/Cookies/HSTS.plist
После выполнненый действий сайт должен открываться через http://
