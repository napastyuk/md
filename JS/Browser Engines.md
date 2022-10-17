на основе [wiki](https://en.wikipedia.org/wiki/Comparison_of_browser_engines)

## Актуальные

### Движок - ==Blink== / Браузер - ==Chromium==
Форк от  Webkit в 2013 году. Развивается Google.
Включает в себя
-   HTML и CSS движки
-   ==V8== JS движок

### Движок - ==Webkit== / Браузер - ==Safari==
Форк от KDE в 2001 году. Развивается Apple
Включает в себя
- ==WebCore== (первоначально KDE HTML / KHTML)  HTML, CSS и SVG движки
- ==JavaScriptCore== (первоначально KDE JavaScript / KJS) JS движок. В СМИ что бы показывать улутшения в производительности движок в разное время называли ==SquirrelFish==, ==SquirrelFish Extreme==, ==Nitro==, ==Nitro Extreme==, но репозиторий оставался со старым именем.  

### Движок - ==Gecko== / Браузер - ==Firefox==
Форк от ==Netscape== в 1998 году. Развивается Mozilla Foundation.
Включает в себя
- ==Quantum== с 2017 года FF обновляет части связаные с видео рендерингом (HTML, CSS, UI) портируя их из экспериментального пректа ==Servo==. 
- ==SpiderMonkey== JS движок

----------

## Более не поддерживаются

### Движок - ==Presto== / Браузер - ==Opera==
Развивался компаний Opera c 2003 по 2013. Код закрыт. 
Использовали несколько JS движков. Перед закрытием это был *Carakan*

### Движок - ==Trident== / Браузер - Internet Explorer
Развивался компаний Microsoft c 1997 по 2015. Код закрыт. 
Использовал ==Chakra== для JS движка


### Движок - ==EdgeHTML== / Браузер - ==Edge==
Форк от ==Trident==. Развивался компаний Microsoft c 2015 по 2020. Код закрыт. 
Использовал ==Chakra== для JS движка