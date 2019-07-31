
让twig和vue 1.x template一起工作


先加载本词法分析器：
```php

        // 启用使twig  vuetemplate 支持多语言
        $twig = $this->getContainer()->get("twig");
        $lexer = $this->getContainer()->get("common_twig_lexer");
        $twig->setLexer($lexer);

```

> PS: 对于symfony需要在controller里对twig设置lexer，建议在覆盖controller自带的setContainer()方法里处理，原因是symfony的twig bundle需要compile各个bundle拓展



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






