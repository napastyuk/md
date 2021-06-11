добавить класс с `transition` продолжительностью N и удалить этот класс через N.

css:
```css
.js_gallery_slider-moveEffect {
	transition:left 0.4s ease-in-out;
}
```
js:
```js
sliderCursor.classList.add("js_gallery_slider-moveEffect");
setTimeout(function() {
	sliderCursor.classList.remove("js_gallery_slider-moveEffect");
}, 200);
```

Минут анимация проиграется чуть меньше чем N, потому что есть задержки интерпретации.  Более сложная альтернатива [[Web Animation API]]