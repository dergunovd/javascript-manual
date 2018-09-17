## Методические рекомендации по теме «Основные конструкции и операторы в языке JavaScript»

JavaScript - язык с динамической типизацией. Т.е. тип переменной можно переобъявлять по ходу программы.
Синтаксис JavaScript похож на другие C-подобные языки.

## Основные элементы языка

### Объявление переменной
Переменная в JavaScript объявляется ключевым словом `var`
Пример:
```JavaScript
var a = 5;
var b = 'some strging';
```
В стандарте **ECMAScript6** также доступны два дополнительных ключевых слова для объявления переменных: `let`, и `const`.
Они отличаются от var областью видимости: var доступна в пределах текущей функции и может "всплывать", это означает, что следующие два фрагмента эквиваленты:
```JavaScript
console.log(a); // undefined
var a = 5;
```
```JavaScript
var a;
console.log(a); // undefined
a = 5;
```
переменные, объявленные с помощью `let` и `const` не всплывают и доступны в пределах фигурных скобок
```JavaScript
console.log(a); // reference error
{
const a = 5;
}
console.log(b); // error
let b = 10;
```
Различие в `let` и `const` заключается в том, что переменную `const` нельзя переопределять
```JavaScript
let a = 5;
a = 10; // a == 10
const b = 14;
b = 7; // error
```
### Типы данных
* **boolean** - логический тип принимает значения `true`, `false`

* **number** - числовой тип. Как для целочисленных значений, так и для чисел с плавающей точкой.
Примеры значений: `5`, `3.2`, `3e12`, `NaN`.
Значение NaN (Not a number) относится к числовому типу и обозначает "не число". Используется при переводе некорректной строки к числу `Number('helloworld'); // NaN` или при некорректных математических операциях `0 / 0; // NaN`

* **string** - строковый тип.
Примеры значений: `'Hello world'`, `''`, `'asd'`

* **object** - ссылочный тип. Объект представляет собой совокупность __пара - значение__. 
Примеры значений:
```JavaScript
{
	first: 1,
	second: 'asd'
	third: function(a) { return a*a } 
}
```
* **null** - особый тип данных. Указатель на пустой объект

* **undefined** - особый тип данных, обозначающий неинициализированную переменную

Все типы кроме объекта являются иммутабельными и называются примитивными.
При присвоении переменной примитивного типа создается его копия.
Пример:
```JavaScript
var a = 5;
b = a;
b + 5; // a == 5, b == 10
```
При присвоении переменной ссылочного типа, ссылочный тип передается по ссылке.
Пример:
```JavaScript
var a = {key: 'value'};
var b = a;
b.key2 = 123; // a == { key: 'value', key2: 123 }, b == { key: 'value', key2: 123 }
```

### Функции
Функция - объект особого типа, имеющий конструктор и возвращающий значение.
Пример: 
```JavaScript
function sum (a, b) {
	return a + b;
}
```
В новом стандарте **ECMAScript6** допускается использование стрелочных функций.
Пример:
```JavaScript
var sum = (a, b) => a + b;
```
Функция в JavaScript является объектом первого типа, т.е. функцию можно передавать как аргумент функции, возвращать из функции.

### Массивы
Массив - упорядоченный набор переменных. Переменные не обязательно должны быть одного типа.

