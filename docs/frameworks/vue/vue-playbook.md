---
title: Vue Playbook
sidebar_position: 1
---


All things we need to know about Vue framework

---

## 1. Essentials
### 1.1. Reactivity Fundamentals

- Refs is used for premitive value case while reactive is used for non-premitive value:
```tsx
// premitive value (string, number,...)
const value = ref<string>('String');


// non-premitive value (Object, array, map,...)
interface IValue {
  name: string,
  old: number,
}

const value = reactive<IValue>({ name: 'Blue', old: 17 });
```

### 1.2. Computed properties

- Auto excute code depend on reactive dependencies (similar like useEffect React)
- Value will be computed and cached depend on reactive dependencies. This mean we can access and get value computed before immediately without re-computed.
- Computed should be used for pure computed, it's shouldn't used for handle async/side-effect.
```tsx
const now = computed(() => Date.now())
```

### 1.3. Class and style bindings

- We can combine *reactive fundamentals* and *computed property* to bindings styles or class with conditional
```tsx
const isActive = ref(true)
const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error?.value?.type === 'fatal'
}))

<div :class="classObject"></div>
```

- :style support both camelCase and kebab-case
```tsx
<div :style="{ 'font-size': fontSize + 'px' }"></div>
```
 or
```tsx
<div :style="{ fontSize: fontSize + 'px' }"></div>
```

- We should bindings a style object directly for cleaner template
```tsx
const styleObject = reactive({
  color: 'red',
  fontSize: '13px'
})

<div :style="styleObject"></div>
```

- We can provide an array of multiple (prefixed) value to bindings style property, browser will render the last property of array what was supported
```tsx
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

## 2. Components In-Depth
## 3. Reusability
## 4. Built-in Components
## 5. Scaling Up
## 6. Best Practices
## 7. TypeScript
