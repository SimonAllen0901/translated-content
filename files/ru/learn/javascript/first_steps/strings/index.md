---
title: Работа с текстом — строки в JavaScript
slug: Learn/JavaScript/First_steps/Strings
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Первые_шаги/Math", "Learn/JavaScript/Первые_шаги/Useful_string_methods", "Learn/JavaScript/Первые_шаги")}}

Теперь мы обратим внимание на строки — в программировании так называют части текста. В этой статье мы рассмотрим все распространённые вещи, которые вы должны действительно знать о строках при изучении JavaScript, например, создание строк, экранирование кавычек в строках и объединение строк вместе.

| Необходимые навыки: | Базовая компьютерная грамотность, базовое понимание HTML и CSS, понимание что такое JavaScript. |
| ------------------- | ----------------------------------------------------------------------------------------------- |
| Цель:               | Знакомство с основами строк в JavaScript.                                                       |

## Сила слов

Слова очень важны для людей — это основа нашего общения. Интернет представляет собой преимущественно текстовую среду, предназначенную для того что бы люди общались и делились информацией, поэтому нам полезно иметь контроль над словами, которые появляются в нем. {{glossary ("HTML")}} предоставляет визуальную и смысловую структуру для нашего текста, {{glossary ("CSS")}} позволяет нам стилизовать его, а JavaScript содержит ряд функций для управления строками, создания пользовательских приветственных сообщений, при необходимости отображая нужные текстовые метки, сортируя элементы в желаемом порядке и многое другое.

Практически во всех программах, которые мы показали вам на данный момент, были задействованы некоторые манипуляции со строками.

## Строки — основы

С первого взгляда строки обрабатываются аналогично числам, но если копнуть глубже, вы увидите некоторые заметные отличия. Давайте начнём с ввода некоторых основных строк в [консоль разработчика](/ru/docs/Learn/Common_questions/What_are_browser_developer_tools), чтобы познакомиться с ними.

### Создание строки

1. Для начала введите следующие строки:

   ```js
   const string = "Революция не будет транслироваться по телевидению.";
   string;
   ```

2. Как и в случае с числами, мы объявляем переменную, инициализируя её строковым значением, а затем возвращаем значение. Единственное различие здесь в том, что при написании строки вам нужно окружить значение кавычками.
3. Если вы не сделаете этого или пропустите одну из кавычек, вы получите сообщение об ошибке. Попробуйте ввести следующие строки:

   ```js example-bad
   const badString = Тест;
   const badString = 'Тест;
   const badString = Тест';
   ```

   Эти строки не работают, потому что любая текстовая строка без кавычек считается именем переменной, именем свойства, зарезервированным словом или чем-то подобным. Если браузер не может найти его, возникает ошибка (например, «missing, before statement»). Если браузер может видеть, где начинается строка, но не может найти конец строки, как указано во 2-й строке, она жалуется на ошибку (с «unterminated string literal»). Если ваша программа выявляет такие ошибки, вернитесь назад и проверьте все свои строки, чтобы убедиться, что у вас нет пропущенных кавычек.

4. Следующий код будет выполнен только в том случае, если ранее была объявлена переменная `string` — убедитесь сами:

   ```js
   const badString = string;
   badString;
   ```

   В настоящее время строка `badString` имеет то же значение, что и строка `string`.

### Одиночные кавычки vs. Двойные кавычки

1. В JavaScript вы можете выбрать одинарные кавычки или двойные кавычки, чтобы обернуть ваши строки. Оба варианта будут работать нормально:

   ```js
   const sgl = "Одиночные кавычки.";
   const dbl = "Двойные кавычки.";
   sgl;
   dbl;
   ```

2. Существует очень мало различий между одиночными и двойными кавычками, и решение какие из них использовать в коде остаётся на ваше усмотрение. Однако вы должны выбрать один вариант и придерживаться его, иначе ваш код может выдать ошибку, особенно если вы используете разные кавычки в одной строке! Ниже приведён пример:

   ```js example-bad
   const badQuotes = 'Что происходит?";
   ```

3. Браузер будет считать, что строка не была закрыта, потому что в строке может появиться другой тип цитаты, который вы не используете, чтобы хранить ваши строки в переменных. Из примера можно понять, о чем идёт речь (в коде ошибок нет):

   ```js
   const sglDbl = 'Я не сказала "да", милорд…';
   const dblSgl = "Вы не сказали 'нет'… (королева, Бэкингем)";
   sglDbl;
   dblSgl;
   ```

4. Однако вы не можете включить один и тот же знак кавычки внутри строки, если он используется для их хранения. Ниже приведена ошибка, браузер ошибочно определяет место, где строка кончается:

   ```js example-bad
   const bigmouth = 'Жанна Д'Арк — народная героиня Франции.';
   ```

   Что приводит нас к следующей теме.

### Экранирование кавычек в строках

Чтобы исправить нашу предыдущую строку кода, нам нужно дать понять браузеру, что кавычка в середине строки не является меткой её конца. Экранирование символов означает, что мы делаем что-то с ними, чтобы убедиться, что они распознаются как текст, а не часть кода. В JavaScript мы делаем это, помещая обратную косую черту непосредственно перед символом. Введите эти строки:

```js
const bigmouth = "Жанна Д'Арк — народная героиня Франции.";
bigmouth;
```

