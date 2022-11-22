#vue2
# Vue

## Vue CLI

```bash
    vue create hello-world   #создание нового проекта
    vue ui   #запуск графической оболочки vue cli
    npm run serve   #запуск сервера vue cli
```

## Vue шаблонизатор

```html
<h1>String: {{ name }}</h1>
<h1>Sum (10 + 60): {{ 10 + 60 }}</h1>
<h1>Number: {{ number }}</h1>
<h1>Method: {{ sayHello() }}</h1>
<h1>If statement: {{ isOk ? 'I am OK' : 'I am not OK!!' }}</h1>
<h1>Functions: {{ string.split('').reverse().join('') }}</h1>
```

## Директивы в Vue

_Директивы в Vue_ кусок javascript кода, который применяется на любой DOM элемент и может его менять. выглядит как `v-show="true"` где:

- _v-название_ - после него через двоеточие могут быть аргументы директивы или через точку - модификаторы
- _true_ - литерал, переменная, выражение или имя функции

### Сокращенние директив/Ярлыки модификаторов

`<a v-bind:href="url"> ... </a>` -> `<a :href="url"> ... </a>`
добавляет одностороннее связывание/биндинг

`<a v-on:click="doSmt"> ... </a>` -> `<a @click="doSmt"> ... </a>`
добавляет слушатель событий

### Директива `v-bind`

биндинг/одностороннее связывание. Применяется для изменения html атрибутов:

```html
<a v-bind:href="url">{{ url }}</a>
```

### Директива `v-html`

вывод сгенерированого html

```html
<h2 v-html="link"></h2>
```

### Директива `v-on`

добавление слушателей событий,
в функции обработчике элемент доступен по event.target()

```html
<h2 v-on:mouseover="onHover">Счётчик {{ counter2 }}</h2>
<button v-on:click="counter2++">Увеличить</button>
```

### Передача объекта event в функцию

```html
<button v-on:click="riseCounnter($event)">Увеличить</button>
```

### Модификаторы событий

```html
<span v-on:click.prevent="sameFunction"> </span> //Event.preventDefault()
<span v-on:click.stop="sameFunction"> </span> //Event.stopPropagation()
```

### Модификаторы клавиш

после точки можно писать несколько клавишь, событие будет срабатывать по любой
остальные клавиши здесь[https://vuejs.org/v2/guide/events.html#Key-Modifiers]

```html
<input type="text" v-on:keyup.enter.space="consoleValue" />
```

### Директива `v-model`

Двусторонним образом связывает элемент ввода данных или компонент с переменной.

```javascript
`v-model = "variableName"`;
```

модификатор, изменять переменную в моделе только когда уходит фокус

```javascript
`v-model.lazy`;
```

## Управление CSS классами во Vue

Способы добавления классов в том числе css

```html
<div :class="color"></div>
<!-- класс будет соответствовать значению переменной color -->
<div :class="{'red':isActive}"></div>
<!-- класс будет 'red' если isActive выдает true -->
<div :class="{'red':isActive,'green':!isActive}"></div>
<!-- то же самое для нескольких классов и условий для них -->
<div :class="[colorClass, {'red':isActive}]"></div>
<!-- массив если надо смешать классы с и без условия -->
```

## Управление инлайн стилями во Vue

```html
<div :style={borderColor:color}></div> <!-- где color имя переменнной -->
<div :style={сolor:color,borderColor:color}></div> <!-- несколько стилей -->
<div :style=[computedColor, {'сolor':color,'border-color':color}]></div> <!--  расчёт некоторых стилей(computedColor) можно выносить в раздел computed конфигурации -->
```

### Директива `v-if`

используется для рендеринга блока по условию. Блок будет отображаться только в том случае, если выражение директивы возвращает значение, приводимое к true.

```html
<h1 v-if="isVisible">I am visible</h1>
<h1 v-else>No, I am not!</h1>
```

switch условия

```html
<h1 v-if="letter==='a'">A</h1>
<h1 v-else-if="letter==='b'">B</h1>
<h1 v-else-if="letter==='c'">C</h1>
<h1 v-else>not match</h1>
```

v-if выкидывает элемент из DOM дерева полностью a v-show только скрывает его

```html
<h1 v-show="true">will show</h1>
```

### Специальный атрибут ref

Название элемента или компонента для регистрации ссылки на него.

```html
<p ref="p">hello</p>
<!-- vm.$refs.p будет DOM-элементом -->
<!-- vm.$refs.child будет указывать на экземпляр дочернего компонента -->
```

## Vue регистрация компонентов

локальная внутри компонента

```html
<template>
  <div>
    <!--корневой тег в шаблоне может быть только один -->
    <app-tag></app-tag>
  </div>
  <template>
    <script>
      import Car from "./components/car.vue";

      export default {
        name: "App",
        components: {
          HelloWorld,
          appCar: Car,
        },
      };
    </script></template
  ></template
>
```

## Vue передача параметра внутрь компонента

в родительском шаблоне

```html
<child-comp newprops="props Value"> </child-comp>
```

в компоненте ребёнка

````javascript
export default {
    props: ['newprops']
}
````

## Передача параметров разных типов

````javascript
export default {
  props: {
    title: String,
    likes: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object,
    callback: Function,
    contactsPromise: Promise // или любой другой конструктор
  }
}
````

### Работа с входными пропсами

#### Инициализация пропсами начальных значений

````javascript
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    counter: Number
  },
  data: function () {
    return {
      newCounter: this.counter+1
    }
  }
}
````

#### Преобразования поступивших пропсов

````javascript
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    counter: Number
  },
  computed: {
    normalizedSize: function () {
      return this.counter+1
    }
  }
}
````

глобальная

```javascript
// перед объявленим new Vue
import OnOffSwitch from './components/onOff';
Vue.component('app-onOff', OnOffSwitch);
````

## Шаблон нового компонента

```javascript
<template>
  <div class="new-component">
      {{ msg }}
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
```

## Передача событий к другому компоненту

передать событие updateCounter c параметром val

````html
<template>
  <div>
      <button class="btn btn-success" v-on:click="updateCounter(1)"></button>
      <button class="btn btn-danger" @click="updateCounter(-1)"></button>
  </div>
</template>

<script>
export default {
  name: 'actions',
  methods: {
    updateCounter: function(val) {
      this.$emit('updateCounter', val)
    }
  }
}
</script>
````

в родительском компоненте

````html
<app-actions @updateCounter="counter += $event"></app-actions>
````

### ESList отключение

````txt
/_ eslint no-unused-labels: "off"_/

/_ eslint-disable no-alert, no-console _/

/_ eslint-disable _/

/_ eslint-disable _/
/_ eslint-enable _/

// eslint-disable-line
// eslint-disable-next-line

// eslint-disable-line no-alert
````

### lazy loading js бандла для vue cli

в файле компонента под импортами

```javascript
const Cars = (resolve) => {
  require.ensure(["./pages/Cars.vue"], () => {
    resolve(require("./pages/Cars.vue"));
  });
};
```

### циклы в шаблоне

````html
<div v-for="item in items">
  {{ item.text }}
</div>
````

# Vue конфигурация приложения

```javascript
new Vue({
  el: "#app", //точка входа для приложения
  data: {
    //переменные приложения
    count: 0,
  },
  computed: {
    //всю сложную логику из шаблонов , в том числе из атрибутов выносим сюда
  },
  methods: {
    //методы приложения
    increment: function (a) {
      this.count += a;
    },
  },
});
```

