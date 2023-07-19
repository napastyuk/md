в файле `... config\storybook\preview.js`
```javascript
import Vue from 'vue';
import Vuex from 'vuex'; //импортируем стор

import store from '../../src/store/store';  //путь до основного стора приложения
import userData from './userDate' //мок объект

Vue.use(Vuex); //подключаем стор

Vue.prototype.$store = store; //хак чтобы стор корректно вызывался в компонентах

store.commit('setIsLoggedIn', userData);  //замокаем данные пользователя в сторе
```

#vue #storybook #vuex