## What is React

Guys in Facebook found the browser dom paint and render is slow, thus they proposed that change of dom tree could be actually be represented as JavaScript Object. 
After all transform and manipulation in JavaScript, output the result to browser to render dom just once.


And also, like html template, introduces `Components` for better reusibility and mantainence.


## A Very Easy Example of React

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="build/react.js"></script>
    <script src="build/react-dom.js"></script>
    <script src="build/JSXTransformer.js"></script>
  </head>
  <body>
    <div id="mount-point"></div>
    <script type="text/jsx">
      // React Code Goes Here
      ReactDOM.render(
        <h1>Hello, world!</h1>,
          document.getElementById('mount-point')
      );
    </script>
  </body>
</html>
```
1. `react.js`, the core functionality of Reactjs
2. `react-dom.js` the library to render react object to browser
3. `JSXTransformer.js` enable you to write HTML-ish tags in JavaScript, basically JSX is a JavaScript XML syntax transform.


> ReactDOM is support library and was introduced in recent version of React. 
> The React DOM implementation was initially in the React library but become a stand alone library in v0.14
> The reason to do so is Facebook is making `React-Native` and put all the core independent code in `React.js`
> `ReactDom.js` is only relevant to browser side.


## The Basics

### JSX
```JavaScript
<script type="text/jsx">
    // Using JXS
    // This is just a syntax surgar for calling React.createElement()
    ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('myDiv')
    );


    // Not using JXS 
    ReactDOM.render(
        React.createElement('h1', null, 'Hello!'),
        document.getElementById('myDiv')
    );
</script>
```
### Components
React's basic building blocks are called __components__.

There are two types of components:
1. functional component.

   used when the componet does not require much complexity.

2. class component. 

   which is exactly functional component plus state and life cycle methods.

functional component

```javascript
// without the use ES6
var MyComponent = function(props) {
  return (
  	<h1>Hello, world</h1>
  )
}

// with the use of ES6
const MyComponet = (props) => {
  return (
  	<h1>Hello, world</h1>
  )
}
```

class component

```javascript
// without the use of ES6 and automatically bind this to component
var MyComponent = React.createClass({
    render: function(){
        return (
            <h1>Hello, world!</h1>
        );
    }
});

// with the use of ES6
class MyComponent extends React.component {
  render() {
    return (
    	<h1>Hello, world!</h1>
    )
  }
}
  

ReactDOM.render(
    <MyComponent/>,
    document.getElementById('myDiv')
);
```

The `render` method is the only _required_ spec for creating component.

Some important LIFECYLE METHODS:

- __componentWillMount__ - Invoked once, on both client & server before rendering occurs
- __componentDidMount__ - Invoked once, only on the client, after rendering occurs.
- __shouldComponentUpdate__ - Returen value determines whether component should update.
- __componentWillUnmount__ - Invoked prior to unmounting component.

Some SPECS, but not used as in ES6

- __getInitialState__ - Return value is the initial value for state.

  in ES6, it is written as in constructor

  ```javascript
  class myComponent extends React.component {
    constructor(props) {
      super(props);
      // set inital state
      this.state = {count: 5}
    }
    render() {
      return(
      	<h1>{this.state.count}</h1>
      )
    }
  }

  // without es6 
  var MyComponent = React.createClass({
      getInitialState: function(){
          return {
              count: 5
          }
      },
      render: function(){
          return (
              <h1>{this.state.count}</h1>
          )
      }
  });
  ```

- __getDefaultProps__ - Sets fallback props values if props aren't supplied.

- __mixins__ - An array of objects, used to extend the current component's functionality.

## Events

React also has a built in cross browser events system. The events are attached as properties of components and can trigger methods.

```javascript
var Counter = React.createClass({
  incrementCount: function(){
    this.setState({
      count: this.state.count + 1
    });
  },
  getInitialState: function(){
     return {
       count: 0
     }
  },
  render: function(){
    return (
      <div class="my-component">
        <h1>Count: {this.state.count}</h1>
        <button type="button" onClick={this.incrementCount}>Increment</button>
      </div>
    );
  }
});

ReactDOM.render(<Counter/>, document.getElementById('mount-point'));
```



## Unidirectional Data Flow

Different from the two-way data binding in Angular or Vue.js, React only supports one-way data transfering with `state` (used inside component) and `props`(used in passing property to children) object. This means that in a multi component heirachy, a common parent component should manage the `state` and pass it down via `props`

And component will re-render only the `state` has changed. Thus, one cannot directly change properties in `state`. Always use `setState` method to ensure the UI refresh in sync.

[an example](http://codepen.io/kenwheeler/pen/jDKEo)

```javascript
var List = React.createClass({
  render: function(){
    return (
      <ul>
      {
        this.props.items.map(function(item) {
          return <li key={item}>{item}</li>
        })
       }
      </ul>
    )  
  }
});

var FilteredList = React.createClass({
  filterList: function(event){
    var updatedList = this.state.initialItems;
    updatedList = updatedList.filter(function(item){
      return item.toLowerCase().search(event.target.value.toLowerCase()) !== -1;
    });
    this.setState({items: updatedList});
  },
  getInitialState: function(){
     return {
       initialItems: [
         "Apples",
         "Broccoli",
         "Chicken",
         "Duck",
         "Eggs",
         "Fish",
         "Granola",
         "Hash Browns"
       ],
       items: []
     }
  },
  componentWillMount: function(){
    this.setState({items: this.state.initialItems})
  },
  render: function(){
    return (
      <div className="filter-list">
        <input type="text" placeholder="Search" onChange={this.filterList}/>
      <List items={this.state.items}/>
      </div>
    );
  }
});

React.renderComponent(<FilteredList/>, document.getElementById('mount-point'));
```





## Reference

1. [scotch.io reactjs basics](https://scotch.io/tutorials/learning-react-getting-started-and-concepts)



   ​

   ​