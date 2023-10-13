Для скачивания файлов в браузере используется атрибут  ссылки `download` https://caniuse.com/download
```html
<a download="newFile.txt" id="link">Загрузить</a>
```
При переходе по этой ссылке( или при генерации события `click`)  будет происходить скачивание.

Если нужно скачать файл сгенерированный на клиенте, но сначала создадим адрес по которому будет располагаться это файл с помощью конструктора `createObjectURL`.   `URL.createObjectURL` берёт Blob и создаёт уникальный URL для него в формате `blob:<origin>/<uuid>`. Например `blob:https://javascript.info/1e67e00e-860d-40a5-89ae-6ab0cbee6273`. `createObjectURL` принимает на вход `Blob` или `File`.   
```js
const file = new Blob(["Hello, world!"], {type: 'text/plain'}); 
//или
const file = new File(["Hello, world!"], "foo.txt", {type: "text/plain"});
link.href = URL.createObjectURL(file);
```
Разница между ними в том, что у `File` уже есть метаданные (имя и дата изменения). Для нашего случая это не актуально так как они все равно будут перезаписаны браузером при скачивании, поэтому обычно используют `Blob`

Если файл большой , то обязательно нужно вызывать `revokeObjectURL` потому что созданная через `createObjectURL` связка ссылки и файла продолжит храниться в памяти браузера 

Полный пример:

```js
let link = document.createElement('a');
link.download = 'hello.txt';
let blob = new Blob(['Hello, world!'], {type: 'text/plain'});
link.href = URL.createObjectURL(blob);
link.click();
URL.revokeObjectURL(link.href);
```


