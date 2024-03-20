---
title: CRLF
slug: Glossary/CRLF
---

{{GlossarySidebar}}

CR и LF это [управляющие символы](https://en.wikipedia.org/wiki/Control_character) или [байт-код](https://en.wikipedia.org/wiki/Bytecode) которые можно использовать для обозначения разрыва строки в текстовых файлах.

- CR = **Возврат каретки (Carriage Return)** (`\r`, `0x0D` в шестнадцатеричной, 13 в десятичной системе счисления) — перемещает курсор в начало строки, не переходя на следующую строку.
- LF = **Перевод строки (Line Feed)** (`\n`, `0x0A` в шестнадцатеричной, 10 в десятичной системе счисления — перемещает курсор на следующую строку, не возвращаясь в начало строки.

CR, за которым сразу следует LF (CRLF, `\r\n`, или `0x0D0A`) перемещает курсор на следующую строку и затем перемещает его в начало строки.