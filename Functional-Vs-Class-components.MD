### Recap: Understanding Functional and Class Component

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Vs 

```
class Welcome extends Component {
  
  constructor(props){
    console.log(this.props)// undefined
    super();
  }
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

```
<Welcome name="Mentees" />
```

**Simple use:**

A functional component = is just a `plain JavaScript function` which accepts props as an argument and returns a React element.

A class component = requires you to `extend from React.Component` and create a `render function` which returns a React element.


***as you can see both have the same implementation.***


**Functional Component:**

A functional component `formerly` called a `stateless component`.

Why? 

 - setState() is not Available in `class component`
 - Did not support lifecycles e.g `componentDidMount()` https://www.w3schools.com/react/react_lifecycle.asp

But version 16.8 introduce react `Hooks` that supports `events` and `states`.

- useState() = https://reactjs.org/docs/hooks-state.html
- useEffect() = https://reactjs.org/docs/hooks-effect.html


**Some reason why not using `class` components for writing tests?**

- Side effects that occur as part of the component lifecycle (componentDidMount, componentWillUnmount, etc)

See example: https://dev.to/craigmichaelmartin/react-hooks-are-a-more-accurate-implementation-of-the-react-mental-model-1k49

```
 componentDidMount(){
  //Side effects (I/O, network, disk, etc.)
 }
```

### When to use class component?

1. So, if you need `lifecycle methods` you should probably use a class component.


### Why use functional components?

1. The React team mentioned that there may be a `performance boost` for functional component in future React versions.
- [stateless-functional-components](https://reactjs.org/blog/2015/10/07/react-v0.14.html#stateless-functional-components).

2. Easier to `read`, `test` and `debug`.

3. Code reusability : [building-reusable-components-using-react](https://buttercms.com/blog/building-reusable-components-using-react)

e.g: 

```
function handleClick(e) {
 // Some function which does fake API call
 fakeApiCall(e.target.value);
}

function Button(props) {
 return (
   <button className="button" onClick={props.handleClick}>
     {props.label}
   </button>
 );
}

function handleAPICall(e) {
 // Do some API call
}

function handleFormReset(e) {
 // Reset some form data
}

function App() {
 return (
   <div className="app">
     <Button handleClick={handleAPICall} label="Submit"/>
     <Button handleClick={handleFormReset} label="Reset"/>
   </div>
 );
}
```

