**what is the difference between constructor and super with props as its parameter and constructor and props without props parameter, normally it happens in a child component**

```
//props = are read only
//constructor = automatically called during the creation of an object
//super() = Superclass
//You can’t access this.props inside a constructor without calling super(props)
constructor(){ //So if you did not assign the props during load time
  super()
  console.log(this.props); //It will gives you undefined property inside constructor, so you cannot set a state safely in the constructor
   this.state = {
  };
}
//The safe way to read a property is to assign both and call properties using super() method
constructor(props) {
 console.log(this.props) => //undefined
 super(props);
 console.log(this.props); //Defined
}
```