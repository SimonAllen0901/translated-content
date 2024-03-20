---
title: Абстракция
slug: Glossary/Abstraction
---

{{GlossarySidebar}}

Абстракция в {{Glossary("computer programming", "программировании")}} — это способ снизить сложность и повысить эффективность проектирования и реализации программного обеспечения за счёт сокрытия технической сложности за более простым {{Glossary("API")}}.

## Преимущества абстракции

- Помогает избежать написания низкоуровневого кода.
- Упрощает повторное использование кода и позволяет избежать дублирования.
- Даёт возможность изменять внутреннюю реализацию программы, не затрагивая пользователей.
- Помогает повысить безопасность приложения или программы, поскольку пользователям доступны только нужные детали.

## Пример

```js
class ImplementAbstraction {
  // метод присваивает значения внутренним свойствам
  set(x, y) {
    this.a = x;
    this.b = y;
  }

  display() {
    console.log("a = " + this.a);
    console.log("b = " + this.b);
  }
}

const obj = new ImplementAbstraction();
obj.set(10, 20);
obj.display();
// a = 10
// b = 20
```