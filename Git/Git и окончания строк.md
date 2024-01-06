---
aliases:
  - CR и LF в Git
---
Окончание строк в текстовых файлов в
WIndows - `CR` `LF`
Linux-based - `LF`

Так как git изначально Linux-based,  git конвертирует все окончания строк в  `LF`  c помощью опции 
`Git core.autocrlf = true`
По дефолту она не выставлена, ее надо выставлять для всех Windows систем при работе с git. 

Тогда цепочка преобразований для windows будет выглядеть так
```
 add, commit       База        checkout
-------------->  данных Git  -------------->
 (CRLF -> LF)       (LF)      (LF -> CRLF)
```