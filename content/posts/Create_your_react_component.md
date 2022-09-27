---
title: "Create your react component"
date: 2022-09-27T22:13:50+05:30
draft: false
tags:
  - tech
  - react
---

Creating your own react component is supereasy.

## Syntax

```js
class MyElement extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return react.createElement('p',null,'This is some text');
  }
}
```

### Or

```js
const myElement = (props) =>{
  return react.createElement('p',null,'This is some text')
}
```

Here we have seen two ways to create a react component one using classes the other using simple arrow function.

## How to use it

```js
const myElement = react.createElement(MyElement);
root.render(myElement);
```

Two important things happen here.

- First `react.createElement` creates a react representation of your component.

- Second `root.render` actually invokes your class to create the react component and mounts it to react DOM.

## Why do we need a render method in our class?

Our class is only constructed when root `root.render` is called which then invokes the render method in our class which should return the element we want to mount to the root.

## Example

Let's look at a simple stateful example to understand use of creating your own react component.

In this example we want a button which will say click me and once it is clicked it will be replaced with a `p` which says `You clicked a button`

We will see a lot more with this example which I will explain after the example.

```js
class MyButton extends React.Component {
  constructor(props) {
    super(props);
    this.state={clicked:false}
  }

  render() {
    const button = React.createElement('button',
    {
      onClick:()=>{
        return this.setState((state)=>return state.clicked=true);
      }
    },'Click me');

    const p = React.createElement('p',null,'You clicked a button');

    return this.state.clicked ? p : button;
  }
}


const button = React.createElement(MyButton);
root.render(button);
```
In the above example in the render method of the `MyButton` class we are making a decision on what to render the basis of current state of the button.

### What is `this.setState`?

It is a method defined in super of `MyButton` which takes a function which gets state and if you return something from this function if before and after the invocation of `this.setState` the state is different than `render` is called. One cool effect of this is that react won't rerender your component until there is a state change so redrawing will be minimal.

So what we did in above example is that we created a button which when clicked sets the `clicked` property as true inside `state` and on the basis of `clicked` we are returning either a p or that button.


Hopefully this example helps you to understand the use of custom react components.