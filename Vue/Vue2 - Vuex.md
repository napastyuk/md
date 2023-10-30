# Vuex

## заведение стора

в файле store/index.js

```javascript
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    counter: 10,
  },
});
```

в файле main.js

```javascript
import Vue from "vue";
import App from "./App.vue";
import store from "./store/index";

Vue.config.productionTip = false;

new Vue({
  render: (h) => h(App),
  store: store,
}).$mount("#app");
```

## чтение из стора

```javascript
this.$store.state.counter;
```

## запись в стор

```javascript
this.$store.state.counter += val;
```

#vue #vue2 #state-manager
