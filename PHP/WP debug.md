Если надо вывести переменную:
```
 echo $my_var; // Только для строчных/приводящихся к строчным

 print_r($my_var); //для сложных структур, отображает вывод в удобном виде

 var_dump($array); //для сложных структур, отображает значения и типы
```

Если надо понять ситуацию глубже , включаем режим дебага. В `wp-config.php` в любое место до строчки `require_once ABSPATH . 'wp-settings.php';`  добавляем

```
define( 'WP_ENVIRONMENT_TYPE', 'development' ); //установка env переменной

define( 'WP_DEBUG', true ); // включение дебаг режима

define( 'WP_DEBUG_LOG', true ); // логирование ошибок в файл /wp-content/debug.log

define( 'WP_DEBUG_DISPLAY', true ); //включает показ ошибок на экране

//нужно очень редко
define( 'SCRIPT_DEBUG', true ); //не минифицировать JS и CSS движка WP
define( 'SAVEQUERIES', true ); //сохраняет SQL запросы в $wpdb->queries
```

После этого самые явные ошибки начнут появлятся сразу на странице, менее явные надо выводить в консоль. 

Если не не показывается вообще ничего можно выводить в файл `wp-content/debug.log` через команды
```
error_log( $value ); // строчных/приводящихся к строчным
error_log( print_r( $value, 1) ); // Любые данные
```

Если страница и админ панель грузится можно воспользоватся более удобными инструментами. Вот комбинация плагинов, которая мне показалась самой удобной и информативной.   
**Debug This**
https://wordpress.org/plugins/debug-this/
удобный вывод всех внутренных WP объектов.

**Query Monitor**
https://wordpress.org/plugins/query-monitor/
стандарный набор для дебаг панели.

**Kint Debugger**
https://wordpress.org/plugins/kint-debugger/
добавляет красивый вывод вложенных структур для обоих предыдущих плагинов.

Если объекты крупные, можно выводить через Kint
```
<?php d( $var ); ?>
```

Или писать в консоль  Query Monitor
```
do_action( 'qm/debug', $var );
```

Документация по Query Monitor https://querymonitor.com/docs/




