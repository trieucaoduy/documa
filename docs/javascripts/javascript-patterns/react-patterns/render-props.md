---
title: Render Props Pattern
sidebar_position: 3
---

Pass JSX elements to components through props

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/react-patterns/render-props#overview)

With the Render Props pattern, we pass components as props to other components. The components that are passed as props can in turn receive props from that component.

Render props make it easy to reuse logic across multiple components.

<video width="100%" height="100%" controls autoplay loop>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653712978/FM%20Workshop/react-state-patterns/render-props-pattern/Screen_Recording_2022-05-27_at_11.42.05_PM_h5i8tf.mov" type="video/mp4" />
</video>

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/react-patterns/render-props#implementation)

If we wanted to implement an `input` field with which a user can convert a temperature from Celsius to Kelvin and Fahrenheit, we can use the `renderKelvin` and `renderFahrenheit` render props.

These props receive the `value` of the input, which they convert to the correct temperature in either K or °F.

```
function Input(props) {
  const [value, setValue] = useState("");

  return (
    <>
      <input value={value} onChange={(e) => setValue(e.target.value)} />
      {props.renderKelvin({ value: value + 273.15 })}
      {props.renderFahrenheit({ value: (value * 9) / 5 + 32 })}
    </>
  );
}

export default function App() {
  return (
    <Input
      renderKelvin={({ value }) => <div className="temp">{value}K</div>}
      renderFahrenheit={({ value }) => <div className="temp">{value}°F</div>}
    />
  );
}
```

---

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/react-patterns/render-props#tradeoffs)

**Reusability**: Since render props can be different each time, we can make components that receive render props highly reusable for multiple usecases.

**Separation of concerns**: We can separate our app's logic from rendering components through render props. The stateful component that receives a render prop can pass the data onto stateless components, which merely render the data.

**Solution to HOC problems**: Since we explicitly pass props, we solve the HOC's implicit props issue. The props that should get passed down to the element, are all visible in the render prop's arguments list. We know exactly where certain props come from.

**Unnecessary with Hooks**: Hooks changed the way we can add reusability and data sharing to components, which can replace the render props pattern in many cases.