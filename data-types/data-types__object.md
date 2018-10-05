# Объект

Коллекция данных (по принципу «ключ: значение»), объединяющая множество значений в единый модуль.

Пример: данные о пользователях. Для каждого пользователя нужно хранить уникальный идентификатор, имя, фамилию, возраст, электропочту, массив с уникальными идентификаторами друзей.

- У объекта могут быть свойства — любые данные, кроме функций.
- У объекта могут быть методы — функции, записанные как элементы объекта.


```js
// Создание объекта
var user = {
  name: 'Виссарион',
  age: 67,
};
console.log( typeof user ); // object

// Добавление свойств
user.role = 'Семейный диктатор';
user['Семейный статус'] = 'Женат и есть подруга';

// Доступ к свойству через точку
console.log( user.role ); // Семейный диктатор

// Доступ к свойству через квадратные скобки (имя свойства может быть любой строкой: с пробелами, минусами и т.п.)
console.log( user['Семейный статус'] ); // Женат и есть подруга

// Доступ к НЕСУЩЕСТВУЮЩЕМУ свойству
console.log( user.dance ); // undefined

// Проверка существования свойства
if ( 'dance' in user ) { // ВНИМАНИЕ: ключ передаётся в виде строки
  console.log( 'Свойство есть' );
}

// Удаление свойства
delete user.age;
console.log( user.age ); // undefined

// Ключом должна быть строка, значением может быть любой тип
var newUser = {
  name: 'Виссарион',
  age: 67,
  size:  {
    weight: 120,
    height: 168,
  },
  bald: true,
  '9': 'test',
  '1': 'test',
};
console.log( newUser.size.height );

// Перебор
for (key in newUser) {
  // Внимание! Если ключ — числовая строка, такие ключи выводятся в начале перебора и сортируются
  console.log( "Ключ: " + key + ", значение: " + newUser[key] );
}

// Свойства и методы
// name и age — свойства
// askFood    — метод
var cat = {
  name: 'Василиск',
  age: 3,
  askFood: function () {
    console.log('Жрать давай! МЯУ! Я ' + this.name + ', мотхерфуцкер!');
  },
  rename: function (newName) {
    this.name = newName;
  },
}
console.log( cat.age );    // получение свойства
cat.askFood();             // вызов метода
cat.rename('Попрошайник'); // вызов метода
```



## В переменной с объектом нет объекта

В переменной, которой присвоен объект, хранится только ссылка на объект, а не сам объект.

```js
// Создание переменной user
var user = {
  name: 'Виссарион',
  age: 67,
};

// Создание переменной newUser, идентичной переменной user.
// Объект останется один, но теперь на него указывают 2 ссылки.
var newUser = user;

console.log( 'В переменной user ключ name = ' + user.name );
console.log( 'В переменной newUser ключ name = ' + newUser.name );

// Изменим значение ключа name ТОЛЬКО в переменной user.
user.name = 'Аброр';

// Значение ключа name изменилась в обеих переменных:
console.log( 'В переменной user ключ name = ' + user.name );
console.log( 'В переменной newUser ключ name = ' + newUser.name );
```