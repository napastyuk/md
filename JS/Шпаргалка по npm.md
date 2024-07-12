
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

Кодирование версий в package.json

Semver:
major.minor.patch

После команды `npm i`

```
//для стабильных пакетов
"same-pcg": "1.0.0"   //останется на тоже версии
"same-pcg": "~1.0.0"  //установит ту же или patch-версию , например 1.0.1
"same-pcg": "^1.0.0"  //установит ту же или minor-версию , например 1.1.0

//для нестабильных пакетов
"same-pcg": "^0.1.0"    //установит ту же или patch-версию , например 0.1.1
```

--legacy-peer-deps