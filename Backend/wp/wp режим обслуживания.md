Добавить в `functions.php`
```php
function wp_maintenance_mode(){
    if(!current_user_can('edit_themes') || !is_user_logged_in()){
        wp_die('<h1 style="color:red">Website under Maintenance</h1><br />We are performing scheduled maintenance. We will be back on-line shortly!');
    }
}
add_action('get_header', 'wp_maintenance_mode');
```

#wordpress  #php 