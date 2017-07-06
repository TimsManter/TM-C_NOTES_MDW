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

> - Do NOT update `state` directly, use `setState()` instead.
> - Additional ones can be added to class but not used in `render()` method.
> - `props` has special property `children` which contains component nested element.

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

## Forms

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault(); // to prevent submitting form
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Textarea

```jsx
<textarea value={this.state.value} onChange={this.handleChange} />
```

### Select

```jsx
<select value={this.state.value} onChange={this.handleChange}>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

### Naming elements

```jsx
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true, // first input
      numberOfGuests: 2 // second input
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value // short syntax...
    });

    /* ...for:
    var partialState = {};
    partialState[name] = value;
    this.setState(partialState); */
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```