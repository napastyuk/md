Ака css variables

Задание
```css
:root {  
  --main-color: #ff6f69;
  --title-size: 16px;  
}
```

Использование:
```css
#title {  
  color: var(--main-color, black); /*где black - значение по умолчанию*/
  font-size: var(--title-size);  
}
```

Получение значения из JS
```javascript
var root = document.querySelector(':root');  
var rootStyles = getComputedStyle(root);  
var mainColor = rootStyles.getPropertyValue('--main-color');
```

Задание значения через JS
```javascript
root.style.setProperty('--main-color', '#88d8b0');
```

вместо `:root` может быть любой другой DOM-элемент или их список, тогда видимость переменной будет ограничена этой областью
```javascript
const tableNodeEl = document.querySelector('.result > table');
const rowsNodeList = this.$refs.table.$el.querySelectorAll('.result tbody > tr');
rowsNodeList.forEach((el,index) => tableNodeEl.style.setProperty(`--${index}-row-height`, `${el.clientHeight}px`));
```
