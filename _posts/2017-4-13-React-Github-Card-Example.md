---
layout: post
title: React Github Card Example
categories: [react]
---

This example can be run in [jscomplete.com/repl](https://jscomplete.com/repl), which is a zero-configuration playground for writing React.

```
const Card = (props) => {
  return (
    <div className="github-card clearfix">
      <img src={props.avatar_url} />
      <div className="github-profile">
        <div className="github-name"><a href={props.html_url} target="_blank">{props.name}</a></div>
        <div className="github-location">{props.location}</div>
      </div>
    </div>
  )
}

const CardList = (props) => {
  return (
    <div>
      {props.cards.map((card) => <Card key={card.id} {...card} />)}
    </div>
  )
}

class Form extends React.Component {
  state = { 
    userName: "stevemao"
  };
  handleSubmit = (event) => {
    // prevent the default form submit behavior
    event.preventDefault();
    // retrieve the Github user data
    axios.get(`https://api.github.com/users/${this.state.userName}`)
      .then(res => {
        this.props.addNewCard(res.data);
        this.setState({ userName: "" })
      })
  };
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input 
          value={this.state.userName}
          onChange={(event) => {this.setState({userName: event.target.value})}}
          type="text"
          placeholder="Github username"
          required />
        <button type="submit">Add card</button>
      </form>
    );
  }
}

class App extends React.Component {
  state = {
    cards: []
  };
  addNewCard = (cardInfo) => {
    this.setState((prevState) => {
      return {cards: prevState.cards.concat(cardInfo)}
    });
  };
  render() {
    return (
      <div>
        <Form addNewCard={this.addNewCard} />
        <CardList cards={this.state.cards} />
      </div>
    );
  }
}

ReactDOM.render(<App />, mountNode);
```
CSS styles for the example
```
.github-card {
	margin: 1em;
}

.clearfix:after {
  content: "";
  display: table;
  clear: both;
}

.github-card img {
	float: left;
	width: 75px;
  height: 75px;
}

.github-profile {
	margin-top: 10px;
  margin-left: 15px;
  float: left;
}

.github-name {
	font-size: 1.25em;
  font-weight: bold;
}
```
A few things to note in this simple example:

1. The addNewCard function is passed to Form component, where it is being invoked in a submit handler function. React only allows one-way data flow, which means we cannot change a parent or peer's component state. Therefore, we need to define state and function that alters state in the parent component, then pass them down to children components. Another thing to note is only state is changeable, props is immutable.

2. Spread `...` operator can sometimes save you a lot of key strokes.
```
const CardList = (props) => {
	return (
  	<div>
    	{props.cards.map((card) => <Card key={card.id} {...card} />)}
    </div>
  )
}
```