# SVG
## Способы вставки svg
### 1. Тег Img / picture / стиль Background-image
подходит для контентных изображений, которым не нужно взаимодействие.
т е размеры svg до рендеринга изменить тоже не получится.
```html
<img src="bblogo.svg" height="65" width="68">
```
```css
.logo {
  background-image: url(bblogo.svg);
}
```
| Функции стилизации                         | Доступность |
| ------------------------------------------ | ----------- |
| подключаемый в svg внешний сss             | нет         |
| подключаемый в svg внутренний сss          | да          |
| подключаемый в svg внешний js              | нет         |
| подключаемый в svg внутренний js           | нет         |
| обычная SVG-анимация(SMIL)                 | да          |
| интерактивная SVG-анимация                 | нет         |
| обращение из DОМ документа к атрибутам SVG | невозможно  |

*Генерация SVG is js*

### 2. Object
больше вариантов для интерактива внутри SVG, но ограничение на вставку с другого домена
```html
<object type="image/svg+xml" data="bblogo.svg" id="object">not support SVGs</object>
```
| Функции стилизации                | Доступность |
| --------------------------------- | ----------- |
| подключаемый в svg внешний сss    | да          |
| подключаемый в svg внутренний сss | да          |
| подключаемый в svg внешний js     | да          |
| подключаемый в svg внутренний js  | да          |
| обычная SVG-анимация(SMIL)        | да          |
| интерактивная SVG-анимация        | да          |


*обращение из DОМ документа к атрибутам SVG*
```js
var object = document.getElementById("object"); //получаем элемент object
var svgDocument = object.contentDocument; //получаем svg элемент внутри object
var svgElement = svgDocument.getElementById("some_id_in_svg"); //получаем любой элемент внутри svg
svgElement.setAttribute("fill", "black"); //меняем атрибуты выбранного элемента
```

### 3. Inline
легко управляются(т к являются частью DOM), но по этим же причинам не кешируются браузером
```html
<svg xmlns="http://www.w3.org/2000/svg">
    <!-- svg tags here -->
</svg>
```
| Функции стилизации                | Доступность |
| --------------------------------- | ----------- |
| подключаемый в svg внешний сss    | да          |
| подключаемый в svg внутренний сss | да          |
| подключаемый в svg внешний js     | да          |
| подключаемый в svg внутренний js  | да          |
| обычная SVG-анимация(SMIL)        | да          |
| интерактивная SVG-анимация        | да          |


*обращение из DОМ документа к атрибутам SVG*
```js
var svgDocument = document.getElementsByTag("object")[0]; //получаем элемент object
var svgElement = svgDocument.getElementById("some_id_in_svg"); //получаем любой элемент внутри svg
svgElement.setAttribute("fill", "black"); //меняем атрибуты выбранного элемента
```

### 4. Так же возможно, но не нежелательно

- _Iframe_
т к строит внутри себя полноценную DOM модель, может быть ресурсозатратно
```html
<iframe src="bblogo.svg">not support Iframes</iframe>
```

- _Embed_
так как семантически придназначен для "внешних приложениях» или «интерактивном контенте"
```html
<embed type="image/svg+xml" src="bblogo.svg" />
```

## Способы изменения svg

### 1. Подключаемый в svg внешний сss
```xml
<svg xmlns="http://www.w3.org/2000/svg">
  <style type="text/css">
    <![CDATA[
        /*css rules here*/
    ]]>
  </style>
<!-- svg tags here -->
</svg>
```

### 2. Подключаемый в svg внутренний сss
на svg элементы действуют не все свойства css!
```xml
<?xml-stylesheet type="text/css" href="style.css"?>
    <svg xmlns="http://www.w3.org/2000/svg">
</svg>
```

### 3. Подключаемый в svg внешний js для svg v 2.*
```xml
<svg xmlns="http://www.w3.org/2000/svg">
    <!-- svg tags here -->
    <script href="script.js"/>
</svg>
```






### 4. Подключаемый в svg внешний js для svg v 1.*
```xml
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <!-- svg tags here -->
    <script xlink:href="script.js"/>
</svg>
```

