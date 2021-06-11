```js
let timeoutID;
let mouseFollower = e => {                
	if ( !timeoutID ) {
		timeoutID = setTimeout(function() {
			timeoutID = null;
			movingEL.style.transform = `translate(${e.clientX}px, ${e.clientY)`;
		}, 66);
	}
};
```