- `boolean` 
- `number`
- `string`

Явное определение типов (необязательное в TS)
`let tmp:string = 'tmp string'`

Объединение типов/Union Type. Удобна чтобы записать в типы отсутвующее значение
`let tmp : number | null = 12`

или так при определении функции
`function someFunction(name?: string | null){}`
? выводится в `| underfined` и мы получаем  `name: string | underfined | null`

если задать дефолтное значение, то тип параметра можно не указывать, он выводится
`function someFunction(name='tmp'){}`

так же можно указать тип данных возвращаемый функцией, но обычно он тоже выводится
```
function someFunction(name:string):string{
	return tmp
}
```


## Массивы
1 способ
```
let list: number[] = [10, 20, 30];
let colors: string[] = ["red", "green", "blue"];
```
2 способ
```
let list: Array<number> = [10, 20, 30];
let colors: Array<string> = ["red", "green", "blue"];
```
не смотря на то что `number` с маленькой буквы, `Array` всегда с большой!



#typescript  #типизация 