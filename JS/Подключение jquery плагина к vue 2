# Подкдлючение jquery плагина к vue
Подключаем jquery
`npm i jquery`
потом в простом случае
`import jQuery from 'jquery' `
иногда нужно добавить это
`window.$ = window.jQuery = jQuery` 
иногда возможны случаи, что jquery не успеет инициализирватся
в таких случая иногда помогает обёртка
`$(document).ready(function () { /*...*/ });`
в особо тяжелых случаях нужно включать jquery на уровне webpack на весь проект
через https://webpack.js.org/plugins/provide-plugin/
```js
const webpack = require("webpack");
module.exports = {
  configureWebpack: {
    plugins: [
      new webpack.ProvidePlugin({
        $: 'jquery',
        jquery: 'jquery',
        'window.jQuery': 'jquery',
        jQuery: 'jquery'
      }),
    ],
  },
}
```
если не заработало, дописываем в package.json
```js
"env": {
    "node": true,
    "jquery": true,
    "browser": true
}
```

Подключаем плагин
`import 'whateverplugin';`
или если плагин со старой модульной системой
`require("whateverplugin");`

Ипользуем внутри Vue
```js
export default {
  data () {
    return {
      options: [...]
    };
  },
  mounted () {
    var $vm = this; //если нужнен обмен данными сохраняем ссылку на Vue
    $('#plugin-container').whateverplugin({
       // передаем в плагин данные из свойства Vue
       options: this.options
    });
  }
}
```


```
@hook:beforeCreate="console('beforeCreate')"
@hook:created="console('created')"
@hook:beforeMount="console('beforeMount')"
@hook:mounted="console('mounted')"
@hook:beforeUpdate="console('beforeUpdate')"
@hook:updated="console('updated')"
@hook:activated="console('activated')"
@hook:deactivated="console('deactivated')"
@hook:beforeDestroy="console('beforeDestroy')"
@hook:destroyed="console('destroyed')"
@hook:errorCaptured="console('errorCaptured')"
```
