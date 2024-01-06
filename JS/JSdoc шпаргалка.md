---
Источник: https://jsdoc.app/
---
### Functions / Функции

```js
/**
 * This is a function.
 *
 * @param {string} n - A string param
 * @param {string} [o] - A optional string param
 * @param {string} [d=DefaultValue] - A optional string param
 * @return {string} A good string
 *
 * @example
 *
 *     foo('hello')
 */

function foo(n, o, d) {
  return n
}
```
Подробнее: [https://jsdoc.app/index.html](https://jsdoc.app/)

---
### Typedef / Возвращаемые типы

```js
/**
 * A song
 * @typedef {Object} Song
 * @property {string} title - The title
 * @property {string} artist - The artist
 * @property {number} year - The year
 */
```

```js
/**
 * Plays a song
 * @param {Song} song - The {@link Song} to be played
 */

function play(song) {}
```
Подробнее: [https://jsdoc.app/tags-typedef.html](https://jsdoc.app/tags-typedef.html)

---
### Types / Типы данных в параметрах 

|   |   |
|---|---|
|`@param {string=} n`|Optional|
|`@param {string} [n]`|Optional|
|`@param {(string\|number)} n`|Multiple types|
|`@param {*} n`|Any type|
|`@param {...string} n`|Repeatable arguments|
|`@param {string} [n="hi"]`|Optional with default|
|`@param {string[]} n`|Array of strings|
|`@return {Promise<string[]>} n`|Promise fulfilled by array of strings|

See: [https://jsdoc.app/tags-type.html](https://jsdoc.app/tags-type.html)

---
### Variables / Переменные 

```js
/**
 * @type {number}
 */
var FOO = 1
```

```js
/**
 * @const {number}
 */
const FOO = 1
```
---



#js  #cheatsheet #документация