#php/основы

Ссылки в PHP - средство доступа к одному и тому же содержимому переменной под разными именами. Ссылки в PHP не похожи на указатели языка C, например, нельзя выполнять над ссылками адресную арифметику. Cсылки в PHP - псевдонимы в таблице имён переменных.

```
$x = 1;
$y = 2;
$x = $y; // $x теперь содержит значение переменной $y
$z = &$y; // $z содержит ссылку на $y. Изменение значения $z затронет значение $y и наоборот.
// Значение $x остается неизменным.
```

