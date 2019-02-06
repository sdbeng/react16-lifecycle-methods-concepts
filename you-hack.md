## Mounting
### constructor
The first thing that gets called is your component constructor, if your component is a class component. This does not apply to functional components.

Your constructor might look like so:
```
class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0,
    };
  }
}
```
The constructor gets called with the component props. You must call super and pass in the props.

You can then initialize your state, setting the default values. You can even base the state on the props:
```
class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: props.initialCounterValue,
    };
  }
}
```
Note that using a constructor is optional, and you can initialize your state like so if your Babel setup has support for class fields:
```
class MyComponent extends Component {
  state = {
    counter: 0,
  };
}
```
This approach is widely preferred. You can still base your state off props:
```
class MyComponent extends Component {
  state = {
    counter: this.props.initialCounterValue,
  };
}
```
You may still need a constructor, though, if you need to use a ref. Here’s an example from our grid app:
```
class Grid extends Component {
  constructor(props) {
    super(props);
    this.state = {
      blocks: [],
    };
    this.grid = React.createRef();
  }
  ```
We need the constructor to call createRef, to create a reference to the grid element, so we can pass it to bricks.js.

You can also use the constructor for function binding, which is also optional. 

**Most Common Use Case For Constructor: Setting up state, creating refs and method binding.**

## ff

## ff


## ff

## ff

## ff
