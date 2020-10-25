---
title: react state management - class components
date: "2020-06-02"
description: class components
---

Despite the large variety of 3rd party state management solutions, the React Core library has state management already built in. Before hooks, which we’ll discuss in part 2, only class components were able to store state.

In this series of posts we’ll look at different ways to manage state in a todo list app.

*Note: There’s are many ways to make a todo app. This is not meant to be the ultimate example, but simply an exercise to demonstrate different approaches to storing state in a React app.*

For this and any other example React apps on this newsletter I recommend using create-react-app to get a boilerplate project set up. The full example app can be found [on my Github](https://github.com/ajcwebdev/react-state-management/tree/master/class-components).

Our app will contain:

### Three components:
* TodoItem
* TodoList
* TodoForm

### Three helper functions:
* addTodo
* toggleComplete
* clearComplete

### Two event handlers:
* inputChange
* submitForm

First let’s declare a variable with a JSON like syntax containing an array of objects. This will give us a couple tasks rendered when we open the app. Each object is a todo task with 3 properties: task, id, and a boolean value for toggling the todo complete.

```javascript
const initialState = [
  {
    task: "Organize Garage",
    id: 1528817077286,
    complete: false
  },
  {
    task: "Bake Cookies",
    id: 1528817084358,
    complete: false
  }
];
```

Our App component takes in this.state with the initialState array set to the variable todo.

```javascript
class App extends React.Component {
  constructor() {
    super();
    this.state = {
      todo: initialState
    };
  } 
```

## Helper Functions

### addTodo

addTodo takes in a parameter for a task and sets each property accordingly. this.setState sets the todo state to a new array with newTask added to the end. Date.now() generates a new id for every task.

```javascript
addTodo = task => {
  const newTask = {
    task: task,
    id: Date.now(),
    complete: false
  }
  this.setState(
    {todo:
      [...this.state.todo, newTask]
    }
  )
}
```

### toggleComplete

toggleComplete takes in an event target and grabs a todo’s id. The spread operator gives us the list of todos in an array and sets it to newTodo. The splice method is then used for toggling completed todos by grabbing the todo that is clicked on and giving it a CSS class called complete. We will see the necessary CSS at the very end of this tutorial.

```javascript
toggleComplete = e => {
    const id = e.target.id
    const newTodo = [...this.state.todo]
    newTodo.splice(id, 1, {
      ...this.state.todo[id],
      complete: !this.state.todo[id].complete
    })
    this.setState({todo: newTodo})
  }
```

### clearComplete

clearComplete uses the filter method to remove completed todos by looping over all todos and returning an array of todos that have the complete property set to false.

```javascript
clearComplete = e => {
  this.setState(
    {todo:
      [...this.state.todo.filter(
        todo => todo.complete === false)
      ]
    }
  )
}
```

The render method contains two components, one for our list of todo items (TodoList) and another with a form that accepts input to add a task and a button to clear completed todos (TodoForm).

```javascript
render() {
    return (
      <div className="container">

        <h2>React Todo</h2>

        <TodoList
          todo={this.state.todo}
          toggleComplete={this.toggleComplete}
        />

        <TodoForm
          addTodo={this.addTodo}
          clearComplete={this.clearComplete}
        />

      </div>
    )
  }
}
```

## Components

### TodoItem

Our TodoItem component returns an html list item with the tasks id. The className checks the complete property, if the complete property is true then the className will be set to complete. If false it will set the className to null.

```javascript
class TodoItem extends React.Component {
  render() {
    return (
      <li
        id={this.props.id}
        className={this.props.todo.complete ? "complete" : null}
        onClick={this.props.toggleComplete}
      >
        {this.props.todo.task}
      </li>
    )
  }
}
```

### TodoList

The TodoList component uses the map array method to render all the todos inside an unordered list tag.

```javascript
class TodoList extends React.Component {
  render() {
    return (
      <ul>
        {this.props.todo.map((todo, id) => (
          <TodoItem
            key={todo.id}
            id={id}
            todo={todo}
            toggleComplete={this.props.toggleComplete}
          />
        ))}
      </ul>
    )
  }
}
```

### TodoForm

The TodoForm component has an input value so the user can input new todo tasks. inputChange and submitForm use the event object to grab the information entered into the form and set it to TodoForm’s state.

```javascript
class TodoForm extends React.Component {
  constructor() {
    super()
    this.state = {
      input: ""
    }
  }

  inputChange = e => {
    this.setState({
      input: e.target.value
    })
  }

  submitForm = e => {
    e.preventDefault()
    this.props.addTodo(
      this.state.input
    )
    this.setState({
      input: ""
    })
  }
```

### Event Handlers

The form uses React’s [event handlers](https://reactjs.org/docs/handling-events.html) including onSubmit, onChange, and onClick. These are similar to the native HTML event handlers with the exception of writing camelCase instead of all lowercase.

```javascript
render() {
    return (
      <form onSubmit={this.submitForm}>
        <input
          type="text"
          onChange={this.inputChange}
          value={this.state.input}
        />
        <button>Add Todo</button>
        <button
          type="button"
          onClick={this.props.clearComplete}
        >
          Clear Complete
        </button>
      </form>
    )
  }
}
```

The last thing we need to make our todo list functional is a complete class in our index.css file. This will draw a line through our todos when we click them to toggle them complete.

```javascript
.complete {
  text-decoration: line-through;
}
```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/z4qhaqogigdi3ihi4zk4.jpg)