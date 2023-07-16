
```bash

# инициализация папки как npm-пакета, нужна для любой работы с npm
npm init

# Устанавливает/обновляет все пакеты, перечисленные в package.json
npm i
npm install

# Устанавливает конкретный пакет express
npm i express
npm install express

# Удаляет конкретный пакет express
npm r express
npm uninstall express

# Устанавливает express и вносит запись о нем в package.json в секцию dependencies
npm install express -S
npm install express --save

# Устанавливает grunt и вносит запись о нем в package.json в секцию devDependencies
npm install express -D
npm install express --save-dev

#проверить, не устарели ли пакеты
npm outdated

#обновить пакеты
npm update

# NPM вполне может обновлять сама себя
npm update npm -g

# все npm-скрипты прописываются в package.json
# у npm есть 2 типа скриптов которые можно запускать напрямую.
npm start

# и
npm test
# все остальные скрипты должны запускаться через команду
npm run yourScript
```