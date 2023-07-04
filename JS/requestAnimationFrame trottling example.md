```js
someWrapper.addEventListener('mousemove', mouseFollower, false);

let timeoutID;
let mouseFollower = e => {                
	if (timeoutID) {
		 window.cancelAnimationFrame(timeoutID);
	}  
	timeoutID = window.requestAnimationFrame(function () {
		moveingEl.style.transform = `translate(${e.clientX}px, ${e.clientY)`;
	});
};
```

устаревшая альтернатива через `timeout` [[mouse event trottling over timeout]]

#js #performance 