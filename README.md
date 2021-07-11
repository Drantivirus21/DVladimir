# uplab


## __Димитриев Владимир__

### __a89279946399@gmail.com__

***
# Задача 1 - Выведите чётные числа
При помощи цикла for выведите чётные числа от 2 до 10.
## Выполнение:
```js
for (let i = 2; i <= 10; i++) {
  if (i % 2 == 0) {
    alert( i );
  }
}
```
***
# Задача 2 - Создайте калькулятор
Создайте объект calculator (калькулятор) с тремя методами:
                 
      *  read() (читать) запрашивает два значения и сохраняет их как свойства объекта.
      *  sum() (суммировать) возвращает сумму сохранённых значений.
      *  mul() (умножить) перемножает сохранённые значения и возвращает результат.
``` js
let calculator = {
  // ... ваш код ...
};
calculator.read();
alert( calculator.sum() );
alert( calculator.mul() );
```
## Выполнение:
```js
let calculator = {
  sum() {
    return this.a + this.b;
  },
  mul() {
    return this.a * this.b;
  },
  read() {
    this.a = +prompt('a?', 0);
    this.b = +prompt('b?', 0);
  }
};
calculator.read();
alert( calculator.sum() );
alert( calculator.mul() );
```
***
# Задача 3 - Покажите день недели
Напишите функцию getWeekDay(date), показывающую день недели в коротком формате: «ПН», «ВТ», «СР», «ЧТ», «ПТ», «СБ», «ВС».
## Выполнение:
```js
function getWeekDay(date) {
  let days = ['ПН', 'ВТ', 'СР', 'ЧТ', 'ПТ', 'СБ', 'ВС'];
  return days[date.getDay()];
}
let date = new Date(2021, 6, 11); // 11 июля 2021 год
alert( getWeekDay(date) ); // ВС
```
***
# Задача 4 - Декоратор-шпион
Создайте декоратор spy(func), который должен возвращать обёртку, которая сохраняет все вызовы функции в своём свойстве calls.
Каждый вызов должен сохраняться как массив аргументов.
## Выполнение:
```js
function spy(func) {
  function wrapper(...args) {
    wrapper.calls.push(args);
    return func.apply(this, arguments);
  }
  wrapper.calls = [];
  return wrapper;
}
```
***
# Задача 5 - Алгоритм поиска
У нас есть объекты:
```js
let head = {
  glasses: 1
};
let table = {
  pen: 3
};
let bed = {
  sheet: 1,
  pillow: 2
};
let pockets = {
  money: 2000
};
```
С помощью свойства __proto__ задайте прототипы так, чтобы поиск любого свойства выполнялся по следующему пути: pockets → bed → table → head. Например, pockets.pen должно возвращать значение 3 (найденное в table), а bed.glasses – значение 1 (найденное в head).
## Выполнение:
```js
let head = {
  glasses: 1
};
let table = {
  pen: 3,
  __proto__: head
};
let bed = {
  sheet: 1,
  pillow: 2,
  __proto__: table
};
let pockets = {
  money: 2000,
  __proto__: bed
};
alert( pockets.pen );
alert( bed.glasses ); 
alert( table.money );
```
# Задача 6 - Улучшенные часы
У нас есть класс Clock. Сейчас он выводит время каждую секунду:
```js
class Clock {
  constructor({ template }) {
    this.template = template;
  }

  render() {
    let date = new Date();

    let hours = date.getHours();
    if (hours < 10) hours = '0' + hours;

    let mins = date.getMinutes();
    if (mins < 10) mins = '0' + mins;

    let secs = date.getSeconds();
    if (secs < 10) secs = '0' + secs;

    let output = this.template
      .replace('h', hours)
      .replace('m', mins)
      .replace('s', secs);

    console.log(output);
  }

  stop() {
    clearInterval(this.timer);
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), 1000);
  }
}
```
Создайте новый класс ExtendedClock, который будет наследоваться от Clock и добавьте параметр precision – количество миллисекунд между «тиками». Установите значение в 1000 (1 секунда) по умолчанию.
## Выполнение: 
```js
class ExtendedClock extends Clock {
  constructor(options) {
    super(options);
    let { precision=1000 } = options;
    this.precision = precision;
  }
  start() {
    this.render();
    this.timer = setInterval(() => this.render(), this.precision);
  }
};
```
***
# Задача 7 - Наследование от SyntaxError
Создайте класс FormatError, который наследует от встроенного класса SyntaxError.
Класс должен поддерживать свойства message, name и stack.
## Выполнение:
```js
let err = new FormatError("ошибка форматирования");
alert( err.message ); // ошибка форматирования
alert( err.name ); // FormatError
alert( err.stack ); // stack
alert( err instanceof FormatError ); // true
alert( err instanceof SyntaxError ); // true 
```
***
# Задача 8 - Задержка на промисах
Встроенная функция setTimeout использует колбэк-функции. Создайте альтернативу, использующую промисы.

Функция delay(ms) должна возвращать промис, который перейдёт в состояние «выполнен» через ms миллисекунд, так чтобы мы могли добавить к нему .then:
```js
function delay(ms) {
  // ваш код
}

delay(3000).then(() => alert('выполнилось через 3 секунды'));
```
## Выполнение:
```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

delay(3000).then(() => alert('выполнилось через 3 секунды'));
```
***
# Задача 9 - Псевдослучайный генератор
Задачей является создать функцию-генератор pseudoRandom(seed), которая получает seed и создаёт генератор с указанной формулой.
```js
next = previous * 16807 % 2147483647
```
## Выполнение:
```js
function* pseudoRandom(seed) {
  let value = seed;
  while(true) {
    value = value * 16807 % 2147483647
    yield value;
  }
};
let generator = pseudoRandom(1);
alert(generator.next().value); // 16807
alert(generator.next().value); // 282475249
alert(generator.next().value); // 1622650073
```
# Задача 10 - Ошибка при чтении несуществующего свойства
Создайте прокси, который генерирует ошибку при попытке прочитать несуществующее свойство.
Напишите функцию wrap(target), которая берёт объект target и возвращает прокси, добавляющий в него этот аспект функциональности.
```js
let user = {
  name: "John"
};

function wrap(target) {
  return new Proxy(target, {
      /* ваш код */
  });
}

user = wrap(user);

alert(user.name); // John
alert(user.age); // Ошибка: такого свойства не существует
```
## Выполнение:
```js
let user = {
  name: "John"
};

function wrap(target) {
  return new Proxy(target, {
    get(target, prop, receiver) {
      if (prop in target) {
        return Reflect.get(target, prop, receiver);
      } else {
        throw new ReferenceError(`Свойство не существует: "${prop}"`)
      }
    }
  });
}

user = wrap(user);

alert(user.name); // John
alert(user.age); // Ошибка: Свойство не существует
```
