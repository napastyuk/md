
Если jquery долго загружается, то скрипты которые его используют могут начать выполнятся раньше загрузки и инициализации jquery. Чтобы это избежать добавляет обёртку

```javascript
window.addEventListener("load", function (event) {
	  //к этому могут все подключенные на странице скрипты не только загрузились, но и выполнились
	  //и можно спокойно использовать $
});
```

```javascript
document.addEventListener("DOMContentLoaded", function(event) {

});
```

Так же для ускорения загрузки jquery можно сделать:
- перенести jquery c cdn в локальные скрипты
- использовать минифицированную версию дистрибутива
- перенести подключение выше в списке скриптов
- убрать атрибуты `async` и `defer` (подробнее про атрибуты [[Процесс рендеринга Web-страницы]] )


#jquery  #js #performance 