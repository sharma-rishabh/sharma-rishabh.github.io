---
title: "Intro to react"
date: 2022-09-26T22:08:42+05:30
draft: false
tags: 
  - tech
  - react
---

React is a frontend javascript framework which allows us to decouple the logic and rederning of an element in DOM.

## Creating an React Element

```js
React.createElement('Element name', props, ...children)
```

## Mounting a React Elment


After creating an element you will need a place to mount the element until then the element you created will not be present in HTML DOM.

The element you will mount your react element to is called root.

Lets assume this is your html structure and your react script is inside index.js.

```html
<html>
  <head>
    <title>webpage</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  </head>
  <body>
    <div id="container">
    <script src="index.js"></script>
    </div>
  </body>
</html>
```

```js
const container = document.getElementById('container');
const root = React.createRoot(container);
const para = React.createElement('p', {style:{color:'red'}}, 'Hello World');

root.render(para);
```

The syntax shown above gets the container element from html DOM, we make that our react root and then we create a p element with some text and color and using `root.render` we are able to mount our element to HTML DOM. The p will now appear inside the `#container`.


## What happens when render is called

Important thing to understand is what happens on a `root.render` call, render is not responsible to add p element to html DOM, render add this p to React DOM then react figures out that it's dom and HTML DOM are no in sync so it repaints the element which has changed in this case our root element.

One thing to note is that render assumes you are blowing stuff away so if your try to render more than one react element on the same root, it will unmount the first element and then it will mount the next one. `render` doesn't blow away the already present html elements only the react elements.


If you want to learn how to create your own react component [click here](/posts/create_your_react_component)