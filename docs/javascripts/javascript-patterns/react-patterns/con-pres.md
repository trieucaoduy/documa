---
title: Con-Pres Pattern
sidebar_position: 1
---


Enforce separation of concerns by separating the view from the application logic.

---

### [Overview](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#overview)

We can use the Container/Presentational pattern to separate the logic of a component from the view. To achieve this, we need to have a:

- **Presentational** Component, that cares about **how** data is shown to the user.
- **Container** Component, that cares about **what** data is shown to the user.

For example, if we wanted to show listings on the landing page, we could use a container component to fetch the data for the recent listings, and use a presentational component to actually render this data.

<video width="100%" height="100%" controls autoplay loop>
  <source src="https://res.cloudinary.com/dq8xfyhu4/video/upload/q_auto/v1653700248/FM%20Workshop/react-state-patterns/con-pres/Screen_Recording_2022-05-27_at_8.08.53_PM_kyd2eq.mov" type="video/mp4" />
</video>

---

### [Implementation](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#implementation)

We can implement the Container/Presentational pattern using either Class Components or functional components.

```js
import React from "react";
import { LoadingListings, Listing, ListingsGrid } from "../components";

function ListingsContainerComponent() {
  const [listings, setListings] = React.useState([]);

  React.useEffect(() => {
    fetch("https://my.cms.com/listings")
      .then((res) => res.json())
      .then((res) => setListings(res.listings));
  }, []);

  return <Listings listings={listings} />;
}

function ListingsPresentationalComponent(props) {
  if (props.listings.length === 0) {
    return <LoadingListings />;
  }

  return (
    <ListingsGrid>
      {listings.map((listing) => (
        <Listing listing={listing} />
      ))}
    </ListingsGrid>
  );
}
```

---

### [Tradeoffs](https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres#tradeoffs)

**Separation of concerns**: Presentational components can be pure functions which are responsible for the UI, whereas container components are responsible for the state and data of the application. This makes it easy to enforce the separation of concerns.

**Reusability**: We can easily reuse the presentational components throughout our application for different purposes.

**Flexibility**: Since presentational components don't alter the application logic, the appearance of presentational components can easily be altered by someone without knowledge of the codebase, for example a designer. If the presentational component was reused in many parts of the application, the change can be consistent throughout the app.

**Testing**: Testing presentational components is easy, as they are usually pure functions. We know what the components will render based on which data we pass, without having to mock a data store.

**Not necessary with Hooks**: Hooks make it possible to achieve the same result without having to use the Container/Presentational pattern.

For example, we can use SWR to easily fetch data and conditionally render the listings or the skeleton component. Since we can use hooks in functional components and keep the code small and maintainable, we don't have to split the component into a container and presentational component.

```js
import React from "react";
import useSWR from "swr";
import { LoadingListings, Listing, ListingsGrid } from "../components";

function Listings(props) {
  const {
    data: listings,
    loading,
    error,
  } = useSWR("https://my.cms.com/listings", (url) =>
    fetch(url).then((r) => r.json())
  );

  if (loading) {
    return <LoadingListings />;
  }

  return (
    <ListingsGrid>
      {listings.map((listing) => (
        <Listing listing={listing} />
      ))}
    </ListingsGrid>
  );
}
```

**Overkill**: The Container/Presentational pattern can easily be an overkill in smaller sized application.