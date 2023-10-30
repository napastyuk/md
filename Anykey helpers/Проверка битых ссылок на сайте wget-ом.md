```bash
wget --recursive --spider --level=10 --no-directories --reject '*.css, *.png, *.jpg, *.gif, *.js, *.pdf, *.ico, *.exe, *.xls' --no-verbose http://beget.com
```
или сокращенный
```bash
wget -r --spider -l 10 -nd -R '*.css, *.png, *.jpg, *.gif, *.js, *.pdf, *.ico, *.exe, *.xls' -nv http://beget.com
````
дает вывод типа 
```
2019-05-15 21:28:02 URL:https://beget.com/ru [64493] -> "index.html.tmp.tmp" [1]
2019-05-15 21:28:02 URL:https://beget.com/robots.txt [67/67] -> "robots.txt" [1]
2019-05-15 21:28:02 URL:https://beget.com/ru [64493] -> "index.html.tmp.tmp" [1]
Found 1 broken link.
https://beget.com/ru/voip
FINISHED --2019-05-15 21:12:00--
Total wall clock time: 34s
Downloaded: 333 files, 20M in 1,9s (10,6 MB/s)`
```

Большой вывод можно записать в файл `--output-file` или `-o` , но все там не будет номеров http ответов конкретных страниц
Также можно попробовать записывать только http заголовки ключом `--server-response` или `-S`. Правда записываться они будут не stdout а в stderr, а учитывая что в stdout идет еще и поток загружаемых файлов, делаем так 
`2>&1 >/dev/null` что переводится как сначала STDERR(2) перенаправим(>) на консоль, а потом(&) STDOUT(1) в пустоту(/dev/null) 
но текста будет много поэтому попробуем перенаправить вывод

Единственный минус - wget ходит только по самому сайту не заходя на внешние ссылки , а curl не получилось заставить ходить в режиме паука