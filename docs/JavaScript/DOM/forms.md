## Свойства HTMLFormElement
Тег `<form>` представлен экземпляром `HTMLFormElement`. Тип `HTMLFormElement` наследуется от `HTMLElement`, от которого получает
все стандартные свойства. К ним он добавляет свои свойства и методы: 

Свойство        | Описание
--------------- | ---------------------
`acceptCharset` | Кодировки, которые может обрабатывать сервер (эквивалентен атрибуту `accept-charset`)
`action`        | URL-адрес для отправки запроса (эквивалентен атрибуту `action`). Свойство можно получить или установить. Например `form.action = '/cgi-bin/publish'`
`elements`      | Коллекция `HTMLFormControlsCollection` содержит все элементы управления формы. Это живая коллекция; если элементы управления формы добавляются или удаляются из формы, эта коллекция будет обновляться. Коллекции находятся в том же порядке, в котором они появляются в форме - это называется *древовидным порядком*
`length`        | Свойство только для чтения, которое возвращает количество элементов управления в элементе `<form>`.
`enctype`       | Тип кодировки запроса (эквивалентен атрибуту `enctype`)
`method`        | Тип отправляемого HTTP-запроса, `get` или `post` (эквивалентен атрибуту `method`). Если явно не указан, по умолчанию используется метод `get`.
`name`          | Представляет имя текущего элемента `<form>` в виде строки. (эквивалентен атрибуту `name`)
`target`        | Имя окна, используемого для отправки запроса или получения ответа (эквивалентен атрибуту `target`)

??? example "Элементы, включенные `HTMLFormElement.elements` и `HTMLFormElement.length`"

    * `<button>`
    * `<fieldset>`
    * `<input>` (за исключением тех, чьи `type` значения "image")
    * `<object>`
    * `<output>`
    * `<select>`
    * `<textarea>`

## Навигация: формы и элементы
Ссылку на элемент `<form>` можно получить разными способами:

* Часто назначают атрибут `id`, что позволяет использовать метод `getElementById()`
* Формы в документе входят в специальную коллекцию `document.forms` мы можем использовать для получения формы как её имя, так и порядковый номер в документе.
```JavaScript
document.forms.my - форма с именем "my" // атрибут name="my"
document.forms[0] - первая форма в документе
document.forms["my name"] - если имя содержит пробелы
```

Когда мы уже получили форму, любой элемент формы доступен в именованной коллекции `form.elements`
```JavaScript
let form = document.forms[0]

// Получение первого поля формы
let field1 = form.elements[0];

// Получение поля с именем "textbox"
let field2 = form.elements["textbox"];

// Получение количество полей
let fieldCount = form.elements.length;
```
!!! info "Элементы с одним именем возвращают коллекцию"

    Может быть несколько элементов с одним и тем же именем, это часто бывает с кнопками-переключателями `radio`.
    В этом случае `form.elements[name]` является коллекцией, например:
    ```html
    <form>
        <input type="radio" name="age" value="10">
        <input type="radio" name="age" value="20">
    </form>
    <script>
        let form = document.forms[0];

        // коллекция из радио
        let ageElems = form.elements.age;
    </script>
    ```

Все элементы управления формы, как бы глубоко они не находились в форме, доступны в коллекции `form.elements`.

```html
<form id="form">
    <fieldset name="userFields">
        <legend>info</legend>
        <input name="login" type="text">
    </fieldset>
</form>

<script>
    form.elements.login; // <input name="login">

    let fieldset = form.elements.userFields; // HTMLFieldSetElement

    // мы можем достать элемент по имени как из формы, так и из fieldset с ним
    fieldset.elements.login == form.elements.login; // true (1)
</script>
```

1.  Форма может содержать один или несколько элементов `<fieldset>` внутри себя. Они также поддерживают свойство `elements`, в котором находятся элементы управления внутри них.

!!! info "Сокращенная форма"

    Есть более короткая запись, вместо `form.elements.login` мы можем написать `form.login`

Для любого элемента **обращение к родителю**(форме) доступно через `element.form`
```html
<form id="form">
    <input type="text" name="login">
</form>

<script>
    // form -> element (к дочерним)
    let login = form.login; 

    // element -> form (к родителю)
    login.form; // HTMLFormElement
</script>
```

## Свойства Элементов формы
За исключением элемента `<fieldset>` все поля форм имеют несколько общих свойств:

* `disabled `- `true/false` Указывает отключено ли поле
* `form` - указывает на форму предка, к которой относится поле
* `name` - имя поля
* `readOnly` - `true/false` Указывающее доступна ли поле только для чтения
* `tabIndex` - порядок перехода по нажатию клавиши табуляции.
* `type` - тип поля (`checkbox`, `radio` и т.д.)
* `value` - значение поля, отправляемого серверу.

!!! note ""

    Все свойства кроме `form`, можно изменять

* `checked` - `true/false` для чекбоксов и переключателей

### select и option - раскрывающийся список

`#!html <select>` имеет 3 важных свойства чтобы **получить значение**:

* `select.options` – коллекция из подэлементов `<option>`,
* `select.value` – значение **выбранного в данный момент** `<option>`,
* `select.selectedIndex` – номер **выбранного** `<option>`.


Три разных способа **установить значение** в `<select>`:
```html
<select id="select">
  <option value="apple">Яблоко</option>
  <option value="pear">Груша</option>
  <option value="banana">Банан</option>
</select>

<script>
  // Список с возможностью одиночного выбора
  select.type // "select-one" 
  // все три строки делают одно и то же
  select.options[2].selected = true; // (1)
  select.selectedIndex = 2; // (2)
  select.value = 'banana'; // (3)
</script>
```

1.  Находим соответствующий элемент `<option>` и устанавливаем в `option.selected` значение `true`.
2.  Установить в `select.selectedIndex` номер нужного `<option>`.
3.  Установить в `select.value` значение нужного `<option>`.

`<select>` позволяет нам выбрать несколько вариантов одновременно, если у него стоит атрибут `multiple`.
```HTML
<select id="select" multiple>
  <option value="blues" selected>Блюз</option>
  <option value="rock" selected>Рок</option>
  <option value="classic">Классика</option>
</select>

<script>
  // Список множественного выбора
  select.type // "select-multiple" 
  // получаем все выбранные значения из select с multiple
  let selected = Array.from(select.options) // (1)
    .filter(option => option.selected) // (2)
    .map(option => option.value); // (3)

  alert(selected); // blues,rock
</script>
```

1.  Метод `#!js Array.from()` создаёт новый экземпляр `Array` из массивоподобного, 
    чтобы мы могли использовать методы такие как `filter`, `map` и т.д.
2.  Метод `filter()` возвращает новый массив со всеми элементами, прошедшими проверку, задаваемую в передаваемой функции(callback).
3.  `map()` вызывает функцию для каждого элемента массива и возвращает массив результатов выполнения этой функции.




