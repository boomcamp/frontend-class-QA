## What is Mounting?

is the process of outputting the `virtual` representation of a component(Other terms: [Virtual DOM](https://stackoverflow.com/questions/21965738/what-is-virtual-dom)) into the final UI representation


### Life cycles Classification

- initialization

- mounting

- updating, and

- unmounting


### Initialization

```
this.state = {
   list:[]
};
```


### Mounting = Created/inserted into DOM

1. componentWillMount() =  called just `before` a component mounts on the DOM or the render.

```
componentWillMount() {
    console.log('Waiting for component to mount then next is to call api')
}
```

2. componentDidMount()  =  called `after` the component gets mounted on the DOM. Called only `once`.(commonly used)

```
componentDidMount(){
	//Called the api once
	console.log('componentWillMount was executed then call getList() once')

	//The api function to called once!
	this.getList
}

getList=()=>{
    fetch('https://api.mydomain.com')
        .then(response => response.json())
        .then(data => this.setState({ list:data }));
}
```

### Updating = Re-render a component

1. shouldComponentUpdate() = determines whether the `component should be updated or not`, default returns `true`, you can `re-render`.

```
shouldComponentUpdate(nextProps, nextState){

	//if list[] is still, empty then re-render component
    return this.state.list !== nextState.list //returns true or false

    //So, i need to call
    //componentWillUpdate(nextProps,nextState)
    //ComponentDidUpdate(prevProps,prevState)
}
```

2. componentWillUpdate(nextProps,nextState) =  called once after the ‘shouldComponentUpdate’, can perform any logic before re-rendering

```
componentWillUpdate(nextProps, nextState) {
   console.log('I was called once by shouldComponentUpdate!');

   //So, i can perform any logic here before component re-renders :)
}
```

3. ComponentDidUpdate(prevProps,prevState) = called just `after the re-rendering of the component`. After the new (updated) component gets updated on the DOM.

```
componentDidUpdate(prevProps,prevState){
	console.log('I was called after the dom updated and component rendered');
}
```

### Unmounting = Remove into DOM

- componentWillUnmount() = The end of the component’s lifecycle.

```
componentWillUnmount(){
	//So this is the last part of lifecycles, you can add your logic here to destruct DOM.
}
```




### Resource

[Lifecycles](https://www.freecodecamp.org/news/how-to-understand-a-components-lifecycle-methods-in-reactjs-e1a609840630/)