Пример: 
```JavaScript
var array = [1, 2, 'asd', null, { a: 123 }]; // инициализированный массив
var arr = [5, 3, 1, 2, 4];
var anoutherArray = new Array(5); // пустой массив размером 5
```
#### Методы массива
Язык предоставляет некоторые методы и свойства для работы с массивом
* `arr.length; // 5` - длина массива
* `arr.sort(); // [1, 2, 3, 4, 5]` - сортировка массива. Принимает фукнцию-компаратор. Которая принимает два аргумента и возвращает отрицательное число, если первый аргумент должен находиться перед вторым, ноль, если порядок элементов не важен, положительное число, если первый элемент должен стоять после второго.
Пример:
```JavaScript
arr.sort((a, b) => b - a); // [5, 4, 3, 2, 1]
```
* `arr.map((item, index, array) => item * index); // [0, 3, 2, 6, 16]` - поэлементная обработка массива. Возвращает новый массив с применением переданной функции к каждому элементу, не изменяя текущий массив. Функция-аргумент принимает текущий элемент, индекс текущего элемента и указатель на массив.
* `arr.filter((item, index, array) => a % 2 == 0);` - фильтрация массива, возвращает новый массив. Принимает функцию, которая должна примениться к каждому элементу массива и вернуть `true`, если элемент должен включаться в выборку и `false` в противном случае. Функция-аргумент принимает текущий элемент, индекс текущего элемента и указатель на массив. 
* `arr.reduce((accum, value) => accum + value, 0); // 15` - метод возвращает одно значение, на основе обхода всего массива. Принимает два звачения: фукнцию, которая принимает аккумулирующее значени, текущий элемент массива и возвращает новое значение, и начальное значение.
* `arr.forEach((item, index, array) => { a += item } );` - подобно `.map()`, но не возвращает новый массив.

### Операторы равенства и эквивалентности.
В языке существуют два оператора для сравнения переменных на равенство: `==` и `===`
Различие заключается в том, что оператор `==` предварительно приводит переменные к одному типу, `===` же выполняет строгое сравнение, при котором переменные разного типа всегда являются не равных, даже если приводятся к одному и тому же значению.
Пример:
```JavaScript
2 == '2'; // true
2 === '2'; // false
```

При сравнении двух переменных разного типа с помощью оператора `==` выполняется приведение типов. Приведение происходит по следующим правилам:
* Если операнд - логическое значение, перед проверкой оно преобразуется в число (`true` в `1`, `false` в `0`)
* Если операнды - строка и число, перед сравнением предпринимается попытка преобразовать строку в число
* Если один из операндов объект - для него вызывается метод `.valueOf()`, чтобы получить примитивное значение, которое затем сравнивается по предыдущим правилам
* Значения `null` и undefined равны
* Значения `null` и undefined не преобразуются в другие типы
* Значение `NaN` не равно ни одному другому значению, в том числе `NaN`
* Если оба операнда объекты - они сравниваются по ссылке (`true` возвращается, если это один и тот же экземпляр)

### Унарные операторы
* `++` - инкремент. Допустимы как префиксная, так и постфиксная запись
```JavaScript
let a = 5;
a++; // a == 6;
++a; // a == 7;
```
* `--` - декремент. Допустимы как префиксная, так и постфиксная запись
```JavaScript
let a = 5;
a--; // a == 4;
--a; // a == 3;
```
* `+` - унарный плюс. Если применяется к числовому значению, то ничего с ним не делает. Если применяется к нечисловому значению - приводит его к числу подобно функции `Nubmer()`
```JavaScript

```
* `-` - унарный минус

### Поразрядные операторы
* &
* ^
* |

### Логические операторы
* &&
* ||
* !

### Мультипликативные операторы
### Операторы сложения и вычитания
* `+`
* `-`

### Операторы отношений
* `<`
* `>`
* `<=`
* `>=`
* `!=`
* `!==`

### Условный тернарный оператор
* `? :`

### Операторы присвоения
* `+=`
* `-=`
* `*=`
* `/=`
* `&=`
* `^=`
* `|=`
* `%=`

### Инструкция if
`if(<condition>) { <body> }`

### Инструкция do-while
`do {<body>} while(<condition>)`

### Инструкция while
`while(<condition>) {<body>}`

### Инструкция for
`for(<declarations>; <condition>; <loop>) {<body>}`

### Инструкция for-in
`for(<var> in <object>) {<body>}`

### Инструкция for-of
`for(<var> of <object>) {<body>}`

### Инструкции break и continue
`break;`, `continue;`

### Инструкция switch
```JavaScript
switch(/*var*/) {
case /*cond*/: /*body*/
...
case /*cond*/: /*body*/
default: /*body*/
}
```
# Примеры решения задач

# Задачи для самостоятельного решения

# Решения задач

# Тест

# Ответы

# Источники
* Zakas N.C. - Professional JavaScript for Web Developers 2011
