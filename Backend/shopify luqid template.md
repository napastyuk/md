## Комментарии

все символы, заключенные между 

&#123;&#37; comment &#37;&#125; some comment  &#123;&#37; endcomment &#37;&#125;

будут проигнорированы и не будут обрабатываться с помощью языка Liquid.
тоже самое с тегами 

&#123;&#37; literal &#37;&#125; some comment  &#123;&#37; endliteral &#37;&#125;

если в комментариях надо разместить luqid теги то можно воспользоваться тегом row
```
{% raw %} any content with curlky brackets {% endraw %}
```

#shopify #luquid 