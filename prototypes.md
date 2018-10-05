# Прототипы

При обращении к свойствам и методам объекта, если они не найдены в самом объекте, интерпретатор пытается найти их в прототипе объекта.

- Объект `Object` — прототип любого объекта.
- Методы лучше помещать в прототипы, а не в конструкторы.

```js
// Создаём конструктор
function Rect(w, h) {
  this.width = w;
  this.height = h;
}

// Обращаемся к прототипу конструктора, добавляя прототипу функцию
Rect.prototype.getArea = function () {
  return this.width * this.height;
}

// Обращаемся к прототипу конструктора, добавляя прототипу свойство
Rect.prototype.name = 'Прямоугольник';
Rect.prototype.msg = 'Wow!';

// Создаём объект с помощью конструктора
var test = new Rect(20, 40);

// Вызываем функцию, которой нет в конструкторе, но которая есть в прототипе конструктора
test.getArea();

// Получаем свойство name, которого нет в объекте и конструкторе, но есть в прототипе
console.log(test.name); // Прямоугольник

// Определяем для объекта своё собственное свойство name
test.name = 'Я гордый недоквадрат!';
console.log(test.name); // Я гордый недоквадрат!

// Упоротый способ вызвать конструктор «такой же как у того парня»
var testConst = new test.constructor(10, 10);
testConst.getArea(); // 100

// Переопределение методов прототипа
console.log(test);           // Rect {width: 20, height: 40, name: "Я гордый недоквадрат!"}
console.log(test.valueOf()); // Rect {width: 20, height: 40, name: "Я гордый недоквадрат!"}
Rect.prototype.valueOf = function() {
  return this.getArea();
}
console.log(test.valueOf()); // 800, т.к. теперь valueOf() вызовет getArea()
console.log(test + 1);       // 801, т.к. теперь valueOf() вызовет getArea(), 800 + 1 = 801

// Выяснение: есть ли свойство у объекта, или это свойство прототипа
console.log(test.hasOwnProperty('width')); // true, ибо свойство width есть на самом объекте
console.log(test.hasOwnProperty('msg'));   // false, ибо свойство msg есть только на прототипе объекта, а не на нём самом
// Выяснение: есть ли свойство у объекта ИЛИ У прототипа
console.log('width' in test); // true, т.к. свойство было найдено у объекта или у одного из его прототипов
console.log('msg' in test);   // true, т.к. свойство было найдено у объекта или у одного из его прототипов
```