---
title: Module Pattern
sidebar_position: 1
---


Split up your code into smaller, reusable pieces

---

## [Overview](https://javascriptpatterns.vercel.app/patterns/design-patterns/module-pattern#overview)

ES2015 introduced built-in JavaScript modules. A module is a file containing JavaScript code and makes it easy to expose and hide certain values.

The module pattern is a great way to split a larger file into **multiple smaller**, **reusable pieces**. It also promotes **code encapsulation**, since the values within modules are kept private inside the module by default, and cannot be modified. Only the values that are explicitly exported with the `export` keyword are accessible to other files.

<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653682630/FM%20Workshop/design-patterns/module-pattern/Screen_Recording_2022-05-27_at_3.15.38_PM_j40sjt.mov" type="video/mp4" />
</video>

The module pattern provides a way to have both public and private pieces with the `export` keyword. This protects values from leaking into the global scope or ending up in a naming collision.

<video width="100%" height="100%" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1654008290/FM%20Workshop/design-patterns/module-pattern/Screen_Recording_2022-05-31_at_9.43.04_AM_dbq340.mov" type="video/mp4" />
</video>

In the above example, the `secret` variable is accessible within the module, but not outside of it. Other modules cannot import this value, as it hasn't been `export`ed.

---

Without modules, we can access properties defined in scripts that are loaded prior to the currently running script.

With modules however, we can only use the values that have been exported.

---

## [Implementation](https://javascriptpatterns.vercel.app/patterns/design-patterns/module-pattern#implementation)

There are a few ways we can use modules.

### [HTML tag](https://javascriptpatterns.vercel.app/patterns/design-patterns/module-pattern#html-tag)

When adding JavaScript to HTML files directly, you can use modules by adding the `type="module"` attribute to the `script` tags.
<video width="100%" height="500" controls>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653509683/FM%20Workshop/design-patterns/module-pattern/Screen_Recording_2022-05-25_at_3.12.53_PM_t2xcdy.mov" type="video/mp4" />
</video>

### [Node](https://javascriptpatterns.vercel.app/patterns/design-patterns/module-pattern#node)

In Node, you can use ES2015 modules either by:

- Using the `.mjs` extension
- Adding `"type": "module"` to your `package.json`

---

## [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/design-patterns/module-pattern#tradeoffs)

**Encapsulation**: The values within a module are scoped to that specific module. Values that aren't explicitly exported are not available outside of the module.

**Reusability**: We can reuse modules throughout our application

---