1. Скачивание HTML. Скачивание идет последовательно по частям. Параллельно из уже скачанных частей стоится DOM.  

2. Как только браузер натыкается на запрос любого внешнего источника, он запускает сканер предварительной загрузки. Ищет все внешние ресурсы и начинает их скачивать. Количество потоков для HTTP/1.х от 2 до 8 у разных браузеров(для HTTP/2 снято). Приоритет скачивание обычно идет независимо от упоминания в коде по приоритетам и эвристике браузера (css и js выше картинок и т д). Если запрос на скачивание внешнего ресурса(css/js) ничего не вернул, то по прошествии таймаута браузер снимает блок и пытается построить render tree из того что есть

3. CSS. Скачивание - синхронно. Очередь на скачивание по мере упоминания в коде. Асинхронность можно добиться через link rel preload / медиа запросами / js вставкой тега со стилями. Встреченные импорты тоже скачиваются синхронно! 

4. Выполнение CSS (построение CCSOM) - из-за каскадной структуры не может выполнятся по частям, поэтому если начался анализ, он блокирует выполнение JS и дальнейшее построение DOM (не не блокирует скачивание и парсинг)

5. JS. Скачивание - синхронно. Очередь на скачивание по мере упоминания в коде. Выполнение 
- без атрибутов и инлайновые скрипты при начале выполнения блокируют парсинг/выполнение HTML и CSS
- с `async`. Без блокирования загрузки страницы. Браузер будет грузить его в другом потоке с более низким приоритетом. Как только скрипт будет загружен, браузер заблокирует DOM и выполнит его, порядок выполнения не гарантируется и зависит от порядка скачивания. 
- с `defer`. Без блокирования загрузки страницы. Скрипты будут ждать завершения парсинга HTML и только потом выполняться в порядке появления в коде.
[Подробнее про js события загрузки страницы](События%20загрузки%20страницы%20по%20порядку.md)

6. Построение дерева рендеринга / construction render tree - объединение DOM + CSSОМ + JS операции над ними.

7. Построение макета страницы / layout rednder tree - определение размеров и координат всех элементов на странице - объекты пересчитываются в набор прямоугольников видимых на экране

8. вывод на экран / Painting - страница появляется на экране

P.S. Для чего нужен Virtual DOM?
Web строился текстово-ориентированным. Поэтому стандарт DOM получился таким что точечные изменения проводятся не оптимально. Но так как к тому времени он уже успел стать общепринятым стандартом, ломать обратную совместимость не стали. Так получилось что любые JS операции запрашивающие размеры, цвета и координаты элементов вызывают вызывают предварительный reflow repaint иногда даже каскадный. 


