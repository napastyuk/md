### Упрощенный синтаксис с `script setup`
```javascript
<script setup>
//обязательный импорт
import { ref,reactive } from 'vue'

//задание переменных
  
//reactive работает только с объектами
const message = reactive({content:"Привет мир"}) 
message.content = 'Привет вью'
  
//ref с любыми типами данных, но только через .value  
const counter = ref({count:0}); 
counter.value.count++;
</script>

<template>
  <p>{{message.content}}</p>
  <p>{{counter.count}}</p>	
</template>
```

TODO: Написать про вариант script без setup

#vue #vue3 