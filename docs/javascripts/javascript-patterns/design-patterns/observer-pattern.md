---
title: Observer Pattern
sidebar_position: 4
---

Use observables to notify subscribers when an event occurs

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/design-patterns/observer-pattern#overview)

With the observer pattern, we have:

1. An **observable object**, which can be observed by subscribers in order to notify them.
2. **Subscribers**, which can subscribe to and get notified by the observable object.

For example, we can add the `logger` as a subscriber to the observable.

<video width="100%" height="100%" controls autoplay loop>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1661499081/FM%20Workshop/design-patterns/observable-pattern/observable2_nsxqmi.mov" type="video/mp4" />
</video>

When the `notify` method is invoked on the observable, all subscribers get invoked and (optionally) pass the data from the notifier to them.

<video width="100%" height="100%" controls autoplay>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1661499025/FM%20Workshop/design-patterns/observable-pattern/observable_dtcqep.mov" type="video/mp4" />
</video>

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/design-patterns/observer-pattern#implementation)

We can export a singleton Observer object, which contains a `notify`, `subscribe`, and `unsubscribe` method.

```js
const observers = [];

export default Object.freeze({
  notify: (data) => observers.forEach((observer) => observer(data)),
  subscribe: (func) => observers.push(func),
  unsubscribe: (func) => {
    [...observers].forEach((observer, index) => {
      if (observer === func) {
        observers.splice(index, 1);
      }
    });
  },
});
```

We can use this observable throughout the entire application, making it possible to subscribe functions to the observable

```js
import Observable from "./observable";

function logger(data) {
  console.log(`${Date.now()} ${data}`);
}

Observable.subscribe(logger);
```

and notify all subscribers based on certain events.

```js
import Observable from "./observable";

document.getElementById("my-button").addEventListener("click", () => {
  Observable.notify("Clicked!"); // Notifies all subscribed observers
});
```

---

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/design-patterns/observer-pattern#tradeoffs)

**Separation of Concerns**: The observer objects aren't tightly coupled to the observable object, and can be (de)coupled at any time. The observable object is responsible for monitoring the events, while the observers simply handle the received data.

**Decreased performance**: Notifying all subscribers might take a significant amount of time if the observer handling becomes too complex, or if there are too many subscibers to notify.