Так лучше. Таким же образом можно экранировать и другие символы, например `"\`. Кроме того существуют специальные коды. Для дополнительной информации см. [Escape notation](/ru/docs/Web/JavaScript/Reference/Global_Objects/String#escape_notation).

## Конкатенация строк

1. Конкатенация — это новомодное программистское слово, которое означает «объединить». Объединение строк в JavaScript использует оператор плюс (+), тот же, который мы используем для сложения чисел, но в этом контексте он делает кое-что другое. Попробуем пример в нашей консоли.

   ```js
   const one = "Привет, ";
   const two = "как дела?";
   const joined = one + two;
   joined;
   ```

   Результат этой программы - это переменная `joined`, содержащая значение "Привет, как дела?".

2. В последнем случае мы просто объединим две строки вместе, но на самом деле, вы можете объединить столько строк, сколько хотите, до тех пор, пока вы ставите `+` между ними. Попробуйте это:

   ```js
   const multiple = one + one + one + one + two;
   multiple;
   ```

3. Вы также можете использовать сочетание переменных и фактических строк. Попробуйте это:

   ```js
   const response = one + "Я в порядке — " + two;
   response;
   ```

> **Примечание:** Когда вы вводите фактическую строку в свой код, заключённую в одинарные или двойные кавычки, она называется **строковым литералом**.

### Конкатенация строк в контексте

Давайте посмотрим на конкатенацию строк в действии — вот пример из предыдущего курса:

```html
<button>Press me</button>
```

```js
const button = document.querySelector("button");

button.onclick = function () {
  const name = prompt("Как тебя зовут?");
  alert("Привет, " + name + ", рад тебя видеть!");
};
```

{{ EmbedLiveSample('Конкатенация_строк_в_контексте', '100%', 50, "", "", "hide-codepen-jsfiddle") }}

Здесь мы используем функцию {{domxref ("Window.prompt ()", "Window.prompt ()")}} в строке 4, которая просит пользователя ответить на вопрос через всплывающее диалоговое окно, а затем сохраняет введённый текст внутри заданной переменной — в этом случае **`name`**. Затем мы используем функцию {{domxref ("Window.alert ()", "Window.alert ()")}} в строке 5 для отображения другого всплывающего окна, содержащего строку, которую мы собрали из двух строковых литералов и переменной `name`.

### Числа vs. строки

1. Итак, что происходит, когда мы пытаемся добавить (или конкатенировать) строку и число? Попробуем это в нашей консоли:

   ```js
   "Front " + 242;
   ```

   Вы можете ожидать, что это вызовет ошибку, но все работает отлично. Попытка представить строку как число на самом деле не имеет смысла, но число как строку — имеет, поэтому браузер довольно умно преобразует число в строку и объединяет две строки вместе.

2. Вы даже можете сделать это с двумя числами, вы можете заставить число стать строкой, обернув её в кавычки. Попробуйте следующее (мы используем оператор `typeof` для того, чтобы установить является ли переменная числом или строкой):

   ```js
   const myDate = "19" + "67";
   typeof myDate;
   ```

3. Если у вас есть числовая переменная, которую вы хотите преобразовать в строчную без внесения каких-либо иных изменений или строковую переменную, которую вы хотите преобразовать в число, вы можете использовать следующие две конструкции:

   - Объект {{jsxref ("Number")}} преобразует всё переданное в него в число, если это возможно. Попробуйте следующее:

     ```js
     const myString = "123";
     const myNum = Number(myString);
     typeof myNum;
     ```

   - С другой стороны, каждое число имеет метод, называемый [`toString()`](/ru/docs/Web/JavaScript/Reference/Global_Objects/Number/toString), который преобразует его в эквивалентную строку. Попробуй это:

     ```js
     const myNum = 123;
     const myString = myNum.toString();
     console.log(typeof myString);
     ```

Эти конструкции могут быть действительно полезны в некоторых ситуациях. Например, если пользователь вводит число в текстовое поле формы, данные будут распознаны как строка. Однако, если вы хотите добавить это число к чему-то, вам понадобится его значение, поэтому вы можете передать его через `Number()`, чтобы справиться с этим. Именно это мы сделали в нашей [Number Guessing Game](https://github.com/mdn/learning-area/blob/master/javascript/introduction-to-js-1/first-splash/number-guessing-game.html#L63), в строке 59.

## Совмещение строк с различными выражениями

Вы можете совмещать выражения JavaScript в литералы шаблона, а также простые переменные, и результаты будут включены в конечную строку:

```js
const song = "Fight the Youth";
const score = 9;
const highestScore = 10;
const output = `Мне нравится песня ${song}. Я оценил её на ${
  (score / highestScore) * 100
}%.`;
console.log(output); // "Мне нравится песня Fight the Youth. Я оценил её на 90%."
```

## Многострочный текст

Литералы шаблона учитывают разрывы строк в исходном коде, поэтому вы можете писать текст в несколько строчек, например:

```js
const output = `Мне нравится эта песня. 
  Я оценил её на 90%.`;
console.log(output);

/*
  Мне нравится эта песня.
  Я оценил её на 90%.
  */
```

Чтобы получить эквивалентный вывод с использованием обычной строки, вам придется включить в строку символы переноса строки (`\n`):

```js
const output = "Мне нравится эта песня.\nЯ оценил её на 90%.";
console.log(output);

/*
  Мне нравится эта песня.
  Я оценил её на 90%.
  */
```

Смотри нашу справочную страницу [литералов шаблонов](/ru/docs/Web/JavaScript/Reference/Template_literals) для получения дополнительных примеров и подробной информации о расширенных функциях.

## Заключение

Итак, это основы строк, используемых в JavaScript. В следующей статье мы рассмотрим некоторые из встроенных методов, доступных для строк в JavaScript и то, как мы можем использовать их для управления нашими строками только в той форме, в которой мы хотим.

{{PreviousMenuNext("Learn/JavaScript/Первые_шаги/Math", "Learn/JavaScript/Первые_шаги/Useful_string_methods", "Learn/JavaScript/Первые_шаги")}}