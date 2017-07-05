# React

## JSX

```jsx
const inlineCode = <div>Text</div>;
const multilineCode = (
  <div id="literal-string">
    <span>Text</span>
  </div>
);
const expressionCode = (
  <div id={someValue} className={classString}> // no quotes here
    <span>{isCorrect ? "Yes" : "No"}</span> // can be multiline too
  </div>
);
```

> Inserted values are always escaped

## Root render

```jsx
ReactDOM.render(
  <Board />,
  document.getElementById('root')
);
```

## Component schema

### `class` type

```jsx
class Board extends React.Component {
  renderSquare(i) { // sample helper method
    return <Square value={i} onClick={() => handleClick()} />; // pass method to child component
  }
}

class Square extends React.Component {
  constructor(props) { // props object with attributes data
    super(props); // should be always added
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square" // set class
        onClick={() => this.props.onClick()}> // invoke passed method in parent component
        {this.props.value} // use prop value
      </button>
    );
  }
}
```

### `function` type

```jsx
function Square(props) {
  return ( // only return, without `render()`
    <button className="square"
      onClick={props.onClick}> // do NOT add `()`
      {props.value} // do NOT add `this`
    </button>
  );
}
```

> Limits: Function type cannot use `state` object nor conatins helper functions.

## Build-in controller objects

- `props` - tag attributes (immutable), gathered from constructor parameter, can be used in `render()`
- `state` - private properties of the component, defined in constructor, can be used in `render()`

> Do NOT update `state` directly, use `setState()` instead.

> Additional ones can be added to class but not used in `render()` method.

## Build-in controller methods

- `render()` - returns JSX code to render
- `setState({newState})` - update `this.state`'s object properties (one or many)
- `setState((prevState[, props]) => {newState})` - use previous state (and props) in function
- `componentDidMount()` - lifecycle hook called when mounted in DOM
- `componentWillUnmount()` - lifecycle hook called when unmounted from DOM

## Conditional rendering

### By `null`

```jsx
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}
```

### By ternary operator

```jsx
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```

### By JavaScript autism

```jsx
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div> // (╯°□°）╯︵ ┻━┻
  );
}
```

## Enumeration

### List

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number[, index]) =>
    <li key={number.toString()}> // or `index`
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

> - Key have to be unique only in specific array scope, not in global scope.
> - Key is not passed to component.