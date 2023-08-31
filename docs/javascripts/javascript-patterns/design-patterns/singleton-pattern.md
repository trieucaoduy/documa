---
title: Singleton Pattern
sidebar_position: 2
---


Share a single global instance throughout our application

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/design-patterns/singleton-pattern#overview)

With the Singleton Pattern, we restrict the instantiation of certain classes to one single instance. This single instance is unmodifiable, and can be accessed globally throughout the application.

For example, we can have a `Counter` singleton, which contains a `getCount`, `increment`, and `decrement` method.

![Singleton](https://javascriptpatterns.vercel.app/design-patterns/singleton-pattern/1.png)

This singleton can be shared globally across multiple files within the application. The imports of this Singleton all reference the same instance.

The `increment` method increments the value of `counter` by 1. Any time the `increment` method has been invoked anywhere in the application, thus changing the value of `counter`, the change is reflected throughout the entire application.


<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1652717288/FM%20Workshop/Screen_Recording_2022-05-16_at_11.05.50_AM_xzeo41.mov" type="video/mp4" />
</video>

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/design-patterns/singleton-pattern#implementation)

In ES6, there are several ways to create Singletons.

#### [Classes](https://javascriptpatterns.vercel.app/patterns/design-patterns/singleton-pattern#classes)

Creating a singleton with an ES2015 `class` can be done by:

```js
let instance;

// 1. Creating the `Counter` class, which contains a `constructor`, `getInstance`, `getCount`, `increment` and `decrement` method.
// Within the constructor, we check to make sure the class hasn't already been instantiated.
class Counter {
  constructor() {
    if (instance) {
      throw new Error("You can only create one instance!");
    }
    this.counter = counter;
    instance = this;
  }

  getCount() {
    return this.counter;
  }

  increment() {
    return ++this.counter;
  }

  decrement() {
    return --this.counter;
  }
}

// 2. Setting a variable equal to the the frozen newly instantiated object, by using the built-in `Object.freeze` method.
// This ensures that the newly created instance is not modifiable.
const singletonCounter = Object.freeze(new Counter());

// 3. Exporting the variable as the `default` value within the file to make it globally accessible.
export default singletonCounter;
```

---

#### [Objects](https://javascriptpatterns.vercel.app/patterns/design-patterns/singleton-pattern#objects)

We can also directly create objects without having to use a `class`, which can lead to much simpler and cleaner code.

To create a singleton using a regular object, we have to:

```js
let counter = 0;

// 1. Create an object containing the `getCount`, `increment`, and `decrement` method.
const counterObject = {
  getCount: () => counter,
  increment: () => ++counter,
  decrement: () => --counter,
};

// 2. Freeze the object using the `Object.freeze` method, to ensure the object is not modifiable.
const singletonCounter = Object.freeze(counterObject);

// 3. Export the object as the `default` value to make it globally accessible.
export default singletonCounter;
```

We could even export the frozen object directly, without having to declare multiple variables.

```js
let counter = 0;

export default Object.freeze({
  getCount: () => counter,
  increment: () => ++counter,
  decrement: () => --counter,
});
```

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/design-patterns/singleton-pattern#tradeoffs)

**Memory**: Restricting the instantiation to just one instance could potentially save a lot of memory space. Instead of having to set up memory for a new instance each time, we only have to set up memory for that one instance, which is referenced throughout the application.

**Unnecessary**: ES2015 Modules are singletons by default. We no longer need to explicitly create singletons to achieve this global, non-modifiable behavior.

**Depedency Hiding**: When importing another module, it may not always be obvious that that module is importing a Singleton. This could lead to unexpected value modification within the Singleton, which would be reflected throughout the application.

**Global Scope Pollution**: The global behavior of Singletons is essentially the same as a global variable. Global Scope Pollution can end up in accidentally overwriting the value of a global variable, which can lead to a lot of unexpected behavior. Usually, certain parts of the codebase modify the values within global state, whereas others consume that data. The order of execution here is important, understanding the data flow when using a global state can get very tricky as your application grows, and dozens of components rely on each other.

**Testing**: Since we can't create new instances each time, all tests rely on the modification to the global instance of the previous test. The order of the tests matter in this case, and one small modification can lead to an entire test suite failing. After testing, we need to reset the entire instance in order to reset the modifications made by the tests.