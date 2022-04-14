Добавленный в *ES6* `Map` - новый тип коллекции ключ/значение, как и `Object`. 
Но основное отличие в том, что Map позволяет использовать ключи любого типа.

## Базовый API 
Создание экземпляра типа `Map`
```JavaScript
const map = new Map()

// Заполнение при инициализации 
let user = {
    name: "John",
    age: 30,
}
let map = new Map(Object.entries(user))
```

* `new Map()` – создаёт коллекцию.
* `map.set(key, value)` – записывает по ключу key значение value. Если такой ключ уже есть, то перезапишет.
    ```JavaScript
    map.set(undefined, 'ничего')
      .set(5, 'пять')
      .set(NaN, 'Не число');
    // ключём может быть все что угодно, даже ссылки на объект
    ```
* `map.get(key)` – возвращает значение по ключу или undefined, если ключ key отсутствует.
    ```JavaScript
    map.get(undefined) // 'ничего'
    map.get(5)         // 'пять'
    map.get(NaN)       // 'Не число'
    ```
* `map.has(key)` – возвращает true, если ключ key присутствует в коллекции, иначе false.
* `map.delete(key)` – удаляет элемент по ключу key.
    ```JavaScript
    map.delete(NaN) // true
    // true если элемент в Map объекте существовал и был удален, или false если элемент не существует.
    ```
* `map.clear()` – очищает коллекцию от всех элементов.
* `map.size` – возвращает текущее количество элементов.

### Перебор Map
Для перебора коллекции Map есть 4 метода:

* `map.keys()` – возвращает итерируемый объект `MapIterator` по ключам
    ```JavaScript
    for (let key of map.keys()) {
        console.log(key);
        // "name"
        // "age"
        // undefined
        // 5
        // NaN
    }
    ```
* `map.values()` – возвращает итерируемый объект `MapIterator` по значениям
    ```JavaScript
    for (let value of map.values()) {
        console.log(value);
        // "John"
        // 30
        // "ничего"
        // "пять"
        // "Не число"
    }
    ```
* `map.entries()` – возвращает итерируемый объект по парам вида [ключ, значение], этот вариант используется по умолчанию в `for..of`.
    ```JavaScript
    for (let [key, value] of map) { // то же самое, что и map.entries()
        console.log([key, value]);
        // ['name', 'John']
        // ['age', 30]
        // [undefined, 'ничего']
        // [5, 'пять']
        // [NaN, 'Не число']
    }
    ```
* `map.forEach()` – перебирает каждый ключ/значение, схожий со встроенным методом массивов Array
    ```JavaScript
    map.forEach((value, key, map) => {
        console.log(`${key} = ${value}`)
    }) // name = John
       // age = 30
    ```

## Преобразования Map в массив или объект
```JavaScript
// в массив
const arr = [...map]
const arr2 = Array.form(map)

// в объект
const obj = Object.fromEntries(map)
```

## Примеры
У нас есть объект с пользователями и мы хотим узнать их время посещения.
```JavaScript
const users = [
    {name: "Elena"},
    {name: "Sergey"},
    {name: "Alex"},
];

// Карта со временем последнего визита 
let visits = new Map();

visits.set(users[0], new Date())
    .set(users[1], new Date())
    .set(users[2], new Date())

// Функция получения даты последенего визита, определенного юзера
function getLastVisit(user) {
    return visits.get(user)
}

getLastVisit(users[0]) // Sun Apr 10 2022 21:45:40 GMT+0600 (Восточный Казахстан)
```