1. Create simple app
		
	npx create-react-app my-app
	cd my-app
	npm start

2. Add a functional component.

	import React from 'react';
	import ReactDOM from 'react-dom';
	import App from "./components/App";
	ReactDOM.render(
	  <App />,
	  document.getElementById('root')
	);


	import React from "react";
	import List from "./List";
	function App() {
	  return (
	    <div>
	      <List />
	    <div> // <- should be </div>
	  )
	}
	export default App;

3. i 4. Extract the component out to a separate file and nesting components.
		
	import React from "react";
	import List from "./List";
	function App() {
  		return (
    	<div>
      		<List />
    	<div> // <- </div>
		);
	}
	export default App;


	import React from "react"
	function List() {
	let siema = "Siema";
	return (
	  <div className="list"> 
	    <input type="checkbox" />
	    <p>{siema}<p> // error
	  <div> // error
	)
	export default List

5. Styling your components
	return (
    <div className="list"> 
      <input type="checkbox" />

6. JSX vs JavaScript
	let siema = "siema"; 
	<p>{siema}<p>

7. Writing inline styles
	<div style={{color: "yellow", fontSize: 16 }} className="list">

	const styles = {
    color: "yellow",
    fontSize: "16px"
	}
	<div style={styles} className="list">

8. props
	<div className="contacts">
      <ContactCard 
      name="Mr. Whiskerson" 
      imgUrl="http://placekitten.com/300/200" 
      phone="(212) 555-1234" 
      email="mr.whiskaz@catnap.meow"
    />

    <ContactCard 
    	contact={{name: "Mr. Whiskerson", imgUrl: "http://placekitten.com/300/200", phone: "(212) 555-1234", email: "mr.whiskaz@catnap.meow"}}
    >

	function ContactCard(props) {
  		return (
	    	<div className="contact-card">
	    		<img src={props.imgUrl}/>
	      		<h3>{props.name}<h3>
	      		<p>Phone: {props.phone}<p>
	      		<p>Email: {props.email}<p>
	    	<div>
  		)
	}


9. Lists - stored in .js file, every element should have id attribute to then pass it to Key in component
	const jokesData = [
	    {
	        id: 1,
	        punchLine: "It’s hard to explain puns to kleptomaniacs because they always take things literally."
	    },
	    {
	        id: 2,
	        question: "What's the best thing about Switzerland?",
	        punchLine: "I don't know, but the flag is a big plus!"
	    }
    ]
    export default products

    to use:
    import jokesData from "./jokesData"

	function App() {
    		const jokeComponents = jokesData.map(joke => <Joke key={joke.id} question={joke.question} punchLine={joke.punchLine} />)

    		return (
        		<div className="todo-list">
            		{todoItems}
        		</div>
    		)

10. + 11. Class components + State management

	class App extends React.Component {
    constructor() {
        super();
        this.state = {
            isLoggedIn: true
        }
    }
    
    render() {
        return (
            <div>
                <h1>You are currently logged {this.state.isLoggedIn ? "in" : "out"}</h1>
            </div>
        )
    }
}
export default App

12. Events
		- list of all available events - https://reactjs.org/docs/events.html#supported-events

		<div>
            <img src="https://www.fillmurray.com/200/100"/>
            <br />
            <br />
            <button onClick={handleClick}>Click me</button>
        </div>

13. Changing state
	class App extends React.Component {
    	constructor() {
        	super()
        	this.state = {
            	count: 0
        	}
       		this.handleClick = this.handleClick.bind(this)
    	}
    
    	handleClick() {
        	this.setState(prevState => {
           		return {
               		count: prevState.count + 1
            	}
        	})
    	}
    
    	render() {
        	return (
            	<div>
                	<h1>{this.state.count}</h1>
                	<button onClick={this.handleClick}>Change!</button>
                	<ChildComponent count={this.state.count}/> <--- every time value of state changes react will rerender the component
            	</div>
        	)
    	}
	}

	**Changing state of one element in an array** 
	handleChange(id) {
        this.setState(prevState => {
            const updatedTodos = prevState.todos.map(todo => {
                if (todo.id === id) {
                    return {
                        ...todo, <-- return all fields
                        completed: !todo.completed <-- we change one
                    }
                }
                return todo
            })
            console.log(prevState.todos)
            console.log(updatedTodos)
            return {
                todos: updatedTodos
            }
        })
    }

14. Component lifecycle
	// https://engineering.musefind.com/react-lifecycle-methods-how-and-when-to-use-them-2111a1b692b1
	// https://reactjs.org/blog/2018/03/29/react-v-16-3.html#component-lifecycle-changes