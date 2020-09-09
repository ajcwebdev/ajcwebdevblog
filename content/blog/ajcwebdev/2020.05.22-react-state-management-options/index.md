---
title: react state management - options
date: "2020-05-22"
description: a comparison of various state management solutions in the React ecosystem
---

# React Core Library

## [Class Component State](https://reactjs.org/docs/state-and-lifecycle.html) (2013)

Despite the large variety of 3rd party state management solutions, the React Core library has state management already built in. Before hooks, which we'll discuss later in this post, only class components were able to store state. 

```javascript
const todoData = [
  {
    task: "Organize Garage",
    id: 1528817077286,
    completed: false
  },
  {
    task: "Bake Cookies",
    id: 1528817084358,
    completed: false
  }
];

class App extends React.Component {
  constructor() {
    super();
    this.state = {
      todo: todoData
    };
  }
```

## [useState hook](https://reactjs.org/docs/hooks-state.html) (2018)

## [Context API](https://reactjs.org/docs/context.html) (2018)

### React.createContext

```javascript
const MyContext = React.createContext(defaultValue);
```

### Context.Provider

```javascript
<MyContext.Provider value={/* some value */}>
```

# Third Party Libraries

## [Redux](https://redux.js.org/) (2015)

## [MobX](https://mobx.js.org/README.html) (2015)

## [Kea](https://kea.js.org/)
First Commit: March 29, 2016
862 Commits
1,599 Stars

John Au-Yeung - [Simplify React state management with Kea (March 10, 2020)](https://blog.logrocket.com/simplify-react-state-management-with-kea/)

## [Overmind](https://overmindjs.org/)
First Commit: June 18, 2018
1,398 Commits
938 Stars

Nathan Sebhastian - [Easier React State Management with OvermindJS (May 19, 2020)](https://blog.bitsrc.io/making-state-management-easier-with-overmindjs-5fcdd87e8c8e)

## [Easy Peasy](https://easy-peasy.now.sh/) (2018)
First Commit: October 21, 2018
627 Commits
3,445 Stars

Easy Peasy aims to be an intuitive and simple state management library with zero configuration. It includes a store and actions like Redux but no reducers.

### 1 - Create your store

```javascript
const store = createStore({
  todos: {
    items: ['Create store', 'Wrap application', 'Use store'],
    add: action((state, payload) => {
      state.items.push(payload)
    })
  }
});
```

### 2 - Wrap your application

```javascript
function App() {
  return (
    <StoreProvider store={store}>
      <TodoList />
    </StoreProvider>
  );
}
```

### 3 - Use the store

```javascript
function TodoList() {
  const todos = useStoreState(state => state.todos.items)
  const add = useStoreActions(actions => actions.todos.add)
  return (
    <div>
      {todos.map((todo, idx) => <div key={idx}>{todo}</div>)}
      <AddTodo onAdd={add} />
    </div>
  )
}
```

## [Recoil](https://recoiljs.org/) (2020)
First Commit: May 5, 2020
80 Commits
[4,861 Stars](https://github.com/facebookexperimental/Recoil/stargazers)

Recoil is the newest attempt at state management in React. It introduces brand new abstractions including atoms (shared state) and selectors (pure functions).

### Atoms

Atoms are units of state that can be update and subscribed to.

```javascript
const fontSizeState = atom({
  key: 'fontSizeState',
  default: 14,
});
```

```javascript
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return (
    <button onClick={() => setFontSize((size) => size + 1)} style={{fontSize}}>
      Click to Enlarge
    </button>
  );
}
```

### Selectors

Selectors are pure functions that take atoms or other selectors as input.

```javascript
const fontSizeLabelState = selector({
  key: 'fontSizeLabelState',
  get: ({get}) => {
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}`;
  },
});
```

```javascript
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  const fontSizeLabel = useRecoilValue(fontSizeLabelState);

  return (
    <>
      <div>Current font size: ${fontSizeLabel}</div>

      <button onClick={() => setFontSize(fontSize + 1)} style={{fontSize}}>
        Click to Enlarge
      </button>
    </>
  );
}
```

## Further Reading

Daniel Schulz - [Comparison of State Management Solutions for React (September 18, 2018)](https://medium.com/dailyjs/comparison-of-state-management-solutions-for-react-2161a0b4af7b)

Kent C. Dodds - [Application State Management with React (April 22, 2019)](https://kentcdodds.com/blog/application-state-management-with-react)

Robin Wieruch - [React State Management (October 14, 2019)](https://www.robinwieruch.de/react-state)

Adam Nathaniel Davis - [Throw Out Your React State-Management Tools (March 3, 2020)](https://dev.to/bytebodger/throw-out-your-react-state-management-tools-4cj0)

Dmitri Pavlutin - [3 Rules of React State Management (March 4, 2020)](https://dmitripavlutin.com/react-state-management/)

Mateusz Piguła, Adrian Senecki - [React State Management: React Hooks vs Redux (April 2, 2020)](https://tsh.io/blog/react-state-management-react-hooks-vs-redux/)