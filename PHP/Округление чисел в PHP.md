#php/типизация 

| Функция                  | Описание                                 | Пример результата (`3.7`) |
| ------------------------ | ---------------------------------------- | ------------------------- |
| `round()`                | Округление по правилам математики        | `4`                       |
| `floor()`                | Округление вниз                          | `3`                       |
| `ceil()`                 | Округление вверх                         | `4`                       |
| `intval()` / `(int)`     | Отбрасывание дробной части               | `3`                       |
| `number_format()`        | Форматирование числа (возвращает строку) | `"3.70"`                  |
| `sprintf()` / `printf()` | Форматирование строки                    | `"3.70"`                  |
Так же еще есть функция округления в модуле `bcmath` и самостоятельно написанные функции округления.

Кстати функции `floor()` и `intval()` делают разное! Просто разница видна только в отрицательных числах.

