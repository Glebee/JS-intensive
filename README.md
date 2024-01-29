## 1) Написать ответ - почему массивы в JS являются "неправильными" и совмещают в себе несколько структур данных? Какие?
Массивы в JavaScript считаются "неправильными" по нескольким причинам:
- Меняют размер динамически: В отличие от других языков, где массивы статичны, в JavaScript их размер можно менять на лету, добавлять или удалять элементы;
- В них можно класть разные штуки: Массивы в JavaScript могут содержать в себе разные типы данных — числа, строки, объекты, функции, что угодно;
- Схожи с объектами: Все массивы в JavaScript являются объектами, поэтому у них есть свои свойства и методы, как, например, length или toString();
- Могут эмулировать стеки и очереди: Хотя нет специальных методов для стеков и очередей, с помощью push(), pop(), shift() и unshift() можно эмулировать эти структуры.

## 2) Привязать контекст объекта к функции logger, чтобы при вызове this.item выводило - some value (Привязать через bind, call, apply)
```
function logger() {
    console.log(`I output only external context: ${this.item}`);
}

const obj = { item: "some value" };

// С использованием `bind`
const bindedLogger = logger.bind(obj);
bindedLogger();

// С использованием `call`
logger.call(obj);

//С использованием `apply`
logger.apply(obj);
```
Во всех трех случаях контекст this в функции logger будет привязан к объекту obj, и при вызове this.item будет выводить "some value"

## Реализовать полифил(собственную функцию реализующую встроенную в js) метода bind()
```
if (!Function.prototype.customBind) {
  Function.prototype.customBind = function (context, ...args) {
    const originalFunction = this;

    return function (...newArgs) {
      // Используем apply для передачи контекста и аргументов
      return originalFunction.apply(context, args.concat(newArgs));
    };
  };
}

// Пример использования
function logger() {
  console.log(`I output only external context: ${this.item}`);
}

const obj = { item: "some value" };

const customBindedLogger = logger.customBind(obj);
customBindedLogger(); // Выведет: I output only external context: some value
```
