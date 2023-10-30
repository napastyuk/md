```javascript
loadQueriesList() {
	let requestLimit = 1000;
	let promise = (params) => {
		return libAjax.get(`calls/saved-queries`, { params })
				.then(response => {
					this.savedQueryList.push(...response.data.list)
					return response.data.total
				})
				.then(totalQueryCount => {
					if (this.savedQueryList.length < totalQueryCount) {
						promise({
							limit: requestLimit,
							offset: this.savedQueryList.length,
						})
					}
				})
	}

	return promise({
		limit: requestLimit,
		offset: this.savedQueryList.length,
	})
},
```
вызов `libAjax.get` присваивается в переменную `promise`. И в последнем `then()` вызывается заново если нужно сделать запрос  со следующим сд№мгу2мгувигом.

#vue #vue2 #асинхронность 