### 5. Подключаемый в svg внутренний js
```xml
<svg xmlns="http://www.w3.org/2000/svg">
    <!-- svg tags here -->
    <script>
        <![CDATA[
            var object = document.getElementById("ball");
            object.setAttribute("fill", "red");
        ]]>
    </script>
</svg>
```

### 6. Обычная SMIL SVG-анимация
```xml
<svg xmlns="http://www.w3.org/2000/svg">
    <circle cx="20" cy="20" r="20">
        <animate attributeName="cx" from="0" to="100" dur="5s" repeatCount="indefinite" />
    </circle>
</svg>
```

### 7. интерактивная SVG-анимация
```xml
<svg xmlns="http://www.w3.org/2000/svg">
    <circle cx="20" cy="20" r="20">
        <animate begin="click" attributeName="cx" from="0" to="100" dur="5s" repeatCount="indefinite" />
    </circle>
</svg>
```

## Размеры в svg
заранее неизвестные размеры svg элемента можно получить следующими способами:
1. Вставить svg в html напрямую(инлайново) и разместить скрипт в футере
    + много методов определения размера
    - неудобства при сборке и поддержке
2. Вставить svg ссылкой на внешний файл, но в скрипте сначала дождаться прогрузки всей страницы
    + более чистый html код
    - если не прописаны размеры обёртки и/или svg тега, то svg файл при загрузке будет выскакиваать на размер всей страницы.
3. Запросить внешний svg файл через
    + не ломается верстка при загрузке
    - двойная загрузка файлов. Сначала при определении размеров, потом при добавлении в DOM
4. Серверный рендеринг

Размер для svg задаются (в порядке повышения приоритета):
1. Размеры тега svg на странице по умолчанию 300x150рх (если не указывать никаких размеров)
2. Размеры в атрибутах тега svg 'width="300" height="100"'
3. Размеры в внешних и инлайновых стилях по обычным правилам спецефичности css.

Методы получение размеров если уже есть доступ к элементу svg

`svg.getBBox();` //возвращает объект который описывает координаты рамки охватывающей все объекты внутри тега svg независимо от заданных ему размеров и координат в документе.
`svg.getBoundingClientRect();`  //возвращает объект который описывает координаты рамки самого тега svg c учетов размеров и положения на экране;

```js
\\свойства svg как элемента DOM.
svg.clientWidth
svg.clientHeight
svg.scrollHeight
svg.scrollWidth
```
так же можно прочитать атрибуты width и height внутри svg

## Спрайты через svg
# Преимущества
Удобнее растровых картинок потому что:
- меньше весят
- лутше масштабируются

Удобнее шрифтовых иконок потому что:
- Для svg большое возможностей стилизации(несколько цветов, градиенты, паттерны, фильтры, анимации)
- Не нужно "боротся" со втроенным поведеним шрифтов (межстрочные расстояния, выносы шрифта, сглаживание, пробелы между символами)
Минус только в том что сглаживание мелкого текста бывает хуже чем у шрифтов.

# Как использовать

1. Подготавливаем файл со спрайтами
```html
<svg xmlns="http://www.w3.org/2000/svg" height="0" width="0">
  <symbol id="icon_id_1">
    <!-- код одной иконки -->
  </symbol>
  <symbol id="icon_id_2">
    <!-- код другой иконки -->
  </symbol>
</svg>
```
Нулевые width и height нужны для того, чтобы иконки при загрузки без стилей не отобразились на весь экран.
xmlns атрибут указания name space особенно нужен для xhtml

2.Подключаем, желательно до использования самой иконки
```html
<object type="image/svg+xml" data="path/toFile.svg" style="display: none;"></object>
```
Тег symbol на экране не вывождится, но место для него резервируется! Поэтому подключение надо удалять из DOM

3. Используем конкретную иконку
```html
<svg class="styleClasses">
  <use xlink:href="path/toFile.svg#icon_id_1"></use>
</svg>
```
4. Стилизуем иконку
```css
.styleClasses {
    width:50px;
    height:50px;
}

.styleClasses > use {
    fill:red;
}
```
