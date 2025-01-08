```
/*
* this.sourceArr - массив в котором все происходит
* oldPosition и newPosition - соотвественно индексы позиций передвигаемых элементов
*/
this.sourceArr[newPosition] = this.sourceArr.splice(oldPosition, 1, this.sourceArr[newPosition])[0]
```
Метод основан на том , что splice возвращает удаленные элементы( `[0] в конце строки`) 

#vue #реактивность 