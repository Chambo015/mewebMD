Модули ESM всегда базируются на файлах: один файл — один модуль.

ESM всегда работают в строгом режиме и не требуют включения директивы `"use strict"` в начало файла.
Директивы `export` и `import` :

* **`#!js export`** отмечает переменные и функции, которые должны быть доступны вне текущего модуля. 
    - Обычно называемыми открытым API. 
    - Если нечто определяется в модуле, но не экспортируется, то оно остается скрытым. 
    - `export` должна находиться в области видимости верхнего уровня; она не может располагаться внутри любого другого блока или функции.
* **`#!js import`** позволяет импортировать функциональность из других модулей.
    - модули ESM - существуют только в единственном экземпляре, который создается при первом импортировании, 
    а все последующие команды импортирования просто получают ссылку на тот же экземпляр.
    - необходимо явно сказать браузеру, что скрипт является модулем, при помощи атрибута `#!HTML <script type="module">`.
    - Отложенное (deferred) выполнение по умолчанию.
    - Модули не работают локально. Только через HTTP(s)

=== "📁 sayHi.js"

    ``` js
    export function sayHi(user) {
        console.log(`Hello, ${user}!`);
    }
    ```

=== "📁 main.js"

    ``` js
    import {sayHi} from './sayHi.js';
    // Директива import загружает модуль по пути ./sayHi.js относительно текущего файла 
    // и записывает экспортированную функцию sayHi в соответствующую переменную.

    sayHi('John'); // Hello, John!
    ```

=== ":material-console: console"
    "📁 main.js"

    Hello, John!

В реальной жизни часто используется сборщик Webpack, чтобы объединить модули: для производительности и других «плюшек».

## Модуль выполняется только один раз.
Если при запуске модуля возникают побочные эффекты, например выдаётся сообщение(алерт), 
то импорт модуля в нескольких местах покажет его только один раз – при первом импорте:

=== "📁 alert.js"

    ``` js
    alert("Модуль выполнен!");
    ```

=== "📁 1.js"

    ``` js
    import `./alert.js`; // Модуль выполнен!
    ```

=== "📁 2.js"

    ``` JavaScript   
    import `./alert.js`; // (ничего не покажет)
    ```

Генерируется экспорт и после передаётся всем импортёрам, поэтому, если что-то изменится в импортируемом объекте , то другие модули тоже увидят эти изменения. <br>
Такое поведение позволяет *конфигурировать* модули при первом импорте. Мы можем установить его свойства один раз, и в дальнейших импортах он будет уже настроенным.

=== "📁 admin.js"

    ``` js
    export let admin = { };

    export function sayHi() {
        console.log(`Ready to serve, ${admin.name}!`);
    }
    ```

=== "📁 init.js"

    ``` js
    import {admin} from './admin.js';
    admin.name = "Pete";
    ```

=== "📁 main.js"

    ``` JavaScript   
    import {admin, sayHi} from './admin.js';
    sayHi(); // Ready to serve, Pete!
    ```

## Именованный импорт/экспорт
`export` перед переменной, функции или класса.
```js 
export let months = ['Jan', 'Feb']
export const MODULES_BECAME_STANDARD_YEAR = 2015;
export const foo = 'foo', bo = 'bo';
export function counter() { /* ... */ } // без ; в конце
export class User { /* ... */ } // без ; в конце
// Не ставится точка с запятой после экспорта класса/функции
```

Группированный экспорт
```js 
function sayHi() {...}
function sayBye() {...}

export {sayHi, sayBye}; // список экспортируемых переменных
```

Импорт
```js
import { counter, awesomeValue } from './modulePath/index.js';

counter()
```
## Импорт/экспорт «как»
Импортировать всё как объект
```JavaScript
import * as say from './say.js';

say.sayHi('John');
say.sayBye('John');
```

Импортировать под другими именами
```js 
import {sayHi as hi, sayBye as bye} from './say.js';

hi('John'); // Hello, John!
bye('John'); // Bye, John!
```

Аналогичный синтаксис существует и для `export`.

