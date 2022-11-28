```javascript
/*
	 * Автовоспроизведение видео по появлению в видимой части экрана
	 * спека для плеера https://github.com/mediaelement/mediaelement
	 * */
	
	const trueCallback = function(entries, observer) {
		entries.forEach((entry) => {			
			const { target, isIntersecting } = entry;
			let playerId = target.closest('.mejs-container').getAttribute('id');
			var playerInstance = mejs.players[playerId];
			if( isIntersecting ) {
				playerInstance.play();
			} else { 
				playerInstance.pause();
			}
		});
	}
	
	const observer = new IntersectionObserver( trueCallback, {threshold: 1} );
	
	//запуск отслеживания только после инициализации плеера mediaelementplayer
	$('video').mediaelementplayer({
		startVolume: 0,  //начальный уровень громкости
		loop: true,		 //зациклить воспроизведение
		success: function(media, node, instance) {
			/*
			 * скрытие контролов работает только через css. Для полного скрытия в стилях должено содержаться:
			 * .mejs-controls-hide { display: none !important; visibility: hidden !important}  
			 * */
			node.closest('.mejs-container').querySelector('.mejs-controls').classList.add('mejs-controls-hide')
			observer.observe(node);			
		}
	})
```