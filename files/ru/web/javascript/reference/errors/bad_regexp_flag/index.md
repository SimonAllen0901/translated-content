---
title: 'SyntaxError: invalid regular expression flag "x"'
slug: Web/JavaScript/Reference/Errors/Bad_regexp_flag
---

{{jsSidebar("Errors")}}

## Сообщение

```
SyntaxError: invalid regular expression flag "x" (Firefox)
SyntaxError: Invalid regular expression flags (Chrome)
```

## Тип ошибки

{{jsxref("SyntaxError")}}

## Что пошло не так?

В коде есть недопустимые флаги регулярных выражений. Литерал в регулярном выражении, который содержит шаблон заключённый между двумя слешами, флаги определяются после второго флага. Они также могут быть объявлены в конструкторе функции {{jsxref("RegExp")}} object (второй параметр). Флаги регулярного выражения могут быть использованы отдельно или вместе в любой очерёдности, но в ECMAScript их только пять.

Чтоб включить флаг в регулярное выражение, используйте синтаксис:

```js
var re = /pattern/flags;
```

или

```js
var re = new RegExp("pattern", "flags");
```

Флаги регулярного выражения

| Флаг | Описание                                                                                                                         |
| ---- | -------------------------------------------------------------------------------------------------------------------------------- |
| `g`  | Глобальный поиск.                                                                                                                |
| i    | Нечувствительный к регистру поиск.                                                                                               |
| m    | Поиск по всем строкам.                                                                                                           |
| u    | Unicode; обрабатывать шаблон как последовательность кода Unicode                                                                 |
| y    | Выполняет «липкий» поиск, который будет начинаться с текущей позиции в целевой строке. См. {{jsxref("RegExp.sticky", "sticky")}} |

## Примеры

Существует только пять действительных флагов регулярных выражений.

```js example-bad
/foo/bar;

// Ошибка синтаксиса: недействительный флаг "b" для регулярного выражения
```

Вы намеревались создать регулярное выражение? Выражение, содержащее два слеша, интерпретируется как литерал регулярного выражения.

```js example-bad
let obj = {
  url: /docs/Web
};

// Ошибка синтаксиса: недействительный флаг "W" для регулярного выражения
```

Или вы хотели создать строку вместо этого? Добавьте одинарные или двойные кавычки, чтобы создать строковый литерал.

```js example-good
let obj = {
  url: "/docs/Web",
};
```

### Действительные флаги регулярного выражения

Взгляните на таблицу выше, где представлены пять действительных флагов регулярного выражения, которые разрешены в JavaScript

```js example-good
/foo/g;
/foo/gim;
/foo/uy;
```

## Смотрите также

- [Regular expressions](/ru/docs/Web/JavaScript/Guide/Regular_Expressions)
- [XRegEx flags](http://xregexp.com/flags/) – библиотека регулярного выражения, которая предоставляет четыре новых флага (`n`, `s`, `x`, `A`)