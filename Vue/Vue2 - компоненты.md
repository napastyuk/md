# Регистрация компонентов

## Глобальная регистрация компонентов

Сначала регистрируются компоненты, потом инстанс самого приложения.

```html
<div id="app">
  <component-a></component-a>
</div>

<script>
  Vue.component("component-a", { template: "<p>Компонент А</p>" });

  new Vue({ el: "#app" });
</script>
```

тоже самое в более расширенном варианте

```html
<div id="app">
  <button-counter></button-counter>
  {{ message }}
</div>

<script>
  // Пример глобальной регистрации компонентов.
  Vue.component("button-counter", {
    data: function () {
      return {
        count: 0,
      };
    },
    template:
      '<button v-on:click="count++">Счётчик кликов - {{ count }}</button>',
  });

  new Vue({
    el: "#app",
    // свойство data у компонентов должно быть функцией, чтобы обеспечить независимую работу разных экземпляров одного компонента на странице.
    data: {
      message: "Привет, Vue!",
    },
  });
</script>
```

На странице может быть несколько экземпляров vue (new Vue) , и глобальные компоненты смогут использоватся в любом из них.
Но при таком варианте код компонентов всегда будет попадать в сборку, вне зависимости от использования в шаблоне.

## Локальная регистрация компонентов
удобна в том числе тем, что компоненты можно выносить в отдельные файлы, но

```html
<div id="app">
  <component-a></component-a>
</div>

<script>
  var ComponentA = { template: "<p>Компонент A</p>" };

  new Vue({
    el: "#app",
    components: {
      "component-a": ComponentA,
    },
  });
</script>
```

локально зарегистрированные компоненты не будут доступны в дочерних компонентах. Для доступности в дочерних компонентах
их нужно зарегистрировать в родительском

```js
var ComponentA = { /* ... */ }
//import ComponentA from './ComponentA.vue' в случае сборщика

var ComponentB = {
  components: {
    "component-a": ComponentA,
  },
  // ...
};
```


#vue #vue2