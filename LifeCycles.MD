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

1. componentWillMount() =  The first lifecycle to execute, called just `before` a component mounts on the DOM or the render.

```
componentWillMount() {
    console.log('Waiting for component to mount then componentDidMount is next to call.')
}
```

2. componentDidMount()  =  called `after` the component gets mounted on the DOM. Called only `once`.(commonly used)

```
componentDidMount(){
	console.log('componentWillMount was done, then i will call getList() once')

	//The api function to call once!
	this.getList
}

getList=()=>{
    fetch('https://api.mydomain.com')
        .then(response => response.json())
        .then(data => this.setState({ list:data }));
}
```

### Updating = Re-render a component

1. shouldComponentUpdate() = determines whether the `component should be updated/re-render or not`, returns `boolean` the default is `true`, you can `re-render` a component.

```
shouldComponentUpdate(nextProps, nextState){

    //if list[] is still, empty then re-render the component
    return this.state.list !== nextState.list //returns true or false

    //So, i need to call this two methods
    //componentWillUpdate(nextProps,nextState)
    //ComponentDidUpdate(prevProps,prevState)
}
```

2. componentWillUpdate(nextProps,nextState) =  called only `once` and `after the shouldComponentUpdate executed`, you can perform any logic before re-rendering.

```
componentWillUpdate(nextProps, nextState) {
   console.log('I was called once by shouldComponentUpdate!');

   //So, i can perform any logic here before component re-renders :)
}
```

3. ComponentDidUpdate(prevProps,prevState) = called just `after the re-rendering of the component`. After the new (updated) component gets updated on the DOM.

```
componentDidUpdate(prevProps,prevState){
	console.log('I was called after the DOM are updated and component rendered');
}
```

### Unmounting = Remove into DOM

- componentWillUnmount() = The end of the component’s lifecycle.

```
componentWillUnmount(){
	//So this is the last part of lifecycles, you can add your logic here to destruct DOM.
}
```



### Demo Snippet

```
import React, { Component, Fragment } from 'react';

class Language extends Component {

  state = {
    favorite: "Angular"
  };

  //componentWillMount, New implementation
  //constructor(){
  //  super();
  //  this.state = {
  //      favorite: "React",
  //      task : [{ componentWillMount : "Done"}]
  //  };
  //}

  //componentWillMount was renamed to => UNSAFE_componentWillMount(){}
  UNSAFE_componentWillMount() {
    console.log("1.) componentWillMount")
    this.setState({favorite: "PHP"})
  }
  
  componentDidMount() {
    console.log("2.) componentDidMount")
    this.setState({favorite: 'Java'})
  }

  /**
   * So i decide to reupdate the component if my favorite programming language is not equal to `Reactjs`
   */

  shouldComponentUpdate(nextProps, nextState){
    console.log("###### SHOULD COMPONENT UPDATE ? #######")
    console.log(this.state.favorite +" !== "+ nextState.favorite,  (this.state.favorite !== nextState.favorite))

    //if favorite !== Reactjs, then re-render Language!
    return this.state.favorite !== nextState.favorite || this.state.favorite === ''

    //So, i need to call this two methods to read other languages
    //componentWillUpdate(nextProps,nextState)
    //ComponentDidUpdate(prevProps,prevState)
  }

  //componentWillUpdate was renamed to => UNSAFE_componentWillUpdate(){}
  UNSAFE_componentWillUpdate(nextProps,nextState){
    console.log("1.) componentWillUpdate" )
    this.setState({favorite: 'C++'})
  }

  componentDidUpdate(prevProps,prevState){
    console.log("2.) componentDidUpdate")
    this.setState({favorite: 'Reactjs'})
  }

  componentWillUnmount(){
    console.log("Done!")
  }

  render() {
    console.log(this.state.favorite)

    return (<Fragment>Favorite : {this.state.favorite}</Fragment>);
  }
}

export default Language;
```

Output :

```
1.) componentWillMount
PHP
2.) componentDidMount

###### SHOULD COMPONENT UPDATE ? #######
PHP !== Java true
1.) componentWillUpdate
Java
2.) componentDidUpdate


###### SHOULD COMPONENT UPDATE ? #######
Java !== Reactjs true
1.) componentWillUpdate
Reactjs
2.) componentDidUpdate


###### SHOULD COMPONENT UPDATE ? #######
Reactjs !== Reactjs false
```


```
Favorite : Reactjs
```





