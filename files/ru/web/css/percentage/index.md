---
title: <percentage>
slug: Web/CSS/percentage
---

{{CSSRef}}

[CSS](/ru/docs/Web/CSS) [тип данных](/ru/docs/Web/CSS/CSS_Types) **`<percentage>`** представляет значение в процентах. Оно часто используется, чтобы определить размер относительно родительского элемента. Проценты используются в различных свойствах, таких как {{Cssxref("width")}}, {{Cssxref("height")}}, {{Cssxref("margin")}}, {{Cssxref("padding")}}, и {{Cssxref("font-size")}}.

> **Примечание:** Наследуются рассчитанные значения. Таким образом, даже если процентное значение используется на родительском элементе, настоящее значение (такое, как пиксели для типа данных {{cssxref("&lt;length&gt;")}}) будет доступно в унаследованном свойстве, а не значение в процентах.

## Синтаксис

Тип данных `<percentage>` состоит из {{cssxref("&lt;number&gt;")}}, за которым следует знак процента (`%`). Так же впереди может стоять знак `+` или `-`, хотя отрицательные значения допустимы не во всех свойствах. Как и у всех единиц измерения CSS между символом процента и числом нет пробельного символа.

## Интерполяция

При анимировании значения типа данных `<percentage>` интерполируются как настоящие числа с плавающей запятой. Скорость интерполяции зависит от функции времени, с которой используется анимация.

## Примеры

### Ширина и левый отступ

```html
<div style="background-color:blue;">
  <div style="width:50%; margin-left:20%; background-color:lime;">
    Width: 50%, Left margin: 20%
  </div>
  <div style="width:30%; margin-left:60%; background-color:pink;">
    Width: 30%, Left margin: 60%
  </div>
</div>
```

HTML код выше будет выглядеть так:

{{EmbedLiveSample('Ширина_и_левый_отступ', '600', 140)}}

### Размер шрифта

```html
<div style="font-size:18px;">
  <p>Full-size text (18px)</p>
  <p><span style="font-size:50%;">50%</span></p>
  <p><span style="font-size:200%;">200%</span></p>
</div>
```

HTML код выше будет выглядеть так:

{{EmbedLiveSample('Размер_шрифта', 'auto', 160)}}

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}