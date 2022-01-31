## Laravel

@if (isset($isHome) && $isHome) - если переменная существует и она true


{{dump($variable)}} - выполняет var_dump($var)
{{dd($variable)}} - выполняет var_dump($var) + die()


## Как работает @yield в Laravel

Вы создаете шаблон (Назовем его, first.blade.php), вставляете в него @yield():
<div class="example">
    @yield('content')
</div>

Затем вы наследуете от этого шаблона другой шаблон (second.blade.php) и прописываете в него конструкцию @section() с тем же именем, что указали у yield:
@extends('first')

@section('content')
    Hello, World!
@endsection

Теперь вы рендерите второй шаблон:
class Controller
{
    public function indexAction()
    {
        return view('second');
    }
}

Рендерится вот такая страница:
<div class="example">
    Hello, World!
</div>

Таким образом, получается, что @yield() служит своеобразным маркером, на место которого будет подставлено содержимое @section() дочернего шаблона.

