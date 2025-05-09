﻿В чём плюс использования стрелочных функций для методов в конструкторе?

Основным плюсом использования стрелочных функций для методов в конструкторе является то, что `this` будет установлено во время создания функции и `this` не будет изменяться. Cледовательно, когда конструктор используется для создания нового объекта, `this` всегда будет ссылаться на этот объект.

```js
const Person = function (firstName) {
  this.firstName = firstName

  this.sayName1 = function () {
    console.log(this.firstName)
  }

  this.sayName2 = () => {
    console.log(this.firstName)
  }
}

const ivan = new Person('Иван')
const petr = new Person('Пётр')

ivan.sayName1.call(petr) // Пётр, т.к call позволяет нам указать, что this будет 'petr' и  this сейчас ссылается на объект petr.
ivan.sayName2.call(petr) // Иван, так как стрелочная функция не меняет контекст.
```
Любая функция выполняется и создаётся в рамках контекста выполнения. Внутри этого контекста может или не может быть привязки `this`.
Когда функция вызывается с указанием перед ней new, также известный как вызов конструктора, привязка `this` есть. Создаётся новый объект, объект связывается с [[Прототипом]], this внутри функции связывается с `this` из текущего (лексического) контекста выполнения.
Мы можем воспользоваться явной привязкой посредством  вызова `call(..)`, который позволяет нам указать `this`.
Стрелочные функций заимствуют привязку this из окружающей (функции или глобальной) области видимости и  лексическая привязка не может быть изменена.
В стрелочной функции, созданной в `Person`, привязка не динамическая, а лексическая, поэтому контекст изменить нельзя и `this` всегда будет ссылаться на этот объект.
