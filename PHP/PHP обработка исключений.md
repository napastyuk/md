## Стандартные исключения
Пример кода который выбрасывает исключение
```php
try {
	// выполняем какой-то код... В случае ошибки выбрасываем исключение
    // Примеры стандартных исключений
    throw new \InvalidArgumentException('Неверный формат данных');
    throw new \RuntimeException('Ошибка во время выполнения');
    throw new \LogicException('Неправильная логика программы');
    throw new \OutOfBoundsException('Значение вне допустимого диапазона');
    
} catch (\Exception $e) {   
    http_response_code(500);

	// Теперь мы можем использовать методы объекта исключения
    echo $e->getMessage();      // выведет: "Что-то пошло не так"
    echo $e->getFile();         // выведет путь к файлу, где произошла ошибка
    echo $e->getLine();         // выведет номер строки, где произошла ошибка
    echo $e->getTraceAsString(); // выведет полный стек вызовов

	//например записать в логи
	error_log("Error in handleRequest: " . $e->getMessage());
    error_log("Stack trace: " . $e->getTraceAsString());

	//или вернуть на вывод
    return 'Internal Server Error: ' . $e->getMessage();
}

//где то дальше по коду 

throw new \InvalidArgumentException('Ошибка')


```

- `throw` - ключевое слово PHP для генерации исключения
- `new \InvalidArgumentException` - создание нового объекта исключения
- Когда мы пишем `catch (\Exception $e)`, мы говорим PHP: "Перехвати любое исключение и положи его в переменную `$e`". 
- Символ `\` используется для указания на то, что `Exception` - это глобальный класс исключений


## Кастомные исключения

```php
//MyProject\Exceptions\CliException.php
namespace MyProject\Exceptions;
class CliException extends \Exception
{
}

//Main_file.php
try {
    // код, который может выбросить исключение
} catch (CliException $e) {
    echo "CLI error: " . $e->getMessage();  //кастомное исключение
} catch (\Exception $e) {
    echo "General error: " . $e->getMessage();  //стандартное исключение исключение
}
```
Класс `CliException` может быть пустым. Методы туда можно будет добавить если понадобятся нестандартные методы у ошибок.
