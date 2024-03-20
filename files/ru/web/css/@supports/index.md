---
title: "@supports"
slug: Web/CSS/@supports
---

{{ CSSRef() }}

## Описание

[CSS](/ru/docs/Web/CSS) [@-правило](/ru/docs/Web/CSS/At-rule) **`@supports`** связывает набор вложенных правил в блоке CSS-кода, ограниченном фигурными скобками, с условием, представляющим собой одно или несколько проверочных объявлений в виде пар `свойство: значение`, объединенных операторами `and`, `or` или `not` (логические И, ИЛИ, НЕ). Такое условие называется _supports-условием_.

`@supports` позволяет CSS-коду выполнять _feature query_ (запрос на проверку поддержки различных возможностей CSS в браузере).

Правило `@supports` может быть использовано не только на верхнем уровне вложенности CSS, но и внутри блоков любых других [@-правил](/ru/docs/Web/CSS/At-rule#условные_групповые_правила). Доступ к нему можно получить с помощью интерфейса объектной модели CSS {{domxref("CSSSupportsRule")}}.

## Синтаксис

supports-условие состоит из одного или нескольких CSS-объявлений в сочетании с различными логическими операторами. Приоритет операторов может быть переопределён при помощи круглых скобок.

### Синтаксис объявления

В простейшем случае, supports-условие представляет собой одно CSS-объявление, то есть, пару вида `свойство: значение`. Следующее выражение

```css
( transform-origin: 5% 5% )
```

вернёт `true`, если {{ cssxref("transform-origin") }} поддерживает синтаксис, в котором значение `5% 5%` является допустимым.

CSS-объявление всегда заключается в круглые скобки.

### Оператор not

Оператор `not` (логическое НЕ) может стоять перед любым выражением. `not` возвращает значение, противоположное тому, которое вернуло выражение в круглых скобках после `not`. Следующее выражение

```css
not ( transform-origin: 10em 10em 10em )
```

вернёт true, если {{ cssxref("transform-origin") }} **не** поддерживает синтаксис, в котором значение `10em 10em 10em` является допустимым.

Как и другие операторы, `not` может быть применен к любому составному выражению. Следующие примеры являются синтаксически корректными:

```css
not ( not ( transform-origin: 2px ) )
(display: flexbox) and ( not (display: inline-grid) )
```

**Примечание:** Нет необходимости заключать оператор `not` в круглые скобки на верхнем уровне вложенности. Однако, скобки обязательны, если `not` используается в сочетании с другими операторами (`and` или `or`).

### Оператор and

Оператор `and` (логическое И или _конъюнкция_) объединяет два выражения и возвращает `true` тогда и только тогда, когда оба выражения истинны. В следующем примере всё выражение вернет true только в том случае, если оба выражения в круглых скобках одновременно истинны.

```css
(display: table-cell) and (display: list-item)
```

В одном выражении может использоваться несколько операторов `and`; при этом нет необходимости использовать дополнительные круглые скобки. Так, выражение

```css
(display: table-cell) and (display: list-item) and (display:run-in)
```

эквивалентно следующему:

```css
(display: table-cell) and ((display: list-item) and (display:run-in))
```

### Оператор or

Оператор `or` (логическое ИЛИ или _дизъюнкция_) объединяет два выражения и возвращает `true`, если истинно хотя бы одно из них. В следующем примере вся строка вернёт `true`, если хотя бы одно из выражений, заключенных в круглые скобки, истинно:

```css
( transform-style: preserve ) or ( -moz-transform-style: preserve )
```

В одном выражении может использоваться несколько операторов `or`; при этом нет необходимости использовать дополнительные скобки. Так, выражение

```css
( transform-style: preserve ) or ( -moz-transform-style: preserve ) or
( -o-transform-style: preserve ) or ( -webkit-transform-style: preserve  )
```

эквивалентно следующему:

```css
( transform-style: preserve-3d ) or (( -moz-transform-style: preserve-3d ) or
(( -o-transform-style: preserve-3d ) or ( -webkit-transform-style: preserve-3d  )))
```

> **Примечание**: если в выражении используются оба оператора, `and` и `or`, **необходимо использовать скобки**, чтобы указать порядок применения логических операторов. Если скобки не используются, выражение считается некорректным и всё правило `@support` будет полностью проигнорировано.

### Формальный синтаксис

{{csssyntax}}

## Примеры

### Тестирование заданного свойства

```css
@supports (animation-name: test) {
    … /* размещенные в этом блоке правила будут применены, если браузером поддерживаются свойства анимации без префиксов */
    @keyframes { /* @supports является условным правилом группировки, оно может содержать в себе другие @-правила */
      …
    }
}
```

### Тестирование заданного свойства или его версии с префиксом

```css
@supports ( (perspective: 10px) or (-moz-perspective: 10px) or (-webkit-perspective: 10px) or
            (-ms-perspective: 10px) or (-o-perspective: 10px) ) {
    … /* размещенные в этом блоке правила будут применены, если браузером поддерживаются свойства 3D трансформации, хотя бы с префиксами */
}
```

### Тестирование неподдерживаемого или специфического свойства

```css
@supports not ((text-align-last:justify) or (-moz-text-align-last:justify) ){
    … /* в этом блоке могут быть размещены CSS-правила, имитирующие правило `text-align-last: justify` */
}
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- CSSOM-класс {{ domxref("CSSSupportsRule") }}, а также метод {{ domxref("CSS.supports") }}, позволяющий использовать `@supports`-проверки в JavaScript.