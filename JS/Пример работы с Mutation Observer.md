```js
//обновление итоговой цены по изменению количества лицензий

const globalObservers = {};//глобальная переменная для хранения наблюдателей

document.addEventListener('DOMContentLoaded', () => {
    //запускать скрипт только на странице цены
    if (window.location.pathname !== '/ceny/') return;

	//массив с названиями классов для каждой отдельной таблицы
    //на том же элементе в DOM ожидается класс 'prices_table',  
	let tablesArray = [
		'prices_table_local_usb',
		'prices_table_local_prog',
	];

	//для каждой таблице по очереди
	tablesArray.forEach(el=>addCalculationLiseners(el));

	//добавляем прослушиватели на изменение значения в инпутах с количеством рабочих мест
    //поля изменются скриптом, поэтому стандартное событие `change` не подходит 
	function addCalculationLiseners(tableName) {
        //сохраняем MutationObserver-ы в переменную 'globalObservers' чтобы при уходе со страницы закрыть их
        globalObservers[tableName] = new MutationObserver(mutationCallback);
        
        //класс подобран экпериментальным способом, такой чтобы элемент отлавливал мутации
        let workPlacesElList = document.querySelectorAll(`.${tableName} .woopq-quantity-input`);
        workPlacesElList.forEach(workPlaceItem=>{
            globalObservers[tableName].observe(workPlaceItem, { attributes: true });
        })
	};

    function mutationCallback(mutations) {
        let isChanging = false;
        for (let mutation of mutations) {

            //мутации идут подряд, поэтому ставим lock чтобы не запустить несколько пересчётов одновременно
            if (isChanging) continue 
            isChanging = true;

            //опеределим в какой таблице был клик
            let clickedTableEl = mutation.target.closest('.prices_table');
            let currentTableName = tablesArray.find(el=>clickedTableEl.classList.contains(el));
            
            //собираем актуальные значения количества рабочих мест
            let workPlacesArr = []; //массив для значений
            let workPlacesSum = 0;  //переменная для суммы
            let currentTable = document.getElementsByClassName('prices_table_local_usb')[0];
            let workPlacesInputList = Array.from(currentTable.getElementsByClassName('woopq-quantity-input'));
            workPlacesInputList.forEach(el=>{
                let curentWorkPlacesCount = parseInt(el.getElementsByTagName('input')[0].value);
                if (isNaN(curentWorkPlacesCount)) console.warn('в поле ', el.getElementsByTagName('input')[0], 'не число');
                workPlacesArr.push(curentWorkPlacesCount);
                workPlacesSum += curentWorkPlacesCount;
            });

            //по аналогии с рабочими местами, собираем значения цен за лицензии
            //поддерживаются только суммы без копеек,
            //все что после символа точки или запятая будет проигнорированно
            let licensePriceArr = [];
            let licenseTotalPrice = 0;	
            let priceList = Array.from(currentTable.getElementsByClassName('prices_table_td_program_price'));
            priceList.forEach(el=>{
                let currentPriceText = el.getElementsByClassName('woocommerce-Price-amount')[0].innerText;
                //число может быть с разделением на разряды поэтому уберём все пробелы 
                let currentPriceNumber = parseInt(currentPriceText.replace(/\s/g, '')); 
                if (isNaN(currentPriceNumber)) console.warn('в поле ', el.getElementsByClassName('woocommerce-Price-amount'), 'не число');
                licensePriceArr.push(currentPriceNumber);
                licenseTotalPrice += currentPriceNumber;
            })

            //и точно так же с соберём цену за один ключ
            let keyPriceText = currentTable.getElementsByClassName('prices_table_td_key_price')[0].innerText;
            let keyPriceNumber = parseInt(keyPriceText.replace(/\s/g, ''));
            if (isNaN(keyPriceNumber)) console.warn('в поле ', currentTable.getElementsByClassName('prices_table_td_key_price')[0], 'не число');  

            // если это таблица с локальными USB ключами, то перемножим стоимость одного ключа на количество рабочих мест
            let finalPrice = 0;
            if (currentTableName === "prices_table_local_usb") {
                finalPrice = licenseTotalPrice + (keyPriceNumber * workPlacesSum);
            } else {
                finalPrice = licenseTotalPrice + (keyPriceNumber * 1);
            }

            //для дебага
            console.table({
                'Сумма по лицензиям':licenseTotalPrice.toLocaleString(),
                'Количество рабочих мест':workPlacesSum.toLocaleString(),
                'Сумма за ключи':(keyPriceNumber * workPlacesSum).toLocaleString(),
                'Итоговая сумма':finalPrice.toLocaleString(),
            })

            //меняем итоговую цену в ячейке таблицы
            currentTable.getElementsByClassName('prices_table_td_total_title_value')[0].innerText = finalPrice;

            //снимает lock с задержкой, чтобы скипнуть мутации которые идут подряд
            setTimeout(() => isChanging = false , 100);  
        }
    };
});

//закрываем наблюдателей перед уходом со страницы
window.addEventListener('beforeunload', function () {
    if (globalObservers) Object.values(globalObservers).forEach(observer=>observer.disconnect());
})
```