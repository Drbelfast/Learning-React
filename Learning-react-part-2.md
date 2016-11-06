The previous article mainly scratches the top what React.js can do.

And this article mainly focus on why React.js do this and the envolvment of React eco-system.

Let's all start with the pure and raw React.js development from beginning. 



### from the start

see [example 1]()

React is using `React.createElement` to create React Object (just pure JavaScript Object ) which can be rendered using `ReactDOM.render` method to actual real DOM.

Simple enough ?

### what if app becomes complicated.

what if I want to create some nested doms 

see [example 2]()

Things becomes complicated and more verbose and will definitely out of control when it becomes bigger.

>  If you are confused why `createElement` is taking arguments like that. just refer to their formal [API](https://facebook.github.io/react/docs/react-api.html)
>
> or in the reference 1.

### we can also use components to simplify a little bit

see [example 3]()

 remember we refered in article 1 that there are two types of components?

1. stateless function
2. statefull class with life cycle methods

The `propTypes` is just a react way to check property types. see [API](https://facebook.github.io/react/docs/typechecking-with-proptypes.html), We can also use [Flow]() or [TypeScript]() to type check the application. But in this very basic easy app, we are just going to use what React provides us. And will integrate the fancy techies in future articles.

### Add a read-only form

see [example 4]()

and add some css  styles 

see [example 5 ](),

Add some classes to `ContactItem`.  Here we are using `className` property to assign css classes because `class` is a reserved word in JavaScript.

Since React projects organize everything into components.  Let's put`rootElement` into a component

### Make the form Interactive

`props` can take string, array and functions

we can pass a callback function to `input` element

```javascript
React.createElement("input", {
    // The callback passed to `onChange` will be called when `value` should change
    onChange: function(syntheticEvent) {
        // Log new `value` to JavaScript console
        console.log(syntheticEvent.target.value)
    }
})
```

Modifying `ContactForm.propTypes` 

```javascript
propTypes: {
    contact: React.PropTypes.object.isRequired,
    onChange: React.PropTypes.func.isRequired,
}
```

Adding a console.log to our `ContactView` class to test

```javascript
React.createElement(ContactForm, {
    contact: this.props.newContact,
    onChange: function(contact) { console.log(contact) },
})
```










## References

1. [learn-raw-react-no-jsx-flux-es6-webpack/](http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/)

   Great article, also explains `propTypes` and how `ReactDOM.render` method actually work

2. [Learn Raw React: Ridiculously Simple Forms](http://jamesknelson.com/learn-raw-react-ridiculously-simple-forms/)

   ​