```js
//для переменной testInput мониторим когда она изменится

  mounted() {
    var unwatch = this.$watch('testInput', function (newVal, oldVal) {        
        this.textAc += newVal + '\n'; //делаем что-то 
        unwatch(); //тут же внутри колбэка снимает вотчер 
    });    
  }
```

#vue2