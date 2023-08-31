---
title: Prototype Pattern
sidebar_position: 6
---

Share properties among many objects of the same type

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/design-patterns/prototype-pattern#overview)

If we want to share properties among many objects of the same type, we can use the Prototype pattern.

![Four](https://javascriptpatterns.vercel.app/design-patterns/prototype-pattern/4.png)

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/design-patterns/prototype-pattern#implementation)

Say we wanted to create many dogs with a `createDog` factory function.

```js
const createDog = (name, age) => ({
  name,
  age,
  bark() {
    console.log(`${name} is barking!`);
  },
  wagTail() {
    console.log(`${name} is wagging their tail!`);
  },
});

const dog1 = createDog("Max", 4);
const dog2 = createDog("Sam", 2);
const dog3 = createDog("Joy", 6);
const dog4 = createDog("Spot", 8);
```

This way, we can easily create many dog objects with the same properties.

![Three](https://javascriptpatterns.vercel.app/design-patterns/prototype-pattern/3.png)

---

However, we're unnecessarily adding a new `bark` and `wagTail` methods to each dog object. Under the hood, we're creating two new functions for each dog object, which uses memory.

We can use the Prototype Pattern to share these methods among many dog objects.

```js
class Dog {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  bark() {
    console.log(`${this.name} is barking!`);
  }
  wagTail() {
    console.log(`${this.name} is wagging their tail!`);
  }
}

const dog1 = new Dog("Max", 4);
const dog2 = new Dog("Sam", 2);
const dog3 = new Dog("Joy", 6);
const dog4 = new Dog("Spot", 8);
```

![Four](https://javascriptpatterns.vercel.app/design-patterns/prototype-pattern/4.png)

ES6 classes allow us to easily share properties among many instances, `bark` and `wagTail` in this case.

## [](https://javascriptpatterns.vercel.app/patterns/design-patterns/prototype-pattern#)

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/design-patterns/prototype-pattern#tradeoffs)

**Memory efficient**: The prototype chain allows us to access properties that aren't directly defined on the object itself, we can avoid duplication of methods and properties, thus reducing the amount of memory used.

**Readaibility**: When a class has been extended many times, it can be difficult to know where certain properties come from.

For example, if we have a `BorderCollie` class that extends all the way to the `Animal` class, it can be difficult to trace back where certain properties came from.

![One](https://javascriptpatterns.vercel.app/design-patterns/prototype-pattern/2.png)