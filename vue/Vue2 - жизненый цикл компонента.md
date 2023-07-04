## Vue жизненный цикл

#vue2

```js
let vm = new Vue({
  el: "#app",
  data: {
    title: "First title",
  },
  methods: {
    doDestroy: function () {
      this.$destroy();
    },
  },
  beforeCreate: function () {
    console.log("Before Create");
  },
  created: function () {
    console.log("Created");
  },
  beforeMount: function () {
    console.log("Before Mount");
  },
  mounted: function () {
    console.log("Mounted");
  },
  beforeUpdate: function () {
    console.log("Before Update");
  },
  updated: function () {
    console.log("Updated");
  },
  beforeDestroy: function () {
    console.log("Before Destroy");
  },
  destroyed: function () {
    console.log("Destroyed");
  },
});
```

Если нет возможности править код компонента (например это подключаемый компонент) , то можно повесить хуки снаружи
```
<some-component
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
@hook:errorCaptured="console('errorCaptured')">
</some-component>
```