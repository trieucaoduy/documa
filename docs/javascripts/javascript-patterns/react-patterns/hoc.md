---
title: HOC Pattern
sidebar_position: 2
---

Pass reusable logic down as props to components throughout your application

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/react-patterns/higher-order-component#overview)

Higher-Order Components (HOC) make it easy to pass logic to components by wrapping them.

For example, if we wanted to easily change the styles of a text by making the font larger and the font weight bolder, we could create two Higher-Order Components:

- `withLargeFontSize`, which appends the `font-size: "90px"` field to the `style` attribute.
- `withBoldFontWeight`, which appends the `font-weight: "bold"` field to the `style` attribute.

<video width="100%" height="100%" controls autoplay loop>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653702078/FM%20Workshop/react-state-patterns/hoc-pattern/Screen_Recording_2022-05-27_at_8.39.40_PM_apuejc.mov" type="video/mp4" />
</video>

Any component that's wrapped with either of these higher-order components will get a larger font size, a bolder font weight, or both!

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/react-patterns/higher-order-component#implementation)

We can apply logic to another component, by:

1. Receiving another component as its `props`
2. Applying additional logic to the passed component
3. Returning the same or a new component with additional logic

![HOC](https://javascriptpatterns.vercel.app/react-state-patterns/hoc-pattern/1.png)

To implement the above example, we can create a `withStyles` HOC that adds a `color` and `font-size` prop to the component's style.

```js
export function withStyles(Component) {
  return (props) => {
    const style = {
      color: "red",
      fontSize: "1em",
      // Merge props
      ...props.style,
    };

    return <Component {...props} style={style} />;
  };
}
```

We can import the `withStyles` HOC, and wrap any component that needs styling.

```js
import { withStyles } from "./hoc/withStyles";

const Text = () => <p style={{ fontFamily: "Inter" }}>Hello world!</p>;
const StyledText = withStyles(Text);
```

If you have a component that always needs to be wrapped within a HOC, you can also directly pass it instead of creating two separate components like we did in the example above.

```js
const Text = withStyles(() => (
  <p style={{ fontFamily: "Inter" }}>Hello world!</p>
));
```

---

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/react-patterns/higher-order-component#tradeoffs)

**Separation of concerns**: Using the Higher-Order Component pattern allows us to keep logic that we want to re-use all in one place. This reduces the risk of accidentally spreading bugs throughout the application by duplicating code over and over, potentially introducing new bugs each time

**Naming collisions**: It can easily happen that the HOC overrides a prop of a component. Make sure that the HOC can handle accidental name collision, by either renaming the prop or merging the props.

```js
function withStyles(Component) {
  return props => {
    const style = {
      padding: '0.2rem',
      margin: '1rem',
      // Merge props
      ...props.style
    }

    return <Component {...props} style={style} />
  }
}

// The `Button` component has a `style` prop, that shouldn't get overwritten in the HOC.
const Button = () = <button style={{ color: 'red' }}>Click me!</button>
const StyledButton = withStyles(Button)
```

**Readability**: When using multiple composed HOCs that all pass props to the element that's wrapped within them, it can be difficult to figure out which HOC is responsible for which prop. This can hinder debugging and scaling an application easily.