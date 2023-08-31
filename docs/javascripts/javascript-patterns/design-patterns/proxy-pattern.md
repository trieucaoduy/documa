---
title: Proxy Pattern
sidebar_position: 3
---


Intercept and control interactions to target objects

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/design-patterns/proxy-pattern#overview)

The **Proxy Pattern** uses a **Proxy** intercept and control interactions to target objects.

Let's say that we have a `person` object. We can access properties with either dot or bracket notation,

<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653361839/FM%20Workshop/design-patterns/proxy-pattern/proxy1_gdxego.mov" type="video/mp4" />
</video>

and modify property values in a similar fashion.

<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653361839/FM%20Workshop/design-patterns/proxy-pattern/proxy2_px4kua.mov" type="video/mp4" />
</video>

With the Proxy pattern, we don't want to interact with this object directly. Instead, a Proxy object intercepts the request, and (optionally) forwards this to the target object - the `person` object in this case.

<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1661499156/FM%20Workshop/design-patterns/proxy-pattern/proxy3_ztjb5i.mov" type="video/mp4" />
</video>

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/design-patterns/proxy-pattern#implementation)

In JavaScript, we can easily create a new proxy by using the built-in `Proxy` object.

![Proxy](https://javascriptpatterns.vercel.app/design-patterns/proxy-pattern/001.png)

The `Proxy` object receives two arguments:

1. The target object
2. A handler object, which we can use to add functionality to the proxy. This object comes with some built-in functions that we can use, such as `get` and `set`.

The `get` method on the handler object gets invoked when we want to access a property, and the `set` method gets invoked when we want to modify a property.

```js
const person = {
  name: "John Doe",
  age: 42,
  email: "john@doe.com",
  country: "Canada",
};

const personProxy = new Proxy(person, {
  get: (target, prop) => {
    console.log(`The value of ${prop} is ${target[prop]}`);
    return target[prop];
  },
  set: (target, prop, value) => {
    console.log(`Changed ${prop} from ${target[prop]} to ${value}`);
    target[prop] = value;
    return true;
  },
});
```

---

#### [`Reflect`](https://javascriptpatterns.vercel.app/patterns/design-patterns/proxy-pattern#reflect)

The built-in `Reflect` object makes it easier to manipulate the target object.

Instead of accessing properties through `obj[prop]` or setting properties through `obj[prop] = value`, we can access or modify properties on the target object through `Reflect.get()` and `Reflect.set()`. The methods receive the same arguments as the methods on the handler object.

---

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/design-patterns/proxy-pattern#tradeoffs)

**Control**: Proxies make it easy to add functionality when interacting with a certain object, such as validation, logging, formatting, notifications, debugging.

**Long handler execution**: Executing handlers on every object interaction could lead to performance issues.