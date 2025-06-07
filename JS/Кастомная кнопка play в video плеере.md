
```css
.section_video_area {
	padding: 40px 0 120px;
}

.home_video_wrap {
	display: flex;
	align-items: center;
}

.home_video_player {
	position: relative;
	display: flex;
	align-items: center;
	justify-content: center;
	overflow: hidden;
}

.home_video_player_play {
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
	z-index: 3;
	animation: pulse 1s infinite linear;
}

.home_video_player_code {
	display: flex;
	background-color: #ed6b06;
}

.home_video_player_code video {
	width: 100%;
}

video::-webkit-media-controls-overlay-play-button {
    opacity: 0 !important;
}
```

```html
				
				<div class="home_video_player">

					<div class="home_video_player_play" id="playButton">
						<svg xmlns="http://www.w3.org/2000/svg" width="30%" height="30%" viewBox="0 0 123 123" fill="none"> <circle cx="61.5" cy="61.5" r="61.5" fill="#ED6B06"></circle> <path d="M82.9259 65.1825L52.4631 83.4228C51.8116 83.7989 51.0729 83.9979 50.3205 84C49.5682 84.0021 48.8284 83.8072 48.1748 83.4348C47.5212 83.0624 46.9765 82.5254 46.5949 81.8772C46.2134 81.229 46.0083 80.4923 46 79.7403V43.2597C46.0083 42.5077 46.2134 41.771 46.5949 41.1228C46.9765 40.4746 47.5212 39.9376 48.1748 39.5652C48.8284 39.1928 49.5682 38.9979 50.3205 39C51.0729 39.0021 51.8116 39.2011 52.4631 39.5772L82.9259 57.8175C83.559 58.2014 84.0825 58.7419 84.4458 59.387C84.8091 60.032 85 60.7598 85 61.5C85 62.2402 84.8091 62.968 84.4458 63.613C84.0825 64.2581 83.559 64.7986 82.9259 65.1825V65.1825Z" fill="white"></path></svg>
					</div>

					<div class="home_video_player_code">
						<video 
							id="video"
							controls 
							preload="metadata" 
							poster="path/to/poster.webp">
							<source src="path/to/video.webm" type="video/webm">
							<source src="path/to/video.mp4" type="video/mp4">
						</video>
					</div>
				</div>
```

```js
document.addEventListener('DOMContentLoaded', function () {
	
	const video = document.getElementById('video');
	const playButton = document.getElementById('playButton');

	playButton.addEventListener('click', () => {				
		video.load(); // Загрузка видео вручную
		video.play();
		playButton.style.display='none';
	});

	video.addEventListener('pause', () => {
		if (video.currentTime > 0 && !video.ended) {
			playButton.style.display='flex';
		}
	});

	video.addEventListener('play', () => {
		playButton.style.display='none';
	});
})
```