=== "📁 say.js"

    ``` js
    export {sayHi as hi, sayBye as bye};

    // Теперь hi и bye – официальные имена для внешнего кода, 
    // их нужно использовать при импорте:
    ```

=== "📁 main.js"

    ``` js
    import * as say from './say.js';

    say.hi('John'); // Hello, John!
    say.bye('John'); // Bye, John!
    ```

## Импорт/экспорт по умолчанию
В случае, когда из файла модуля экспортируется только одна сущность, удобнее использовать экспорт по умолчанию. <br>
Ставим `export default` перед тем, что нужно экспортировать (функция или класс), но запрещено ставить перед переменной.

=== "📁 user.js"

    ``` js
    export default class User { // просто добавьте "default"
        constructor(name) {
            this.name = name;
        }
    }
    ```

=== "📁 main.js"

    ``` js
    // для экспорта по умолчанию мы выбираем любое имя при импорте:
    import Admins from './user.js'; // не {Admins}, просто Admins

    new Admins('John');
    ```

Запомним: фигурные скобки необходимы в случае

- именованных экспортов(`import {User} from ...`), 
- для `export default` они не нужны (`import User from ...`)

Поскольку нету ограничения между именованным экспортом и экспортом по умолчанию, es6 позволяет использовать оба в одном модуле:

=== "📁 user.js"

    ``` js
    export default class User {
    constructor(name) {
        this.name = name;
    }
    }
    // или
    export {User as default};
    // или
    export default User;


    export function sayHi(user) {
    alert(`Hello, ${user}!`);
    }
    ```

=== "📁 main.js"

    ``` js
    import {default as User, sayHi} from './user.js';
    ```

Если импортируем всё как объект `import *`, тогда его свойство `default` – будет экспортом по умолчанию

## Реэкспорт
Когда вы захотите объединить модули вместе. Объединив несколько подмодулей в один родительский модуль.
``` title="Структура файлов"
modules/
  shapes.js
  shapes/
    circle.js
    square.js
    triangle.js
```

=== "📁 shapes.js"

    дополнительный модуль с именем `shapes.js`, который собирает функциональность `circle.js`, `square.js` и `triangle.js` вместе.

    ``` js
    export { Square } from './shapes/square.js';
    export { Triangle } from './shapes/triangle.js';
    export { Circle } from './shapes/circle.js';
    ```
=== "📁 main.js"

    теперь в файле `main.js` мы можем получить доступ ко всем трём классам модулей в одной строке

    ``` js
    import { Square, Circle, Triangle } from './modules/shapes.js';
    ```

!!! Info "Примечание"

    Экспорты, указанные в `shape.js`, по сути перенаправляются через файл и на самом деле там не существуют, поэтому вы **не сможете** написать какой-либо полезный связанный код внутри того же файла.

## Динамическая загрузка модулей
Это позволяет вам динамически загружать модули только тогда, когда они необходимы, вместо того, чтобы загружать всё заранее <br>
Обычные методы «статические» им нельзя динамически задать путь или импортировать по условию. <br>
Поддержка динамической загрузки модулей позволяет вызывать `import()` в качестве функции, передав ей аргументом путь к модулю. Данный вызов возвращает `Promise`, который резолвится **объектом** модуля, содержащий все его экспорты.

=== "📁 say.js"

    ``` js
    export function hi() {
        alert(`Привет`);
    }

    export function bye() {
        alert(`Пока`);
    }

    export default function() {
        alert("Module loaded (export default)!");
    }
    ```

=== "📁 main.js"

    ``` js
    let path = './say.js'
    async function load() {
        let say = await import(path);
        say.hi(); // Привет!
        say.bye(); // Пока!
        say.default(); // Модуль загружен (экспорт по умолчанию)!
    }

    load()
    ```

!!! Info "Примечание"

    Динамический импорт работает в обычных скриптах, он не требует указания `script type="module"`. <br>
    Нельзя скопировать `import` в другую переменную или вызвать при помощи `.call/apply`. Это не функция.
