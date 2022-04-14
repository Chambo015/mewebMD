## Массив из всех подходящих элементов
#### `arr.filter(callback, thisArg)`
Вернётся новый массив с элементами, которые прошли проверку. Если ни один элемент не прошёл проверку, то будет возвращён пустой массив.
```JavaScript
function isBigEnough(value) {
  return value >= 10;
}

let filtered = [12, 5, 8, 130, 44].filter(isBigEnough); // [12, 130, 44]
```
## Первый найденный
### Элемент по условию 
#### `arr.find(callback, thisArg)`
*Возвращает значение первого найденного в массиве элемента*

Метод вызывает переданную функцию `callback` один раз для каждого элемента, присутствующего в массиве, до тех пор, пока она не вернёт `true`. Если такой элемент найден немедленно вернёт его. В противном случае, метод вернёт `undefined`.

`thisArg` - необязательный параметр. `this` при выполнении функции callback.
```js 
let users = [
    { id: 1, name: 'Santi'},
    { id: 2, name: 'Robin'},
    { id: 3, name: 'Aaron'},
];

let user = users.find(item => item.id === 2); // {id: 2, name: "Robin"}
```
### Индекс по условию
#### `arr.findIndex(callback, thisArg)`
Метод возвращает индекс в массиве, если элемент удовлетворяет условию проверяющей функции. В противном случае возвращается `-1`.
```js 
let arr = [0, 1, 5, 3];

let id = arr.findIndex(elem => elem > 4) // 2
let index = arr.findIndex(elem => elem > 10) // -1
```
#### `arr.indexOf(searchElem, fromIndex)`
Метод сравнивает искомый элемент `searchElem` с элементами в массиве, используя строгое сравнение `===`. `fromIndex` -  индекс, с которого начинать поиск.

`arr.lastIndexOf() ` -  то же самое, но ищет справа налево.
```js 
let arr = [1, 0, false];

arr.indexOf(0)     // 1
arr.indexOf(false) // 2
arr.indexOf(null)  // -1

arr.lastIndexOf(0) // 1
arr.lastIndexOf(false) // 2
arr.lastIndexOf(1) // 0
```
## Есть или нету
#### `arr.some(callback, thisArg)`
Метод проверяет, удовлетворяет ли какой-либо элемент массива условию. Если такой элемент найден, метод немедленно вернёт `true`. В противном случае `false`
```JavaScript
function isBiggerThan10(element, index, array) {
  return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```
#### `arr.includes(item, from)`
Ищет `item`, начиная с индекса `from`, и возвращает `true`, если поиск успешен.
```js 
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```
### Все подходят под условия
#### `arr.every(callback, thisArg)`
Метод проверяет, удовлетворяют ли все элементы массива условию, заданному в передаваемой функции. Если хоть один элемент не удовлетворяет условиям немедленно вернёт `false`
```js 
function isBigEnough(element, index, array) {
  return element >= 10;
}
[12, 5, 8, 130, 44].every(isBigEnough);   // false
[12, 54, 18, 130, 44].every(isBigEnough); // true
```
> Метод `every()` ищет `false`, как и `&&`  
> Метод `some()` ищет `true`, как и `||`