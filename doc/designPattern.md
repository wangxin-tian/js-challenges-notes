# 设计模式

## 工厂模式

```js
class Animal {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

class Dog extends Animal {
  constructor(name, age, breed) {
    super(name, age);
    this.breed = breed;
  }
}

class Cat extends Animal {
  constructor(name, age, color) {
    super(name, age);
    this.color = color;
  }
}

class AnimalFactory {
  createAnimal(name, age, type, breedOrColor) {
    switch (type) {
      case 'dog':
        return new Dog(name, age, breedOrColor);
      case 'cat':
        return new Cat(name, age, breedOrColor);
      default:
        throw new Error('Invalid animal type.');
    }
  }
}

const animalFactory = new AnimalFactory();

const myDog = animalFactory.createAnimal('Buddy', 5, 'dog', 'Golden Retriever');
const myCat = animalFactory.createAnimal('Whiskers', 3, 'cat', 'orange');

console.log(myDog);
console.log(myCat);

```

## 单例模式

```js
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }

    return Singleton.instance;
  }

  sayHello() {
    console.log('Hello from Singleton instance!');
  }
}

const instance1 = new Singleton();
const instance2 = new Singleton();

console.log(instance1 === instance2); // true

instance1.sayHello();
instance2.sayHello();
```

## 观察者模式

```js
class Subject {
  constructor() {
    this.observers = [];
  }

  addObserver(observer) {
    this.observers.push(observer);
  }

  removeObserver(observer) {
    this.observers = this.observers.filter((o) => o !== observer);
  }

  notifyAll() {
    this.observers.forEach((observer) => observer.notify());
  }
}

class Observer {
  constructor() {}

  notify() {
    console.log('Subject has been updated!');
  }
}

const subject = new Subject();
const observer1 = new Observer();
const observer2 = new Observer();

subject.addObserver(observer1);
subject.addObserver(observer2);

subject.notifyAll();

subject.removeObserver(observer1);

subject.notifyAll();
```

## 装饰器模式

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHello() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}

function addHobby(hobby) {
  return function(person) {
    person.hobby = hobby;
    person.sayHelloWithHobby = function() {
      console.log(`Hello, my name is ${this.name}, I'm ${this.age} years old and I love ${this.hobby}.`);
    };
  };
}

const person = new Person('John', 25);

addHobby('reading')(person);

person.sayHelloWithHobby();

```

## 代理模式

```js
class Network {
  getData() {
    console.log('Fetching data from network...');
    return 'Data from network';
  }
}

class NetworkProxy {
  constructor() {
    this.network = new Network();
    this.cache = null;
  }

  getData() {
    if (!this.cache) {
      this.cache = this.network.getData();
    }

    console.log('Fetching data from cache...');

    return this.cache;
  }
}

const network = new NetworkProxy();

console.log(network.getData());
console.log(network.getData());
```
