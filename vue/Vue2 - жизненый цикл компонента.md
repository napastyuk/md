## Vue жизненый цикл

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
