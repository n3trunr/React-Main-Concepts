# React-Main-Concepts
https://reactjs.org/docs/hello-world.html

# Hello World
The smallest React example looks like this:
```javascript
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```
It displays a heading saying “Hello, world!” on the page.

# Introducing JSX
Consider this variable declaration:
```javascript
const element = <h1>Hello, world!</h1>;
```

The tag stuff is JSX.

## <u>JSX is a syntax extension to JavaScript.</u>
*We recommend using it with React to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript.*
JSX produces React “elements”.

## <u>Embedding Expressions in JSX</u>
```javascript
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

You can put any valid JavaScript expression inside the curly braces in JSX. For example, 2 + 2, user.firstName, or formatName(user) are all valid JavaScript expressions.

In the example below, we embed the result of calling a JavaScript function, formatName(user), into an  < h1> element.

```javascript
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

## <u>JSX is an Expression Too</u>
you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions:

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

## <u>Specifying Attributes with JSX</u>

You may use quotes to specify string literals as attributes:

```javascript
const element = <a href="https://www.reactjs.org"> link </a>;
```

You may also use curly braces to embed a JavaScript expression in an attribute:
```javascript
const element = <img src={user.avatarUrl}></img>;

```

## <u>Specifying Children with JSX</u>
If a tag is empty, you may close it immediately with />, like XML:
```javascript
const element = <img src={user.avatarUrl} />;
```
JSX tags may contain children:
```javascript
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);

```

## <u>JSX Prevents Injection Attacks</u>
It is safe to embed user input in JSX:
```javascript
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.

## <u>JSX Represents Objects</u>
Babel compiles JSX down to React.createElement() calls.

These two examples are identical:
```javascript
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```
```javascript
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this:
```javascript
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

These objects are called “React elements”. You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date.

<div>

# Rendering Elements
*Elements are the smallest building blocks of React apps*

An element describes what you want to see on the screen:
```javascript
const element = <h1>Hello, world</h1>;
```

Note: *Components* **NOT SAME** as *Elements*. Elements are what components are made of. Unlike browser DOM elements, React elements are plain objects are cheap to create. react DOM takes care of updating the DOM to match the React elements. 

## <u>Rendering an Element into the DOM</u>
Let's say there is a ``` <div> ``` somewhere in your HTML file:
```javascript
<div id="root"></div>
```
call this a “root” DOM node because everything inside it will be managed by React DOM.

To render a React element, first pass the DOM element to ReactDOM.createRoot(), then pass the React element to root.render():
```javascript
const root = ReactDOM.createRoot(
  document.getElementById('root')
);
const element = <h1>Hello, world</h1>;
root.render(element);
```

## <u>Updating the Rendered Element</u>
React *elements* are IMMMUTABLE. 

ticking clock example:
```javascript
const root = ReactDOM.createRoot(
  document.getElementById('root')
);

function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

In practice, most React apps only call root.render() once. In the next sections we will learn how such code gets encapsulated into stateful components.

We recommend that you don’t skip topics because they build on each other.


## <u>React Only Updates What’s Necessary</u>

React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state






