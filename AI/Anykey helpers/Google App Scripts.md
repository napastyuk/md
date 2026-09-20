Скрипт который получает значение из api и отдает его в формулу с учетом кеша 

```javascript
// function onOpen() {
//   var ui = SpreadsheetApp.getUi();
//   ui.createMenu('Свое меню')
//       .addItem('Очистить кеш', 'menuItem1')
//       .addToUi();
// }

// function menuItem1() {
//   SpreadsheetApp.getUi()
//      .alert('You clicked the first menu item!');
// }
  
String.prototype.addQuery = function (obj) {
  return (this == "" ? "" : `${this}?`) + Object.entries(obj).flatMap(([k, v]) => Array.isArray(v) ? v.map(e => `${k}=${encodeURIComponent(e)}`) : `${k}=${encodeURIComponent(v)}`).join("&");
}

/**
 * Курс валюты по данным  coinmarketcap.com.
 * Список самых популярных id
 * 2781  - USD фиатный доллар
 * 2806  - RUB фиатный рубль
 * 1     - BTC биткоин
 * 1027  - ETH эфир
 * 11419 - TON тон
 * @param {string} from_coin_id id валюты ИЗ которой надо перевести.
 * @param {string} to_coin_id id валюты В которую надо перевести.
 * @param {number} amount количество валюты которое надо перевести. Необязательный параметр, по умолчанию 1.
 * @return .
 * @customfunction
*/

function CRYPTORATES(from_coin_id,to_coin_id,amount = 1) {
  if (from_coin_id === undefined || to_coin_id === undefined) return 0
  const options = {
    headers: {
      'X-CMC_PRO_API_KEY': '26318a73-94f9-4357-9641-9a83a3017673'
    }
  }
  const url = "https://pro-api.coinmarketcap.com/v2/tools/price-conversion";
  const query = {
    id: from_coin_id,
    convert_id: to_coin_id,
    amount: amount,
  };
  const endpoint = url.addQuery(query); //сформируем url запроса
  //перед запросом проверим кеши, вдруг это запрос уже есть.
  const cache = CacheService.getScriptCache();
  const cacheName = from_coin_id+'-'+to_coin_id+'-'+amount;
  const cached = cache.get(cacheName);
  if (cached != null) {
    //Logger.log('результат из кеша', cached);
    return cached;
  }
  const response = UrlFetchApp.fetch(endpoint, options);
  const content = response.getContentText(); //Декодируем строку ответа
  const result = JSON.parse(content); //Превращаем все еще строку в объект, с которым можно работать
  const resultPrice = Object.values(result.data.quote)[0].price.toString();
  //const commaSeparateResult = resultPrice.replace('.', ','); //В гугл таблицах целая часть отделяется запятой! не нужно
  cache.put(cacheName, commaSeparateResult , 60);
  //Logger.log('результат из сети', resultPrice);
  return commaSeparateResult;
  // Logger.log(Object.values(result.data.quote)[0].price)
}

//Logger.log(CRYPTORATES(11419,2806));
//Logger.log(CRYPTORATES(11419,2806));
```
