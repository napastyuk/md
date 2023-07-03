
# Конфиги для test/stage/dev
## Переопредeление домена или поддомена
Запись имеет максимальный приоритет в процессе загрузки, и перебивает даже запись в БД
```
define( 'WP_HOME', 'https://stats2.fabricmedia.ru' );
define( 'WP_SITEURL', 'https://stats2.fabricmedia.ru' );
```

## Отключение теста и включение вывода ошибок
```
define( 'WP_CACHE', false );

define( 'WP_DEBUG', true );     // включение дебаг режима

define( 'WP_DEBUG_LOG', true ); // true - логирование ошибок в файл /wp-content/debug.log

define( 'WP_DEBUG_DISPLAY', true ); // false - отключает показ ошибок на экране

define( 'SCRIPT_DEBUG', true ); // используем неминифицированные версии JS и CSS файлов движка

define( 'WP_ENVIRONMENT_TYPE', 'development' );
```

## Разные конфиги для прода и дева
```
if ( file_exists( dirname( __FILE__ ) . '/local-config.php' ) ) {
 include( dirname( __FILE__ ) . '/local-config.php' );
 	define( 'WP_LOCAL_DEV', true ); 
}
else {
	define( 'DB_NAME',     'production_db'       );
 	define( 'DB_USER',     'production_user'     );
 	define( 'DB_PASSWORD', 'production_password' );
 	define( 'DB_HOST',     'production_db_host'  );
}
```

# Конфиги для прода
```
define( 'WP_ENVIRONMENT_TYPE', 'production ' ); 

define('DISALLOW_FILE_EDIT', true); //отключают возможность править через файлы админку

define('DISALLOW_FILE_MODS', true); //запрет на мобификацию исходников. было бы неплохо, но надо проверить коректную работу плагинов
```

## Запрет на обновление WP
```
define( 'AUTOMATIC_UPDATER_DISABLED', true );
add_filter('pre_site_transient_update_core',create_function('$a', "return null;"));
wp_clear_scheduled_hook('wp_version_check');
```

## Запрет на обновление плагинов
```
remove_action( 'load-update-core.php', 'wp_update_plugins' );
add_filter( 'pre_site_transient_update_plugins', create_function( '$a', "return null;" ) );
wp_clear_scheduled_hook( 'wp_update_plugins' );
```

## Запрет на обновление плагинов
```
remove_action( 'load-update-core.php', 'wp_update_plugins' );
add_filter( 'pre_site_transient_update_plugins', create_function( '$a', "return null;" ) );
wp_clear_scheduled_hook( 'wp_update_plugins' );
```

## Запрет на обновление темы
```
remove_action('load-update-core.php','wp_update_themes');
add_filter('pre_site_transient_update_themes',create_function('$a', "return null;"));
wp_clear_scheduled_hook('wp_update_themes');
```

## Ограничение количества ревизий постов.
```
define( 'AUTOMATIC_UPDATER_DISABLED', 1 ); //false - отключить совсем
```

## Общие рекомендации для прода
Исключаем из гита wp-content/uploads. Во первых что бы не грузить в гит кучу дублирующих картинок, во вторых так пользователи могут спокойно продолжать писать контент, а программисты в это время делать выкатки.

#wordpress #devops 