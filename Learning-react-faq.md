### Why use parenthesis on JavaScript return statements

[answer](http://jamesknelson.com/javascript-return-parenthesis)

### Why do we need key attribute in array children?

cited from [here](http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/)

To under stand this question, let first see how `ReactDOM.render` works

The first call to `ReactDOM.render` is simple - it walks through the passed in `ReactElement` and creates a corresponding HTML tree under `#react-app` . But look at following example

```javascript
var rootElement = React.createElement(ApplicationComponent, data)
ReactDOM.render(rootElement, document.getElementById('react-app'))
ReactDOM.render(rootElement, document.getElementById('react-app'))
```

The second call actually do nothing. this is because the corresponding `ReactElement` Object has not changed.

In order to decide _what_ to change, React compares the new `ReactElement` tree with the previous one. It uses a number of rules to decide what to do:

- `ReactElement`s with differeing types are trashed and re-rendered
- `ReactElement`s with differing props or children are re-rendered in place
- Identical `ReactElement`s which have been re-ordered within an array are moved to reflect the new order.

There is one more catch - when React encounters an array of `ReactElement`s with identical `type` and `props`, despite _looking_ identical from the outside it cannot know that they are really identical. This is because elements can have internal state - for example, whether the element currently has user focus. This becomes a problem when React goes to re-render those elements, as it cannot tell one from another - and thus doesn't know if their order within the array has changed.

This is where the `key` property from the earlier examples come in. It lets React distinguish between elements, and keep the DOM aligned with our `ReactElement` tree.

### controlled and uncontrolled input
[answer](https://gist.github.com/markerikson/d71cfc81687f11609d2559e8daee10cc)