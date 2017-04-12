---
layout: post
title: React Counter Example
categories: [react]
---

This example can be run in [jscomplete.com/repl](https://jscomplete.com/repl), which is a zero-configuration playground for writing React.

```
class Button extends React.Component {
    handleClick = () => {
        this.props.increment(this.props.incrementValue);
    }

	render() {
        return (
            <button 
                onClick={this.handleClick}>
                +{this.props.incrementValue}
            </button>    
        )
    }
}

const Result = (props) => {
    return (
        <div>{props.counter}</div>
    )
}

class App extends React.Component {
	// initialize the state of the counter
	state = {
    	counter: 0
    }
    increment = (value) => {
        this.setState((prevState) => {
            return {counter: prevState.counter + value}
        });
    }
    render() {
        return (
            <div>
                <Button incrementValue={1} increment={this.increment} />
                <Button incrementValue={2} increment={this.increment} />
                <Button incrementValue={100} increment={this.increment} />
                <Button incrementValue={1000} increment={this.increment} />        
                <Result counter={this.state.counter} />
            </div>
        )
    }
}

// change the mountNode if you run this example in other environments
ReactDOM.render(<App />, mountNode);
```
A few things to note in this simple example:

1. setState() can [take a callback function](https://facebook.github.io/react/docs/react-component.html). This is useful when you need to update your state using the value of the current state.
```
this.setState((prevState) => {
    return {counter: prevState.counter + value}
});
```
2. Take note of the use of arrow function and class property to address the notorious `this` keyword issue. Say good bye to the days that we need to use bind() in the constructor function to make `this` behave properly.
```
increment = (value) => {
    this.setState((prevState) => {
        return {counter: prevState.counter + value}
    });
}
```
3. The increment property, which is a function, in the App component is a bit tricky. It is defined in the App component and passed down to Button component, from where it is then bound to an onClick event.