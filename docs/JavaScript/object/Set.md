Новый тип из ES6 `Set` - коллекция уникальных значений

## Базовый API 
Создание экземпляра типа `Set`
```JavaScript
const set = new Set()

// Конструктор может принять любой итерируемый объект
let set = new Set(['era', 'meweb']) // {'era', 'meweb'} 
let set = new Set('meweb') // {'m', 'e', 'w', 'b'}
```
![](https://sun9-55.userapi.com/impf/wAFIAbLtTBQSeg5MuFNFBejDEPc447kP0u4jAw/mUlMmE_p6_E.jpg?size=322x127&quality=96&sign=d83fceedfce3e4dbf89a789ad7bd3959&type=album)

* `new Set(iterable)` – создаёт Set, и если в качестве аргумента был предоставлен итерируемый объект (обычно это массив), то копирует его значения в новый Set.
* `set.add(value)` – добавляет значение (если оно уже есть, то ничего не делает), возвращает тот же объект `set`.
* `set.delete(value)` – удаляет значение, возвращает `true`, если value было в множестве на момент вызова, иначе `false`.
* `set.has(value)` – возвращает `true`, если значение присутствует в множестве, иначе `false`.
* `set.clear()` – удаляет все имеющиеся значения.
* `set.size`– возвращает количество элементов в множестве.

### Перебор Set
Для перебора коллекции Set есть 4 метода:

* `map.values()` – возвращает перебираемый объект `SetIterator` для значений. Этот вариант используется по умолчанию `Symbol(Symbol.iterator): ƒ values()`
    ```JavaScript
    for (let value of set) { // то же самое, что и set.values()
        console.log(value); // 'era'
         // 'meweb'
    }
    ```
* `set.keys()` – то же самое, что и `set.values()`, присутствует для обратной совместимости с `Map`
* `set.entries()` – возвращает перебираемый объект для пар вида `[значение, значение]`, присутствует для обратной совместимости с `Map`.
* `set.forEach()` – в котором колбэк имеет 3 аргумента `(value, valueAgain, set)`. Выглядит немного странно, но в некоторых случаях может помочь легко заменить Map на Set и наоборот.
   
## Преобразования Set в массив
```JavaScript
const arr = [...set] // ['era', 'meweb']
const arr2 = Array.from(set) // ['era', 'meweb']
```
