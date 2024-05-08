отправка нескольких ajax запросов подряд
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

аналогично для vanila
Первый Promise.all отправляет fetch
Второй Promise.all объединяет response
```javascript
Promise.all([
    fetch('https://jsonplaceholder.typicode.com/posts'), 
    fetch('https://jsonplaceholder.typicode.com/users')
    ])
.then(responses=>Promise.all(responses.map(response=>response.json())))
.then(data => console.log(data))
.catch(error=>console.log(error));

```

#vue2 #vue2 #асинхронность
