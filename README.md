#### 10 правил написания кода на JavaScript
---
#### 1. Используйте понятные имена переменных и функций.
Код гораздо легче читать, когда при его написании используют понятные, описательные имена функций и переменных.

// плохо
 js
function avg (a) {
  let s = a.reduce((x, y) => x + y);
  return s / a.lenght;
}


Его читабельность значительно улучшится, если использовать в нём понятные имена переменных и функций, отражающие их смысл.

// хорошо
 js
function averageArray (array) {
  let sum = array.reduce((number, currentSum) => number + currentSum);
  return sum, array.length;
}



Не стремитесь к минимализму при написании текстов программ. Используйте полные имена переменных, которые тот, кто будет работать с вашим кодом в будущем, легко сможет понять.

---
#### 2. Используйте идеи инкапсуляции и модульности
Группируйте связанные переменные и функции для того, чтобы сделать ваш код понятнее и улучшить его с точки зрения его повторного использования.

// плохо
 js
let name = 'Ali';
let age = 24;
let job = 'Software Engineer';
let getBio = (name, age, job) => `${name} is a ${age} year-old ${job}`;

Если в подобной программе нужно обрабатывать данные многих людей, тогда в ней лучше будет использовать нечто вроде следующей конструкции.

// хорошо
 js
class Person {
    constructor(name, age, job) {
        this.name = name;
        this.age = age;
        this.job = job;
    }
    getBio () {
        return `${this.name} is a ${this.age} year-old ${this.job}`;
    }
}

А если в программе надо работать лишь с данными об одном человеке, то их можно оформить так, как показано ниже.

// хорошо
 js
const ali = {
    name = 'Ali',
    age = 24,
    job = 'Software Engineer',
    getBio: function () {
        return `${this.name} is a ${this.age} year-old ${this.job}`;
    }
}

Похожим образом следует подходить к разбиению длинных программ на модули, на отдельные файлы. Это облегчит использование кода, выделенного в отдельные файлы, в разных проектах. В больших файлах с программным кодом часто тяжело ориентироваться, а небольшие понятные модули легко использовать и в том проекте, для которого они созданы, и, при необходимости, в других проектах. Поэтому стремитесь к написанию понятного модульного кода, объединяя логически связанные элементы.

---
#### 3.Переменные

+ Называйте переменные так, чтобы их имена раскрывали бы их сущность, их роль в программе. При таком подходе их удобно будет искать в коде, а тот, кто увидит этот код, легче сможет понять смысл выполняемых им действий.

:wink: Хороший пример:
 ```
 const MaxAge = 16;
let daysSinceLastVisit = 10;
let currentYear = new Date().getFullYear();
...
const isUserOlderThanAllowed = user.age > MaxAge;
 ```
 😠 Плохой пример:
 ```
let daysSLV = 10;
let y = new Date().getFullYear();
let ok;
if (user.age > 30) {
  ok = true;
}
 ```
 + Всегда используйте let или const для объявления каждой переменной.

 :wink: Хороший пример :
 ```
 let user = "Kseniya";
 const count = 2;
 ```
 😠 Плохой пример:
 ```
var message = "Arror"; //устаревшее объявление переменной, может встречаться в коде до ES-2015, стоит избегать.
count = 2; //объявление переменной нет, ошибка.
 ```

#### 4.Имя переменной
+ Имя переменной должно содержать только буквы, цифры или символы `$` и `_`.
+ Первый символ не должен быть цифрой.
+ Если имя содержит несколько слов,то каждое следующее слово начинается с заглавной буквы:
+ Избегайте использования аббревиатур или коротких имён, таких как a, b, c, за исключением тех случаев, когда вы точно знаете, что так нужно.

:wink: Хороший пример:

```
let userName;
let test123;
```
😠 Плохой пример:
```
let 1b // не может начинаться с цифры
let i-23; // не может включать дефис
```
#### 5.Фигурные скобки

+  Фигурные скобки пишутся  на той же строке, что и соответствующее ключевое слово.Перед открывающей скобкой должен быть пробел.

:wink:  Хороший пример:

```
if (n < 0) {
  alert(`Good!`);
}
```
😠 Плохой пример:

```
if (n < 0){alert(`Bad!`);}
```
#### 6. Размещение функций
Если вы пишете несколько вспомогательных функций, а затем используемый ими код, то существует три способа организации функций.
1)Объявить функции перед кодом, который их вызовет:
// объявление функций
function createElement() {
  ...
}
function setHandler(elem) {
  ...
}
function walkAround() {
  ...
}
// код, который использует их
let elem = createElement();
setHandler(elem);
walkAround();
2)Сначала код, затем функции
// код, использующий функции
let elem = createElement();
setHandler(elem);
walkAround();
// --- вспомогательные функции ---
function createElement() {
  ...
}
function setHandler(elem) {
  ...
}
function walkAround() {
  ...
}
3)Смешанный стиль: функция объявляется там, где она используется впервые.
В большинстве случаев второй вариант является предпочтительным.
Это потому, что при чтении кода мы сначала хотим знать, что он делает. 
Если сначала идёт код, то это тут же становится понятно. 
И тогда, может быть, нам вообще не нужно будет читать функции, особенно если их имена хорошо подобраны.

#### 7. Уровни вложенности
ровней вложенности должно быть немного.
Например, в цикле бывает полезно использовать директиву continue, чтобы избежать лишней вложенности.
Например, вместо добавления вложенного условия if, как здесь:
for (let i = 0; i < 10; i++) {
  if (cond) {
    ... // <- ещё один уровень вложенности
  }
}
Мы можем написать:
for (let i = 0; i < 10; i++) {
  if (!cond) continue;
  ...  // <- нет лишнего уровня вложенности
}

#### 8. Инструкции
Инструкции – это синтаксические конструкции и команды, которые выполняют действия.
Мы уже видели инструкцию alert('Привет, мир!'), которая отображает сообщение «Привет, мир!».
В нашем коде может быть столько инструкций, сколько мы захотим. Инструкции могут отделяться точкой с запятой.
Например, здесь мы разделили сообщение «Привет Мир» на два вызова alert:
alert('Привет'); alert('Мир');
Обычно каждую инструкцию пишут на новой строке, чтобы код было легче читать:
alert('Привет');
alert('Мир');

#### 9. Используйте понятные имена переменных и функций
Код гораздо легче читать, когда при его написании используют понятные, описательные имена функций и переменных. 
Вот не очень понятный код:
function avg (a) {
let s = a.reduce((x,y) => x + y)
return s / a.length
}
Его читабельность значительно улучшится, если использовать в нём 
понятные имена переменных и функций, отражающие их смысл.
function averageArray (array) {
let sum = array.reduce((number, currentSum) => number + currentSum)
return sum / array.length
}
#### 10. Пишите короткие функции, решающие одну задачу
Функции легче поддерживать, они становятся гораздо более понятными, читабельными, если они направлены на решение лишь какой-то одной задачи. 
Если мы сталкиваемся с ошибкой, то, при использовании маленьких функций, найти источник этой ошибки становится гораздо легче. 
Кроме того, улучшаются возможности по повторному использованию кода.
function averageArray (array) {
let sum = array.reduce((number, currentSum) => number + currentSum)
return sum / array.length
}
Её можно разбить на две функции, тогда роль каждого фрагмента кода станет более понятной. 
Кроме того, если мы создаём большую программу, наличие функции sumArray может оказаться очень кстати.
function sumArray(array) {
return array.reduce((number, currentSum) => number + currentSum)
}
function averageArray (array) {
return sumArray)array) / array.length
}