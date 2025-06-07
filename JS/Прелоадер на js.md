Размещается сразу после тега `body` , целиком в html без внешних файлов. Чтобы `preloader` был спарсен первым. 
```css
	.preloader {
		position: fixed;
		max-width: 100vw;
		height: 100%;
		min-height: 100%;
		left: 0;
		top: 0;
		right: 0;
		bottom: 0;
		z-index: 999999;
		text-align: center;
		background-color: #fff;
		overflow: hidden;
	}

	.preloader_img {
		position: absolute;
		display: inline-block;
		width: 100%;
		min-width: 200px;
		height: auto;
		top: 40%;
		left: 0;
	}

	.preloader_img img {
		width: 5%;
		min-width: 200px;
		margin: auto;
	}
```

```html
<div class="preloader">
	<div class="preloader_img">
		<img src="path/to/preload/img.jpg" alt="preloader image">
	</div>
</div>
```

```js
	window.addEventListener('load', () => {
		const preloader = document.querySelector('.preloader');
		if (preloader) {
		// Устанавливаем стили для плавного выцветания
		preloader.style.transition = 'opacity 0.5s ease';
		preloader.style.opacity = '0';

		// После завершения анимации полностью скрываем элемент
		setTimeout(() => {
			preloader.style.display = 'none';
		}, 500); // Время должно соответствовать transition (0.5s)
		}
	});
```