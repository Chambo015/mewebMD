# Object
## Методы для работы со свойствами
Общий объект для примера:
```js 
let user = {
    name: "John",
    age: 30,
    language: [
        'english',
        'russian'
    ],
    family: {
        father: "Leo",
        mather:  "Mia"
    }
};
```
### `Object.keys/values/entries`
Данные статические методы предлагают итерируемый формат для свойств объекта. Методы поддерживаются для структур: `Map` `Set` `Array`

!!! info "Важно знать"

    `Object.values, entries` добавлены в ECMAScript 2017.  
    `Object.values, entries` выполняют поверхностное копирование объекта.  
    `Object.keys/values/entries` игнорируют символьные свойства, но если требуется учитывать и символьные ключи, метод `Object.getOwnPropertySymbols`, возвращающий массив только символьных ключей.

#### `Object.keys(obj)`
Возвращает массив из собственных перечисляемых свойств переданного объекта.  
Есть аналог `Object.getOwnPropertyNames()` отличие ➔ возвращает и не перечисляемые свойства.
```JavaScript
Object.keys(user) // ['name', 'age', 'language', 'family']
```

#### `Object.values(obj) `
Возвращает массив значений перечисляемых свойств объекта.
```js 
Object.values(user) // ['John', 30, ['english', 'russian'], {father: 'Leo', mather: 'Mia'}]
```

#### `Object.entries(obj) `
Возвращает массив собственных перечисляемых свойств указанного объекта в формате `[key, value]`
```js 
Object.entries(user)
// [['name', 'John'], 
//  ['age', 30], 
//  ['language', ['english', 'russian']], 
//  ['family', {father: 'Leo', mather: 'Mia'}]]
```

#### `Object.fromEntries(iterable)`
Выполняет процедуру, обратную `Object.entries()`. `iterable` список пар ключ-значение такой как `Array` или `Map`.

Например мы хотим воспользоваться услугой метода массивов `arr.map()` для объекта:
```js 
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
    Object.entries(prices)
        .map(([key, value]) => [key, value * 2])
);

doublePrices // { banana: 2, orange: 4, meat: 8 }
```