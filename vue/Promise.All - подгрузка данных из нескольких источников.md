#vue2

```javascript
//...
method: {
	loadProfiles() {
		const data = {
			//JSON request body
		}
        return libAjax.post("profile/list", data)
        .then((response) => {
			//сохраняем данные из ответа	
        })
    },
    loadRules(){ //аналогично loadProfiles
    }
},
mounted() {
	//включаем лоадер
	Promise.all([this.loadProfiles(), this.loadRules()])
	.then(() => {
		//все промисы успешно разрешились
	}).final(()=> {
		//выключаем лоадер
	})
}
//...
```