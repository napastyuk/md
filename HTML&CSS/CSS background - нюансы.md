Обычная сокращенная запись
```css
body {
	background: center / contain no-repeat url("../logo.svg")  
}
```

Ниже - отдельные свойства с важными деталями
```css
background-color: blue; /*закраска фона только цвета, так же fallback для загружаемого изображения*/
``` 

```css
background-image: none; /*изображение для фона, можно указывать несколько изображений через запятую тогда они применятся одновременно*/

background-image: url("путь-до-изображения") /*путь до файла с изображением */

background-image: image-set("путь-до-изображения" Nx); /*аналог srcset для img*/

background-image: linear-gradient(); /*линейный градиент*/

background-image: repeating-linear-gradient() /*повторяющийся линейный градиент*/

background-image: radial-gradient() /*радиальный градиент (смена цвета из центра к краям круга)*/

background-image: conic-gradient() /*конический градиант (цвет меняется идя по периметру круга)*/
```
поддержка для `image-set` на https://caniuse.com/?search=image-set  

```css
background-size:  auto auto; /*задает размер фонового изображения*/
```

```css
background-repeat: repeat repeat; /*как повторять фон по горизонтали и вертикали*/
```

```css
background-origin: padding-box; /*позиционирование фонового рисунка, относительно чего НАЧАТЬ ВЫРАВНИВАНИЕ фона*/
```  
  
```css
background-position: 0% 0%; /*позиционирование фона в рамках заданных background-origin по горизонтали(X) и вертикали(Y)*/
```  

```css
background-clip: border-box; /*позиционирование фонового рисунка, относительно чего ОБРЕЗАТЬ фон не смотря изначальное выравнивание*/
```  
  
```css
background-attachment: scroll; /*надо ли прокручивать фон*/
```  
  

  

  
  
