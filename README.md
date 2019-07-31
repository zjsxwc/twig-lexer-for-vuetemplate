
让twig和vue 1.x template一起工作


先加载本词法分析器：
```php

        // 启用使twig  vuetemplate 支持多语言
        $twig = $this->getContainer()->get("twig");
        $lexer = $this->getContainer()->get("common_twig_lexer");
        $twig->setLexer($lexer);

```

> PS: 对于symfony需要在写一个controller event listener 或 subscriber 每次在controller之前设置 twig 的 lexer，因为symfony的twig会经过一系列的初始化和compile，不能直接无脑覆盖或者在kernel boot后直接设置lexer



然后我们在twig里写vue1.x模板，再在vue1.x模板里写twig

input twig:
```
{% set var = 'var' %}
{% set var1 = 'var1value' %}
{% set var2 = 'var2value' %}

{% vuetemplate %}
    hello
    test cat:
    <%= var ~ var2 %>
    test trans
    <%= "服装"|trans %>
     %= hahahahah %>
    print:
    <%= var1 %>
    vue
    {{ sdsdf }}

    <%= "工厂"|trans %>
    <%= 1+2 %>
    666
{% endvuetemplate %}


```

output:
```html
    hello
    test cat:
    varvar2value
    test trans
    Clothing
     %= hahahahah %>
    print:
    var1value
    vue
    {{ sdsdf }}

    Factory
    3
    666
```






