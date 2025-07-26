```php
<?php

// Класс узла связного списка
class ListNode {
    public $val = 0; // Значение, которое хранится в узле
    public $next = null; // Ссылка на следующий узел (по умолчанию null)
    
    function __construct($val = 0, $next = null) { // Конструктор узла
        $this->val = $val; // Устанавливаем значение узла
        $this->next = $next; // Устанавливаем ссылку на следующий узел (если передан)
    }
}

// Класс односвязного списка
class LinkedList {
    private ?ListNode $head = null; // Головной (первый) узел списка, изначально пуст

    // Добавление в конец списка O(n)
    // В худшем случае приходится проходить весь список, чтобы найти последний узел
    // Можно улучшить до O(1), если хранить указатель на последний узел $tail
    public function append($val): void {
        $newNode = new ListNode($val); // Создаем новый узел
        if ($this->head === null) { // Если список пуст, новый узел становится головой списка
            $this->head = $newNode;
            return;
        }

        $current = $this->head; // Начинаем с головы списка
        while ($current->next !== null) { // Двигаемся до последнего узла
            $current = $current->next;
        }
        $current->next = $newNode; // Присоединяем новый узел в конец списка
    }

    // Добавление в начало списка O(1)
    // Просто меняем ссылку $head на новый узел, без обхода списка.
    public function prepend($val): void {
        $newNode = new ListNode($val, $this->head); // Создаем новый узел, указывая, что его "next" указывает на текущую голову
        $this->head = $newNode; // Теперь новый узел становится головой списка
    }

    // Удаление узла по значению O(n)
    // В худшем случае приходится проходить весь список, чтобы найти нужный узел.
    public function delete($val): void {
        if ($this->head === null) { // Если список пуст, выходим
            return;
        }

        if ($this->head->val === $val) { // Если голова содержит удаляемое значение
            $this->head = $this->head->next; // Перемещаем голову на следующий узел
            return;
        }

        $current = $this->head; // Начинаем с головы списка
        while ($current->next !== null) { // Двигаемся по списку
            if ($current->next->val === $val) { // Если следующий узел содержит удаляемое значение
                $current->next = $current->next->next; // Пропускаем этот узел, тем самым удаляя его
                return;
            }
            $current = $current->next; // Переход к следующему узлу
        }
    }

    // Поиск узла по значению O(n)
    // Нужно пройти список от головы до конца в худшем случае.
    public function search($val): ?ListNode {
        $current = $this->head; // Начинаем с головы списка
        while ($current !== null) { // Проходим по всему списку
            if ($current->val === $val) { // Если нашли узел с нужным значением
                return $current; // Возвращаем найденный узел
            }
            $current = $current->next; // Переход к следующему узлу
        }
        return null; // Если не нашли, возвращаем null
    }

    // Вывод списка O(n)
    // Нужно пройти все элементы списка один раз.
    public function printList(): void {
        $current = $this->head; // Начинаем с головы списка
        while ($current !== null) { // Пока есть узлы в списке
            echo $current->val . " -> "; // Выводим значение узла
            $current = $current->next; // Переход к следующему узлу
        }
        echo "NULL\n"; // Указываем конец списка
    }
}

// Пример использования

$list = new LinkedList(); // Создаем новый связный список

$list->append(10); // Добавляем 10 в конец списка
$list->append(20); // Добавляем 20 в конец списка
$list->prepend(5); // Добавляем 5 в начало списка
$list->printList(); // Вывод: 5 -> 10 -> 20 -> NULL

$list->delete(10); // Удаляем узел со значением 10
$list->printList(); // Вывод: 5 -> 20 -> NULL

$foundNode = $list->search(20); // Ищем узел со значением 20
echo $foundNode ? "Найден узел: " . $foundNode->val . "\n" : "Узел не найден\n"; // Вывод: Найден узел: 20

?>

```