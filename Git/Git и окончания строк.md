---
aliases:
  - CR и LF в Git
---
`Git core.autocrlf = true`
Надо выставлять для всех Windows систем при работе с git. 
Тогда цепочка преобразований для windows будет выглядеть так
```
 add, commit       База        checkout
-------------->  данных Git  -------------->
 (CRLF -> LF)       (LF)      (LF -> CRLF)
```