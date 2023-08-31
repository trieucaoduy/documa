---
slug: the-harmony-between-vue-composition-api-and-react-hooks
title: The harmony between VUE Composition API and React Hooks
authors: [trieucd]
tags: [vue, composition api, react hooks, harmony]
---

In Vue 3, the Composition API was introduced to provide a more flexible and scalable way of organizing and reusing code in Vue components. It's similar in spirit to React hooks but with some Vue-specific features. The Composition API allows you to break down component logic into reusable functions called "composition functions." These composition functions can be composed together to create a more modular and maintainable codebase.

Here are some of the core composite APIs in Vue that are similar to React hooks:

1. **`ref` and `reactive`**: These APIs are similar to React's `useState` hook. They allow you to create reactive data that can trigger updates in the component when changed. The difference between them is that `ref` is used for creating a single reactive value, while `reactive` is used to create a reactive object.

   ```tsx
   import { ref, reactive } from 'vue';

   const count = ref(0); // Similar to useState(0)
   const state = reactive({ text: 'Hello' }); // Similar to useState({ text: 'Hello' })
   ```

2. **`computed`**: This API is similar to React's `useMemo` hook. It allows you to create a computed property that is derived from reactive data. Computed properties are cached and only recalculated when their dependencies change.

   ```tsx
   import { computed } from 'vue';

   const doubleCount = computed(() => count.value * 2); // Similar to useMemo(() => count * 2, [count])
   ```

3. **`watch`**: This API is similar to React's `useEffect` hook. It allows you to perform side effects when a reactive dependency changes.

   ```tsx
   import { watch } from 'vue';

   watch(count, (newValue, oldValue) => {
     console.log(`Count changed from ${oldValue} to ${newValue}`);
   }); // Similar to useEffect(() => { ... }, [count])
   ```

4. **`toRefs`**: This API is used to create a reactive reference to each property of a reactive object. This is particularly useful when you want to destructure reactive properties.

   ```tsx
   import { toRefs } from 'vue';

   const { text } = toRefs(state); // Destructuring reactive properties
   ```

5. **`onMounted`, `onUpdated`, `onUnmounted`**: These APIs are similar to React's `useEffect` with specific triggers. They allow you to perform side effects when a component is mounted, updated, or unmounted, respectively.

   ```tsx
   import { onMounted, onUnmounted } from 'vue';

   onMounted(() => {
     console.log('Component mounted');
   }); // Similar to useEffect(() => { ... }, [])

   onUnmounted(() => {
     console.log('Component unmounted');
   }); // Similar to useEffect(() => { return () => { ... } }, [])
   ```

6. **`provide` and `inject`**: These APIs are similar to React's Context API. They allow you to provide and access values across the component tree without prop drilling.

   ```tsx
   import { provide, inject } from 'vue';

   const SomeContext = Symbol();

   const ParentComponent = {
     setup() {
       provide(SomeContext, 'Hello from parent');
     }
   };

   const ChildComponent = {
     setup() {
       const message = inject(SomeContext);
       // message === 'Hello from parent'
     }
   };
   ```

These are just some of the core composition APIs in Vue that allow you to structure your code in a more modular and reusable way. Just like React hooks, the Composition API empowers developers to create cleaner and more maintainable code by encapsulating related logic into separate composition functions.