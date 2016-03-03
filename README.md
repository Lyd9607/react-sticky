react-sticky [![Build Status](https://travis-ci.org/captivationsoftware/react-sticky.svg?branch=master)](https://travis-ci.org/captivationsoftware/react-sticky)
============

### [Demo](https://captivationsoftware.github.io/react-sticky)

NOTE: Version 4.0.0 is in progress -- [3.0.0](https://github.com/captivationsoftware/react-sticky/tree/3.0.0)
 was the last stable version.

The most powerful Sticky library available for React!

##### Highlights:
  - Fully-nestable, allowing you to build awesome layouts with familiar syntax
  - Sane defaults so you spend less time configuring
  - Allows multiple Sticky elements on the page at once with compositional awareness!

## Installation
```sh
npm install react-sticky
```

Tip: run `npm build` to build the compressed UMD version suitable for inclusion via CommonJS, AMD, and even good old fashioned `<script>` tags (available as `ReactSticky`).

## Overview & Basic Example

It all starts with a `<StickyContainer />`. This is basically a plain ol' `<div />` with a React-managed `padding-top` css attribute. As you scroll down the page, all `<Sticky />` tags within
will be constrained to the bounds of its immediate parent `<StickyContainer />`.

The elements you actually want to "stick" should be wrapped in the, you guessed it, `<Sticky />` tag. The full list of props are available below, but typical usage will look something like so:

app.jsx
```js
import React from 'react';
import { StickyContainer, Sticky } from 'react-sticky';

class App extends React.Component ({
  render() {
    return (
      <StickyContainer>

        <Sticky>
          <header>
            <h1>Million Dollar App Idea</h1>
          </header>
        </Sticky>

        <h3>Reasons to trust me</h3>
        <ul>
          <li>I have great hygeine</li>
          <li>I signal before most turns</li>
          ...
          <li>I bought a newspaper subscription to help a kid go to college</li>
        </ul>

      </StickyContainer>
    );
  },
});

```

When the "stickiness" becomes activated, the following css style rules are applied to the Sticky element:

```css
  position: fixed;
  top: 0;
  left: 0;
  width: < width is inherited from the closest StickyContainer >
```

### `<StickyContainer />` Props
`<StickyContainer />` passes along all props you provide to it without interference*. That's right - no restrictions - go `prop` crazy!  

* IMPORTANT: The `style` attribute `padding-top` is managed by React, so avoid setting it with CSS rules.

### `<Sticky />` Props
#### stickyStyle
In the event that you wish to override the style rules applied, simply pass in the style object as a prop:

app.jsx
```js
<StickyContainer>
  <Sticky stickyStyle={customStyleObject}>
    <header />
  </Sticky>
</StickyContainer>
```

Note: You likely want to avoid messing with the following attributes in your stickyStyle: `left`, `top`, and `width`.

#### stickyClass
You can also specify a class name ('sticky' by default) to be applied when the element becomes sticky:

app.jsx
```js
<StickyContainer>
  ...
  <Sticky stickyClass={customClassName}>
    <header />
  </Sticky>
  ...
</StickyContainer>
```

If you wish to use external CSS rules instead of inline styles, first ask yourself if you're sure, because you probably don't. But, if you feel like being reckless, pass an empty object to the stickyStyle property. Doing so will prevent the default inline styles from taking precedence over your own CSS rules. An example of how to do this is found below:

app.jsx
```js
<StickyContainer>
  ...
  <Sticky stickyClass="supersticky" stickyStyle={{}}>
    <header />
  </Sticky>
  ...
</StickyContainer>
```

#### topOffset
Sticky state will be triggered when the top of the element is `topOffset` pixels from the top of the window (0 by default). Positive numbers give the impression of a lazy sticky state, whereas negative numbers are more eager in their attachment.

app.jsx
```js
<StickyContainer>
  ...
  <Sticky topOffset={80}>
    <SomeChild />
  </Sticky>
  ...
</StickyContainer>
```

The above would result in an element that becomes sticky once its top is greater than or equal to 80px away from the top of the <StickyContainer />.


#### className
You can specify a class name that would be applied to the resulting element:

app.jsx
```js
<StickyContainer>
  ...
  <Sticky className={className}>
    <header />
  </Sticky>
  ...
</StickyContainer>
```

#### style
You can also specify a style object that would be applied to the resulting element:

app.jsx
```js
<StickyContainer>
  ...
  <Sticky style={{background: 'red'}}>
    <header />
  </Sticky>
</StickyContainer>
```

Note: In the event that `stickyStyle` rules conflict with `style` rules, `stickyStyle` rules take precedence ONLY while sticky state is active.

#### onStickyStateChange

Use the onStickyStateChange prop to fire a callback function when the sticky state changes:

app.jsx
```js
<StickyContainer>
  ...
  <Sticky onStickyStateChange={this.handleStickyStateChange}>
    <header />
  </Sticky
  ...
</StickyContainer>
```

## Supported By

##### [Captivation Software](http://www.captivationsoftware.com)

## License

MIT License
