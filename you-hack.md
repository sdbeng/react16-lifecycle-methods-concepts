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

## getDerivedStateFromProps
When mounting, getDerivedStateFromProps is the last method called before rendering. You can use it to set state according to the initial props. Here’s the code from the example Grid component:
```
static getDerivedStateFromProps(props, state) {
  return { blocks: createBlocks(props.numberOfBlocks) };
}
```
We look at the numberOfBlocks prop, and then use that to create a set of randomly sized blocks. We then return our desired state object.

Here’s what calling console.log(this.state) afterwards looks like:
```
console.log(this.state);
// -> {blocks: Array(20)}
```
Note that we could have placed this code in the constructor. The advantage of getDerivedStateFromProps is that it is more intuitive—it’s only meant for setting state, whereas a constructor has multiple uses. getDerivedStateFromProps is also called both before mount and before updating, as we’ll see in a bit.

**Most Common Use Case For getDerivedStateFromProps (during mount): Returning a state object based on the initial props.

## render
Rendering does all the work. It returns the JSX of your actual component. When working with React, you’ll spend most of your time here.

**Most Common Use Case For Render: Returning component JSX.**

## componentDidMount
After we’ve rendered our component for the first time, this method is called.

If you need to load data, here’s where you do it. Don’t try to load data in the constructor or render or anything crazy. I’ll let Tyler McGinnis explain why:

You can’t guarantee the AJAX request won’t resolve before the component mounts. If it did, that would mean that you’d be trying to setState on an unmounted component, which not only won’t work, but React will yell at you for. Doing AJAX in componentDidMount will guarantee that there’s a component to update.
You can read more of his answer here.

componentDidMount is also where you can do all the fun things you couldn’t do when there was no component to play with. Here are some examples:

- draw on a <canvas> element that you just rendered
- initialize a masonry grid layout from a collection of elements
- add event listeners
Basically, here you want to do all the setup you couldn’t do without a DOM, and start getting all the data you need.

Here’s our example app:
```
componentDidMount() {
    this.bricks = initializeGrid(this.grid.current);
    layoutInitialGrid(this.bricks)
    this.interval = setInterval(() => {
      this.addBlocks();
    }, 2000);
  }
  ```
We use the bricks.js library (called from the initializeGrid method) to create and arrange the grid.

We then set an interval to add more blocks every two seconds, mimicking the loading of data. You can imagine this being a loadRecommendations call or something in the real world.

**Most Common Use Case for componentDidMount: Starting AJAX calls to load in data for your component.



## ff


## ff

## ff

## ff
