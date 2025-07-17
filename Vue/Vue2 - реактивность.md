Во vue 2 реактивность сделана через getter-ы и setter-ы.  Они проставляли в момент инициализации и если после инициализации в поле добавлялся другой объект, он игнорировался системой реактивности.  Для того чтобы он добавлялся в систему реактивности были метод `$set` 

## Работа с объектами:

```javascript

this.$set(this.someObject, 'b', 2) //добавим в объект this.someObject поле со значением 2

//для нескольких свойств
// вместо `Object.assign(this.someObject, { a: 1, b: 2 })` 
this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })

```

## Работа с массивами:

Vue не может отследить следующие изменения в массиве:

1.  Прямую установку элемента по индексу: `vm.items[indexOfItem] = newValue`
2.  Явное изменение длины массива: `vm.items.length = newLength`


Реактивная установка элементов по индексу
```javascript
// Использовать Vue.set
Vue.set(массив, индексКудаДобавлять, чтоДобавлять)

//тоже самое 
vm.$set(vm.items, indexOfItem, newValue)

//альтернатива использовать Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)

```

Изменение длинны массива
```javascript
// Использовать Vue.set
Vue.set(vm.items, indexOfItem, newValue)

// Использовать Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)

```

Зато удаление можно делать явно , встроенной командой 
```javascript
this.$delete(this.targetArr, index)
```



во vue3 такой проблемы нету, там реактивность сделана через `proxy` 


## Копирование объекта
Если в объекте нет вложенных объектов то через `Object.assign()` если есть то через `JSON.parse(JSON.stringify())`;


#vue #vue2 #реактивность
