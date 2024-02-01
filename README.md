## 1) Какие бывают алгоритмы сортировок ?
Существует множество алгоритмов сортировки, каждый из которых имеет свои преимущества и недостатки в зависимости от конкретных условий использования. Вот несколько популярных алгоритмов:
1) Bubble Sort:
- Проходит по списку многократно, сравнивает пары соседних элементов и меняет их местами, если они находятся в неправильном порядке.
- O(n^2)
2) Сортировка выбором (Selection Sort):
- Ищет минимальный элемент в списке и обменивает его с первым элементом, затем ищет минимальный среди оставшихся и обменивает его со вторым элементом, и так далее.
- O(n^2)
3) Сортировка вставками (Insertion Sort):
- Строит отсортированную последовательность, вставляя элементы из неотсортированной части списка на их места в отсортированной части.
- O(n^2)
4) Сортировка слиянием (Merge Sort):
- Рекурсивно разделяет список на две половины, сортирует каждую половину, а затем объединяет их в отсортированный список.
- O(n log n)
5) Быстрая сортировка (Quick Sort):
- Выбирает опорный элемент, разделяет список на элементы, меньшие и большие опорного, затем рекурсивно сортирует каждую из подсписков.
- O(n^2) в худшем случае, но обычно O(n log n)
## 3) Создать объект Person несколькими способами, после создать объект Person2, чтобы в нём были доступны методы объекта Person. Добавить метод logInfo чтоб он был доступен всем объектам.
- Использование конструктора для создания объекта Person
```
function PersonConstructor(name, age) {
  this.name = name;
  this.age = age;
  this.sayHi = function() {
    console.log("Hi!");
  };
}

let person3 = new PersonConstructor("John", 30);
```
- Создание объекта Person с использованием Object.create
```
let Person = Object.create({}, {
  name: { value: "Gleb" },
  age: { value: 22 },
  sayHi: {value: () => {
    console.log("Hi!");
  }},
});
```

- Создание объекта Person с использованием литерала объекта
```
let Person = {
  name: "Gleb",
  age: 22,
  sayHi: () => {
    console.log("Hi!");
  },
};
```

```
let Person2 = Object.create(Person, {
  name: { value: "Aleksandra" },
  age: { value: 23 },
});

Object.prototype.logInfo = function () {
  console.log(`My name is ${this.name} and im ${this.age} years old`);
};
```

## 4) Создать класс PersonThree c get и set для поля name и конструктором, сделать класс наследник от класса Person.
```
class Person {
  constructor(options) {
    this.name = options.name;
  }

  get getName() {
    return this.name;
  }

  set setName(newName) {
    this.name = newName;
  }

  sayHi() {
    console.log(`Hi, its ${this.name}`);
  }
}

class PersonThree extends Person {
  constructor(options) {
    super(options);
    this.age = options.age;
  }

  get getAge() {
    return this.age;
  }

  set setAge(newAge) {
    this.age = newAge;
  }

  greetings() {
    console.log(`hello, my name is ${this.name} and Im ${this.age} years old`);
  }
}

let Gleb = new PersonThree({ name: "Gleb", age: 22 });
```
## БОНУС: 
## 1) Написать функцию, которая вернет массив с первой парой чисел, сумма которых равна total:
```
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
total = 13;
//result = [4, 9]

const firstSum = (arr, total) => {
  arr.sort((a, b) => a - b);

  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const currentSum = arr[left] + arr[right];

    if (currentSum === target) {
      return [arr[left], arr[right]];
    } else if (currentSum < target) {
      left++;
    } else {
      right--;
    }
  }

  return null;
}

firstSum(arr,total)
```
## 2) Какая сложность у вашего алгоритма ?
Алгоритм имеет временную сложность **O(n log n)**, т.к. сначала идет сортировка массива O(n log n) времени (в среднем случае), затем два указателя проходят по массиву в худшем случае за O(n) времени. 
