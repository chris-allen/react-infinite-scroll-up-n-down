React Infinite Scroll Up n Down
===============================

[![Build Status](https://travis-ci.com/chris-allen/react-infinite-scroll-up-n-down.svg?branch=master)](https://travis-ci.com/chris-allen/react-infinite-scroll-up-n-down)
[![npm](https://img.shields.io/npm/dt/react-infinite-scroll-up-n-down.svg?style=flat-square)](https://www.npmjs.com/package/react-infinite-scroll-up-n-down)
[![React Version](https://img.shields.io/badge/React-%5E0.14.9%20%7C%7C%20%5E15.3.0%20%7C%7C%20%5E16.0.0-blue.svg?style=flat-square)](https://www.npmjs.com/package/react)
[![npm](https://img.shields.io/npm/v/react-infinite-scroll-up-n-down.svg?style=flat-square)](https://www.npmjs.com/package/react-infinite-scroll-up-n-down)
[![npm](https://img.shields.io/npm/l/react-infinite-scroll-up-n-down.svg?style=flat-square)](https://github.com/chris-allen/react-infinite-scroll-up-n-down/blob/master/LICENSE)

Infinitely load content using a React Component. This fork maintains a simple, lightweight infinite scroll package that supports both `window` and scrollable elements.

- [Demo](https://chris-allen.github.io/react-infinite-scroll-up-n-down/demo/)
- [Demo Source](https://github.com/chris-allen/react-infinite-scroll-up-n-down/blob/master/docs/src/index.js)

## Installation

```
npm install react-infinite-scroll-up-n-down --save
```
```
yarn add react-infinite-scroll-up-n-down
```

## How to use

```js
import InfiniteScroll from 'react-infinite-scroll-up-n-down';
```

### Window scroll events

```js
<InfiniteScroll
    pageStart={0}
    loadMore={loadFunc}
    hasMore={true || false}
    loader={<div className="loader" key={0}>Loading ...</div>}
>
    {items} // <-- This is the content you want to load
</InfiniteScroll>
```

### DOM scroll events

```js
<div style="height:700px;overflow:auto;">
    <InfiniteScroll
        pageStart={0}
        loadMore={loadFunc}
        hasMore={true || false}
        loader={<div className="loader" key={0}>Loading ...</div>}
        useWindow={false}
    >
        {items}
    </InfiniteScroll>
</div>
```

### Custom parent element

You can define a custom `parentNode` element to base the scroll calulations on.

```js
<div style="height:700px;overflow:auto;" ref={(ref) => this.scrollParentRef = ref}>
    <div>
        <InfiniteScroll
            pageStart={0}
            loadMore={loadFunc}
            hasMore={true || false}
            loader={<div className="loader" key={0}>Loading ...</div>}
            useWindow={false}
            getScrollParent={() => this.scrollParentRef}
        >
            {items}
        </InfiniteScroll>
    </div>
</div>
```

## Props

| Name                       | Type          | Default    | Description|
|:----                       |:----          |:----       |:----|
| `element`                  | `Component`   | `'div'`    | Name of the element that the component should render as.|
| `hasMore`                  | `Boolean`     | `false`    | Whether there are more items to be loaded. Event listeners are removed if `false`.|
| `initialLoad`              | `Boolean`     | `true`     | Whether the component should load the first set of items.|
| `isReverse`                | `Boolean`     | `false`    | Whether new items should be loaded when user scrolls to the top of the scrollable area.|
| `adjustReverseScroll`      | `Boolean`     | `false`    | Whether the scrollTop should be adjusted when adding items with `isReverse` set to `true`.|
| `loadMore`                 | `Function`    |            | A callback when more items are requested by the user. Receives a single parameter specifying the page to load e.g. `function handleLoadMore(page) { /* load more items here */ }` }|
| `loader`                   | `Component`   |            | A React component to render while more items are loading. The parent component must have a unique key prop. |
| `pageStart`                | `Number`      | `0`        | The number of the first page to load, With the default of `0`, the first page is `1`.|
| `getScrollParent`          | `Function`    |            | Override method to return a different scroll listener if it's not the immediate parent of InfiniteScroll. |
| `threshold`                | `Number`      | `250`      | The distance in pixels before the end of the items that will trigger a call to `loadMore`.|
| `useCapture`               | `Boolean`     | `false`    | Proxy to the `useCapture` option of the added event listeners.|
| `useWindow`                | `Boolean`     | `true`     | Add scroll listeners to the window, or else, the component's `parentNode`.|
