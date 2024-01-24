# homeWork_02
## 1) Создание объектов
```
let counter = { count: 0 };
```

```
let secondCounter = new Object({ count: 0 });
```

```
let thridCounter = Object.create(
  {},
  {
    count: {
      value: 0,
      writable: true,
      enumerable: true,
      configurable: true,
    },
  }
);
```

```
let fourthCounter = Object.assign({}, { count: 0 });
```
## 2) Копирование объектов
```
let objectCopy = { ...counter };
```

```
let secondObjectCopy = JSON.parse(JSON.stringify(counter));
```
```
let thridObjectCopy = Object.assign({}, counter);
```

```
const _ = require("lodash");
const fourthObjectCopy = _.cloneDeep(counter);
```

```
let fifthObjectClone = structuredClone(counter);
```

```
function copyObject(obj) {
  if (obj === null || typeof obj !== "object") {
    return obj;
  }

  const newObject = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      newObject[key] = copyObject(obj[key]);
    }
  }

  return newObject;
}
let fourthObjectCopy = copyObject(counter);
```
## 3) Создать функцию makeCounter
```
let makeCounter = () => {
  return { count: 0 };
};
```

```
function secondMakeCounter() {
  this.count = 0;
}
let objCounter = new secondMakeCounter();
```
## 4)Написать функцию глубокого сравнения двух объектов
```
const deepEqual = (obj1, obj2) => {
  if (obj1 === obj2) {
    return true;
  }

  if (
    typeof obj1 !== "object" ||
    typeof obj2 !== "object" ||
    obj1 === null ||
    obj2 === null
  ) {
    return false;
  }

  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);

  if (keys1.length !== keys2.length) {
    return false;
  }

  for (let key of keys1) {
    if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
      return false;
    }
  }

  return true;
};

const obj1 = { here: { is: "on", other: "3" }, object: "Y" };
const obj2 = { here: { is: "on", other: "2" }, object: "Y" };
console.log(deepEqual(obj1, obj2)); // Выведет false, так как значения свойства other различаются
```
## 5) Развернуть строку в обратном направлении при помощи методов массивов
```
function reverseStr(str) {
  return str.split("").toReversed().join("");
}
console.log(reverseStr("hello")); // выведет "olleh"
```
