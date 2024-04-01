#seo #YMetrika

Не забыть проверить трекинг YM!
номер YM 94510740
событие YM reachGoal
трекинг класс .tracking_email_copy
```html
<script>
//отслеживаем копирование по Ctrl+C и через контекстное меню
function handleCopyEvent(event) {
    if (window.getSelection().toString().includes('@')) {
        ym(94510740, 'reachGoal', 'email_copy');
    }
}

//отслеживаем копирование по клику "Копировать адрес электроной почты" из контекстного меню
function handleMailtoRightClick(event) {
    if (event.target.closest('[href^=mailto]')) {
        ym(94510740, 'reachGoal', 'email_copy');
    }
}

//отслеживаем открытие почтовой программы по клику
function handleMailClick() {
    if (event.target.closest('[href^=mailto]')) {
        ym(94510740, 'reachGoal', 'email_copy');
    }
}

/* js событие copy регистируется не там где курсор закончил выделение, а там где курсор начал выделение.
  Поэтому якорный класс tracking_email_copy набо вешать на весь блок , где курсор может начать движение выделение.*/
const emailBlockList = document.querySelectorAll('.tracking_email_copy');
for (let emailBlock of emailBlockList) {
    emailBlock.addEventListener('copy', handleCopyEvent);
    emailBlock.addEventListener('contextmenu', handleMailtoRightClick);
    emailBlock.addEventListener('click', handleMailClick);
}

</script>
```