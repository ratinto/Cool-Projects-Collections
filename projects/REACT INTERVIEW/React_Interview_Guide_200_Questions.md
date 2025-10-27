# React Interview Preparation Guide - 200 Questions & Answers

## Table of Contents
1. [React Fundamentals (50 Questions)](#react-fundamentals)
2. [React Hooks (40 Questions)](#react-hooks)
3. [State Management (30 Questions)](#state-management)
4. [Performance Optimization (25 Questions)](#performance-optimization)
5. [Advanced Topics (30 Questions)](#advanced-topics)
6. [Forms & Validation (15 Questions)](#forms--validation)
7. [Data Fetching & API (10 Questions)](#data-fetching--api)

---

## React Fundamentals

### 1. What is React and why is it popular?

**Answer:** React is a JavaScript library for building user interfaces, particularly web applications. It was created by Facebook and is now maintained by Meta and the community.

**Why React is popular:**
- **Component-based architecture**: Reusable UI components
- **Virtual DOM**: Efficient updates and rendering
- **Unidirectional data flow**: Predictable state management
- **Rich ecosystem**: Large community and extensive tooling
- **Declarative**: Describe what the UI should look like, not how to achieve it

```jsx
// Example of a simple React component
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Usage
<Welcome name="World" />
```

### 2. What is JSX and how does it work?

**Answer:** JSX (JavaScript XML) is a syntax extension for JavaScript that allows you to write HTML-like code in JavaScript files. It's not required to use React, but it makes the code more readable and easier to write.

**Key points:**
- JSX gets transpiled to `React.createElement()` calls
- Must return a single parent element (or use React.Fragment)
- Use camelCase for HTML attributes (`className` instead of `class`)
- JavaScript expressions are wrapped in curly braces `{}`

```jsx
// JSX syntax
const element = (
  <div className="container">
    <h1>Hello World</h1>
    <p>Current time: {new Date().toLocaleTimeString()}</p>
  </div>
);

// Transpiles to:
const element = React.createElement(
  'div',
  { className: 'container' },
  React.createElement('h1', null, 'Hello World'),
  React.createElement('p', null, 'Current time: ', new Date().toLocaleTimeString())
);
```

### 3. What are React components and their types?

**Answer:** React components are independent, reusable pieces of UI that return JSX. There are two main types:

**1. Function Components (Modern approach):**
```jsx
function MyComponent({ title, count }) {
  return (
    <div>
      <h2>{title}</h2>
      <p>Count: {count}</p>
    </div>
  );
}
```

**2. Class Components (Legacy):**
```jsx
class MyComponent extends React.Component {
  render() {
    return (
      <div>
        <h2>{this.props.title}</h2>
        <p>Count: {this.props.count}</p>
      </div>
    );
  }
}
```

**Key differences:**
- Function components are simpler and more performant
- Class components have lifecycle methods
- Function components use hooks for state and side effects
- Function components are the recommended approach

### 4. What are props in React?

**Answer:** Props (properties) are read-only data passed from parent to child components. They allow components to be reusable and configurable.

**Key characteristics:**
- Props are immutable (cannot be changed by child component)
- Props flow down the component tree
- Props can be any JavaScript value (strings, numbers, objects, functions)
- Use destructuring for cleaner code

```jsx
// Parent component
function App() {
  const user = { name: 'John', age: 30 };
  const handleClick = () => console.log('Button clicked');
  
  return (
    <UserCard 
      user={user} 
      isActive={true} 
      onButtonClick={handleClick}
      className="user-card"
    />
  );
}

// Child component
function UserCard({ user, isActive, onButtonClick, className }) {
  return (
    <div className={className}>
      <h3>{user.name}</h3>
      <p>Age: {user.age}</p>
      <p>Status: {isActive ? 'Active' : 'Inactive'}</p>
      <button onClick={onButtonClick}>Click me</button>
    </div>
  );
}
```

### 5. What is the difference between state and props?

**Answer:** State and props are both ways to store data in React, but they serve different purposes:

| Aspect | State | Props |
|--------|-------|-------|
| **Mutability** | Mutable (can be changed) | Immutable (read-only) |
| **Ownership** | Owned by component | Passed from parent |
| **Updates** | Can be updated with setState/useState | Cannot be updated by child |
| **Purpose** | Internal component data | External configuration |

```jsx
function Counter({ initialValue = 0 }) {
  // State: internal data that can change
  const [count, setCount] = useState(initialValue);
  
  // Props: external data passed from parent
  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  
  return (
    <div>
      <h3>Count: {count}</h3>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
}

// Usage
<Counter initialValue={5} />
```

### 6. What is the Virtual DOM and how does it work?

**Answer:** The Virtual DOM is a JavaScript representation of the real DOM. React uses it to optimize rendering performance.

**How it works:**
1. **Initial render**: Creates Virtual DOM tree
2. **State change**: Creates new Virtual DOM tree
3. **Diffing**: Compares old and new Virtual DOM trees
4. **Reconciliation**: Updates only the changed parts in real DOM

```jsx
// Example showing Virtual DOM benefits
function TodoList({ todos }) {
  const [filter, setFilter] = useState('all');
  
  const filteredTodos = todos.filter(todo => {
    if (filter === 'completed') return todo.completed;
    if (filter === 'active') return !todo.completed;
    return true;
  });
  
  return (
    <div>
      <div>
        <button onClick={() => setFilter('all')}>All</button>
        <button onClick={() => setFilter('active')}>Active</button>
        <button onClick={() => setFilter('completed')}>Completed</button>
      </div>
      <ul>
        {filteredTodos.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    </div>
  );
}
```

**Benefits:**
- Faster updates (batched DOM operations)
- Efficient diffing algorithm
- Predictable rendering
- Better performance for large applications

### 7. What is the component lifecycle in React?

**Answer:** Component lifecycle refers to the different phases a component goes through from creation to destruction. With hooks, we use `useEffect` to handle lifecycle events.

**Lifecycle phases:**
1. **Mounting**: Component is created and inserted into DOM
2. **Updating**: Component re-renders due to state/props changes
3. **Unmounting**: Component is removed from DOM

```jsx
function LifecycleExample({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  // ComponentDidMount equivalent
  useEffect(() => {
    console.log('Component mounted');
    fetchUser(userId);
    
    // ComponentWillUnmount equivalent
    return () => {
      console.log('Component will unmount');
    };
  }, []); // Empty dependency array = run once on mount
  
  // ComponentDidUpdate equivalent
  useEffect(() => {
    if (userId) {
      fetchUser(userId);
    }
  }, [userId]); // Run when userId changes
  
  const fetchUser = async (id) => {
    setLoading(true);
    try {
      const response = await fetch(`/api/users/${id}`);
      const userData = await response.json();
      setUser(userData);
    } catch (error) {
      console.error('Error fetching user:', error);
    } finally {
      setLoading(false);
    }
  };
  
  if (loading) return <div>Loading...</div>;
  
  return (
    <div>
      <h2>User Profile</h2>
      {user && (
        <div>
          <p>Name: {user.name}</p>
          <p>Email: {user.email}</p>
        </div>
      )}
    </div>
  );
}
```

### 8. What are controlled and uncontrolled components?

**Answer:** The difference lies in how form data is managed:

**Controlled Components:**
- Form data is controlled by React state
- Input value is set by React state
- Changes are handled by event handlers
- Single source of truth

```jsx
function ControlledForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form data:', formData);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="name"
        value={formData.name}
        onChange={handleChange}
        placeholder="Name"
      />
      <input
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <textarea
        name="message"
        value={formData.message}
        onChange={handleChange}
        placeholder="Message"
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Uncontrolled Components:**
- Form data is handled by the DOM itself
- Use refs to access form values
- Less React code, more traditional HTML

```jsx
function UncontrolledForm() {
  const nameRef = useRef();
  const emailRef = useRef();
  const messageRef = useRef();
  
  const handleSubmit = (e) => {
    e.preventDefault();
    const formData = {
      name: nameRef.current.value,
      email: emailRef.current.value,
      message: messageRef.current.value
    };
    console.log('Form data:', formData);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        ref={nameRef}
        type="text"
        placeholder="Name"
      />
      <input
        ref={emailRef}
        type="email"
        placeholder="Email"
      />
      <textarea
        ref={messageRef}
        placeholder="Message"
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 9. What is the key prop and why is it important?

**Answer:** The `key` prop is a special attribute used by React to identify which items have changed, been added, or removed in lists. It helps React efficiently update the DOM.

**Why keys are important:**
- **Performance**: Helps React identify which items to update
- **State preservation**: Maintains component state across re-renders
- **Avoiding bugs**: Prevents issues with form inputs and component state

```jsx
// ❌ Bad: Using array index as key
function BadTodoList({ todos }) {
  return (
    <ul>
      {todos.map((todo, index) => (
        <li key={index}>{todo.text}</li>
      ))}
    </ul>
  );
}

// ✅ Good: Using unique, stable identifier
function GoodTodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}

// ✅ Good: Using stable, unique key for dynamic lists
function DynamicList({ items }) {
  return (
    <ul>
      {items.map(item => (
        <li key={`${item.type}-${item.id}`}>
          {item.name}
        </li>
      ))}
    </ul>
  );
}
```

**Key requirements:**
- Must be unique among siblings
- Should be stable (don't change between renders)
- Should be predictable (same key for same item)
- Don't use array index for dynamic lists

### 10. What is React.Fragment and when to use it?

**Answer:** React.Fragment is a component that lets you group multiple elements without adding extra nodes to the DOM. It's useful when you need to return multiple elements but don't want a wrapper div.

```jsx
// ❌ Without Fragment - adds extra div
function WithoutFragment() {
  return (
    <div>
      <h1>Title</h1>
      <p>Description</p>
    </div>
  );
}

// ✅ With Fragment - no extra DOM node
function WithFragment() {
  return (
    <React.Fragment>
      <h1>Title</h1>
      <p>Description</p>
    </React.Fragment>
  );
}

// ✅ Short syntax - most common
function WithShortSyntax() {
  return (
    <>
      <h1>Title</h1>
      <p>Description</p>
    </>
  );
}

// ✅ With keys (only React.Fragment supports keys)
function FragmentWithKeys({ items }) {
  return (
    <React.Fragment>
      {items.map(item => (
        <React.Fragment key={item.id}>
          <h3>{item.title}</h3>
          <p>{item.description}</p>
        </React.Fragment>
      ))}
    </React.Fragment>
  );
}
```

**When to use Fragments:**
- Returning multiple elements from a component
- Avoiding unnecessary wrapper divs
- Maintaining semantic HTML structure
- When you need keys for grouped elements

---

## React Hooks

### 11. What are React Hooks and why were they introduced?

**Answer:** React Hooks are functions that let you use state and other React features in function components. They were introduced in React 16.8 to solve several problems with class components.

**Problems Hooks solve:**
- **Reusing stateful logic**: Hard to share logic between components
- **Complex components**: Class components become hard to understand
- **Confusing classes**: `this` binding and lifecycle methods are confusing
- **Wrapper hell**: Higher-order components create deeply nested trees

```jsx
// Before Hooks - Class component
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.increment = this.increment.bind(this);
  }
  
  increment() {
    this.setState({ count: this.state.count + 1 });
  }
  
  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

// After Hooks - Function component
function Counter() {
  const [count, setCount] = useState(0);
  
  const increment = () => setCount(count + 1);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

### 12. What is useState and how does it work?

**Answer:** `useState` is a Hook that lets you add state to function components. It returns an array with two elements: the current state value and a function to update it.

**Syntax:**
```jsx
const [state, setState] = useState(initialValue);
```

**Key points:**
- State updates are asynchronous
- State updates trigger re-renders
- State updates are batched for performance
- Use functional updates for state that depends on previous state

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  const [user, setUser] = useState({ name: '', email: '' });
  
  // Simple state update
  const increment = () => setCount(count + 1);
  
  // Functional update (recommended when state depends on previous state)
  const incrementBy = (amount) => setCount(prev => prev + amount);
  
  // Object state update
  const updateUser = (field, value) => {
    setUser(prev => ({
      ...prev,
      [field]: value
    }));
  };
  
  // Multiple state updates (batched)
  const reset = () => {
    setCount(0);
    setName('');
    setUser({ name: '', email: '' });
  };
  
  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={increment}>+1</button>
      <button onClick={() => incrementBy(5)}>+5</button>
      
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />
      
      <input
        value={user.name}
        onChange={(e) => updateUser('name', e.target.value)}
        placeholder="User Name"
      />
      
      <button onClick={reset}>Reset All</button>
    </div>
  );
}
```

### 13. What is useEffect and how does it work?

**Answer:** `useEffect` is a Hook that lets you perform side effects in function components. It combines the functionality of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

**Syntax:**
```jsx
useEffect(() => {
  // Side effect code
  return () => {
    // Cleanup code (optional)
  };
}, [dependencies]);
```

**Common use cases:**
- Data fetching
- Setting up subscriptions
- Manually changing the DOM
- Timers and intervals

```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  // Effect with no dependencies - runs on every render
  useEffect(() => {
    console.log('Component rendered');
  });
  
  // Effect with empty dependencies - runs once on mount
  useEffect(() => {
    console.log('Component mounted');
    
    // Cleanup function
    return () => {
      console.log('Component will unmount');
    };
  }, []);
  
  // Effect with dependencies - runs when userId changes
  useEffect(() => {
    const fetchUser = async () => {
      setLoading(true);
      setError(null);
      
      try {
        const response = await fetch(`/api/users/${userId}`);
        if (!response.ok) throw new Error('Failed to fetch user');
        const userData = await response.json();
        setUser(userData);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    
    if (userId) {
      fetchUser();
    }
  }, [userId]); // Dependency array
  
  // Effect with cleanup - setting up and cleaning up subscriptions
  useEffect(() => {
    const interval = setInterval(() => {
      console.log('Timer tick');
    }, 1000);
    
    // Cleanup function
    return () => {
      clearInterval(interval);
    };
  }, []);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!user) return <div>No user found</div>;
  
  return (
    <div>
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
    </div>
  );
}
```

### 14. What is useContext and how does it work?

**Answer:** `useContext` is a Hook that lets you consume context values in function components. It's used to avoid prop drilling and share data across the component tree.

**Creating and using context:**
```jsx
// 1. Create context
const ThemeContext = createContext();

// 2. Create provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  const toggleTheme = () => {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  };
  
  const value = {
    theme,
    toggleTheme,
    isDark: theme === 'dark'
  };
  
  return (
    <ThemeContext.Provider value={value}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Create custom hook for easier usage
function useTheme() {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within ThemeProvider');
  }
  return context;
}

// 4. Use context in components
function Header() {
  const { theme, toggleTheme } = useTheme();
  
  return (
    <header style={{ 
      backgroundColor: theme === 'light' ? '#fff' : '#333',
      color: theme === 'light' ? '#333' : '#fff'
    }}>
      <h1>My App</h1>
      <button onClick={toggleTheme}>
        Switch to {theme === 'light' ? 'dark' : 'light'} theme
      </button>
    </header>
  );
}

function Content() {
  const { theme, isDark } = useTheme();
  
  return (
    <main style={{ 
      backgroundColor: theme === 'light' ? '#f5f5f5' : '#222',
      color: theme === 'light' ? '#333' : '#fff'
    }}>
      <p>Current theme: {theme}</p>
      <p>Is dark mode: {isDark ? 'Yes' : 'No'}</p>
    </main>
  );
}

// 5. App component with provider
function App() {
  return (
    <ThemeProvider>
      <Header />
      <Content />
    </ThemeProvider>
  );
}
```

### 15. What is useReducer and when to use it?

**Answer:** `useReducer` is a Hook that's an alternative to `useState` for managing complex state logic. It's similar to Redux's reducer pattern and is useful when state logic is complex or when the next state depends on the previous one.

**Syntax:**
```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

**When to use useReducer:**
- Complex state logic with multiple sub-values
- State updates depend on previous state
- Need to avoid deep prop drilling
- Want to centralize state logic

```jsx
// Reducer function
function todoReducer(state, action) {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        ...state,
        todos: [...state.todos, {
          id: Date.now(),
          text: action.payload,
          completed: false
        }]
      };
    
    case 'TOGGLE_TODO':
      return {
        ...state,
        todos: state.todos.map(todo =>
          todo.id === action.payload
            ? { ...todo, completed: !todo.completed }
            : todo
        )
      };
    
    case 'DELETE_TODO':
      return {
        ...state,
        todos: state.todos.filter(todo => todo.id !== action.payload)
      };
    
    case 'SET_FILTER':
      return {
        ...state,
        filter: action.payload
      };
    
    case 'CLEAR_COMPLETED':
      return {
        ...state,
        todos: state.todos.filter(todo => !todo.completed)
      };
    
    default:
      return state;
  }
}

// Component using useReducer
function TodoApp() {
  const initialState = {
    todos: [],
    filter: 'all' // 'all', 'active', 'completed'
  };
  
  const [state, dispatch] = useReducer(todoReducer, initialState);
  
  const addTodo = (text) => {
    dispatch({ type: 'ADD_TODO', payload: text });
  };
  
  const toggleTodo = (id) => {
    dispatch({ type: 'TOGGLE_TODO', payload: id });
  };
  
  const deleteTodo = (id) => {
    dispatch({ type: 'DELETE_TODO', payload: id });
  };
  
  const setFilter = (filter) => {
    dispatch({ type: 'SET_FILTER', payload: filter });
  };
  
  const clearCompleted = () => {
    dispatch({ type: 'CLEAR_COMPLETED' });
  };
  
  const filteredTodos = state.todos.filter(todo => {
    if (state.filter === 'active') return !todo.completed;
    if (state.filter === 'completed') return todo.completed;
    return true;
  });
  
  return (
    <div>
      <h1>Todo App</h1>
      
      <TodoInput onAdd={addTodo} />
      
      <div>
        <button onClick={() => setFilter('all')}>All</button>
        <button onClick={() => setFilter('active')}>Active</button>
        <button onClick={() => setFilter('completed')}>Completed</button>
        <button onClick={clearCompleted}>Clear Completed</button>
      </div>
      
      <ul>
        {filteredTodos.map(todo => (
          <li key={todo.id}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => toggleTodo(todo.id)}
            />
            <span style={{ 
              textDecoration: todo.completed ? 'line-through' : 'none' 
            }}>
              {todo.text}
            </span>
            <button onClick={() => deleteTodo(todo.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

function TodoInput({ onAdd }) {
  const [text, setText] = useState('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    if (text.trim()) {
      onAdd(text.trim());
      setText('');
    }
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        value={text}
        onChange={(e) => setText(e.target.value)}
        placeholder="Add a todo..."
      />
      <button type="submit">Add</button>
    </form>
  );
}
```

### 16. What is useMemo and when to use it?

**Answer:** `useMemo` is a Hook that memoizes the result of a computation and only recalculates it when its dependencies change. It's used for performance optimization.

```jsx
function ExpensiveComponent({ items, filter }) {
  // Expensive calculation that only runs when items or filter change
  const filteredItems = useMemo(() => {
    console.log('Filtering items...');
    return items.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
  }, [items, filter]);
  
  return (
    <ul>
      {filteredItems.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

### 17. What is useCallback and when to use it?

**Answer:** `useCallback` returns a memoized version of a callback function that only changes if one of its dependencies has changed. It's useful for preventing unnecessary re-renders of child components.

```jsx
function ParentComponent() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  // Memoized callback - only recreates when count changes
  const handleClick = useCallback(() => {
    console.log('Button clicked, count:', count);
  }, [count]);
  
  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
        placeholder="Name"
      />
      <button onClick={() => setCount(count + 1)}>Count: {count}</button>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

const ChildComponent = React.memo(({ onClick }) => {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
});
```

### 18. What is useRef and how is it different from useState?

**Answer:** `useRef` returns a mutable ref object that persists for the full lifetime of the component. Unlike state, changing a ref doesn't trigger a re-render.

```jsx
function RefExample() {
  const [count, setCount] = useState(0);
  const countRef = useRef(0);
  const inputRef = useRef(null);
  const previousCountRef = useRef();
  
  // Update ref without causing re-render
  const incrementRef = () => {
    countRef.current += 1;
    console.log('Ref count:', countRef.current);
  };
  
  // Update state (causes re-render)
  const incrementState = () => {
    setCount(count + 1);
  };
  
  // Store previous value
  useEffect(() => {
    previousCountRef.current = count;
  });
  
  // Focus input
  const focusInput = () => {
    inputRef.current.focus();
  };
  
  return (
    <div>
      <p>State count: {count}</p>
      <p>Previous count: {previousCountRef.current}</p>
      <p>Ref count: {countRef.current}</p>
      
      <button onClick={incrementState}>Increment State</button>
      <button onClick={incrementRef}>Increment Ref</button>
      
      <input ref={inputRef} placeholder="Focus me" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### 19. What are custom hooks and how to create them?

**Answer:** Custom hooks are JavaScript functions that start with "use" and can call other hooks. They allow you to extract component logic into reusable functions.

```jsx
// Custom hook for API data fetching
function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        const response = await fetch(url);
        if (!response.ok) throw new Error('Failed to fetch');
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    
    fetchData();
  }, [url]);
  
  return { data, loading, error };
}

// Custom hook for local storage
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });
  
  const setValue = (value) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error(error);
    }
  };
  
  return [storedValue, setValue];
}

// Custom hook for debouncing
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);
  
  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);
    
    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);
  
  return debouncedValue;
}

// Usage examples
function UserProfile({ userId }) {
  const { data: user, loading, error } = useApi(`/api/users/${userId}`);
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  
  return (
    <div className={`profile ${theme}`}>
      <h2>{user.name}</h2>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
        Toggle Theme
      </button>
    </div>
  );
}

function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const debouncedSearchTerm = useDebounce(searchTerm, 500);
  const { data: results } = useApi(`/api/search?q=${debouncedSearchTerm}`);
  
  return (
    <div>
      <input
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        placeholder="Search..."
      />
      {results && (
        <ul>
          {results.map(item => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
}
```

### 20. What are the rules of hooks?

**Answer:** Hooks have two fundamental rules that must be followed:

**1. Only call hooks at the top level:**
- Don't call hooks inside loops, conditions, or nested functions
- Always call hooks in the same order

**2. Only call hooks from React functions:**
- Call hooks from React function components
- Call hooks from custom hooks

```jsx
// ❌ Bad - calling hook inside condition
function BadComponent({ shouldFetch }) {
  if (shouldFetch) {
    const [data, setData] = useState(null); // Wrong!
  }
  return <div>Bad</div>;
}

// ❌ Bad - calling hook inside loop
function BadComponent({ items }) {
  items.forEach(item => {
    const [state, setState] = useState(null); // Wrong!
  });
  return <div>Bad</div>;
}

// ❌ Bad - calling hook inside nested function
function BadComponent() {
  const handleClick = () => {
    const [count, setCount] = useState(0); // Wrong!
  };
  return <button onClick={handleClick}>Click</button>;
}

// ✅ Good - calling hooks at top level
function GoodComponent({ shouldFetch, items }) {
  const [data, setData] = useState(null);
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    if (shouldFetch) {
      // Fetch data here
    }
  }, [shouldFetch]);
  
  const handleClick = () => {
    setCount(count + 1);
  };
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Click</button>
    </div>
  );
}
```

---

## State Management

### 21. What is state management and why is it important?

**Answer:** State management is the process of managing and sharing data across components in a React application. It's crucial for maintaining data consistency and managing complex application state.

**Types of state:**
- **Local state**: Component-specific state
- **Global state**: Shared across multiple components
- **Server state**: Data from APIs
- **URL state**: Data in the URL

```jsx
// Local state example
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// Global state with Context
const AppContext = createContext();

function AppProvider({ children }) {
  const [user, setUser] = useState(null);
  const [theme, setTheme] = useState('light');
  
  const value = {
    user,
    setUser,
    theme,
    setTheme,
    isAuthenticated: !!user
  };
  
  return (
    <AppContext.Provider value={value}>
      {children}
    </AppContext.Provider>
  );
}

function useApp() {
  const context = useContext(AppContext);
  if (!context) {
    throw new Error('useApp must be used within AppProvider');
  }
  return context;
}
```

### 22. What is Redux and how does it work?

**Answer:** Redux is a predictable state container for JavaScript applications. It helps manage global state in a predictable way using a unidirectional data flow.

**Redux principles:**
- **Single source of truth**: All state in one store
- **State is read-only**: Only actions can change state
- **Changes via pure functions**: Reducers specify how state changes

```jsx
// Redux setup with Redux Toolkit (modern approach)
import { createSlice, configureStore } from '@reduxjs/toolkit';

// Slice definition
const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
    history: []
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
      state.history.push('increment');
    },
    decrement: (state) => {
      state.value -= 1;
      state.history.push('decrement');
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
      state.history.push(`increment by ${action.payload}`);
    },
    reset: (state) => {
      state.value = 0;
      state.history = [];
    }
  }
});

// Store configuration
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer
  }
});

// Component using Redux
import { useSelector, useDispatch } from 'react-redux';

function Counter() {
  const count = useSelector(state => state.counter.value);
  const history = useSelector(state => state.counter.history);
  const dispatch = useDispatch();
  
  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => dispatch(counterSlice.actions.increment())}>
        Increment
      </button>
      <button onClick={() => dispatch(counterSlice.actions.decrement())}>
        Decrement
      </button>
      <button onClick={() => dispatch(counterSlice.actions.incrementByAmount(5))}>
        +5
      </button>
      <button onClick={() => dispatch(counterSlice.actions.reset())}>
        Reset
      </button>
      
      <h3>History:</h3>
      <ul>
        {history.map((action, index) => (
          <li key={index}>{action}</li>
        ))}
      </ul>
    </div>
  );
}
```

### 23. What is Zustand and how does it compare to Redux?

**Answer:** Zustand is a small, fast, and scalable state management solution. It's simpler than Redux and doesn't require boilerplate code.

**Zustand vs Redux:**
- **Zustand**: Minimal boilerplate, simple API, smaller bundle size
- **Redux**: More structured, better DevTools, larger ecosystem

```jsx
// Zustand store
import { create } from 'zustand';

const useStore = create((set) => ({
  count: 0,
  user: null,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
  setUser: (user) => set({ user }),
  reset: () => set({ count: 0, user: null })
}));

// Component using Zustand
function Counter() {
  const { count, increment, decrement, reset } = useStore();
  
  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

function UserProfile() {
  const { user, setUser } = useStore();
  
  const handleLogin = () => {
    setUser({ name: 'John Doe', email: 'john@example.com' });
  };
  
  return (
    <div>
      {user ? (
        <div>
          <h3>Welcome, {user.name}!</h3>
          <p>Email: {user.email}</p>
        </div>
      ) : (
        <button onClick={handleLogin}>Login</button>
      )}
    </div>
  );
}
```

### 24. What is React Query and how does it help with server state?

**Answer:** React Query (TanStack Query) is a powerful data synchronization library for React. It makes fetching, caching, synchronizing, and updating server state simple.

**Key features:**
- Automatic caching and background updates
- Optimistic updates
- Request deduplication
- Offline support
- DevTools integration

```jsx
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

// Custom hook for fetching users
function useUsers() {
  return useQuery({
    queryKey: ['users'],
    queryFn: async () => {
      const response = await fetch('/api/users');
      if (!response.ok) throw new Error('Failed to fetch users');
      return response.json();
    },
    staleTime: 5 * 60 * 1000, // 5 minutes
    cacheTime: 10 * 60 * 1000, // 10 minutes
  });
}

// Custom hook for creating user
function useCreateUser() {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: async (newUser) => {
      const response = await fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(newUser)
      });
      if (!response.ok) throw new Error('Failed to create user');
      return response.json();
    },
    onSuccess: () => {
      // Invalidate and refetch users
      queryClient.invalidateQueries({ queryKey: ['users'] });
    },
    onError: (error) => {
      console.error('Error creating user:', error);
    }
  });
}

// Component using React Query
function UserList() {
  const { data: users, isLoading, error } = useUsers();
  const createUserMutation = useCreateUser();
  
  const handleCreateUser = () => {
    createUserMutation.mutate({
      name: 'New User',
      email: 'newuser@example.com'
    });
  };
  
  if (isLoading) return <div>Loading users...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return (
    <div>
      <h2>Users</h2>
      <button 
        onClick={handleCreateUser}
        disabled={createUserMutation.isPending}
      >
        {createUserMutation.isPending ? 'Creating...' : 'Add User'}
      </button>
      
      <ul>
        {users?.map(user => (
          <li key={user.id}>
            {user.name} - {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### 25. What is the difference between local and global state?

**Answer:** The choice between local and global state depends on the scope of data usage and component hierarchy.

**Local State:**
- Component-specific data
- Simple to implement
- Better performance (no unnecessary re-renders)
- Use for: form inputs, UI toggles, component-specific data

**Global State:**
- Shared across multiple components
- More complex to implement
- Can cause unnecessary re-renders
- Use for: user authentication, theme, shopping cart

```jsx
// Local state example
function LoginForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [errors, setErrors] = useState({});
  
  const handleSubmit = (e) => {
    e.preventDefault();
    // Validate and submit form
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        placeholder="Password"
      />
      <button type="submit">Login</button>
    </form>
  );
}

// Global state example
const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    // Check for existing session
    const checkAuth = async () => {
      try {
        const token = localStorage.getItem('token');
        if (token) {
          const response = await fetch('/api/me', {
            headers: { Authorization: `Bearer ${token}` }
          });
          if (response.ok) {
            const userData = await response.json();
            setUser(userData);
          }
        }
      } catch (error) {
        console.error('Auth check failed:', error);
      } finally {
        setLoading(false);
      }
    };
    
    checkAuth();
  }, []);
  
  const login = async (email, password) => {
    try {
      const response = await fetch('/api/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ email, password })
      });
      
      if (response.ok) {
        const { user, token } = await response.json();
        localStorage.setItem('token', token);
        setUser(user);
        return { success: true };
      } else {
        return { success: false, error: 'Invalid credentials' };
      }
    } catch (error) {
      return { success: false, error: 'Network error' };
    }
  };
  
  const logout = () => {
    localStorage.removeItem('token');
    setUser(null);
  };
  
  const value = {
    user,
    login,
    logout,
    loading,
    isAuthenticated: !!user
  };
  
  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
}

function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
}

// Components using global auth state
function Header() {
  const { user, logout, isAuthenticated } = useAuth();
  
  return (
    <header>
      <h1>My App</h1>
      {isAuthenticated ? (
        <div>
          <span>Welcome, {user.name}!</span>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <span>Please log in</span>
      )}
    </header>
  );
}

function ProtectedRoute({ children }) {
  const { isAuthenticated, loading } = useAuth();
  
  if (loading) return <div>Loading...</div>;
  if (!isAuthenticated) return <div>Please log in to access this page</div>;
  
  return children;
}
```

---

## Performance Optimization

### 26. What is React.memo and when to use it?

**Answer:** `React.memo` is a higher-order component that memoizes the result of a component and only re-renders if its props have changed. It's useful for preventing unnecessary re-renders.

```jsx
// Without React.memo - re-renders on every parent update
function ExpensiveComponent({ data, onUpdate }) {
  console.log('ExpensiveComponent rendered');
  
  return (
    <div>
      <h3>{data.title}</h3>
      <p>{data.description}</p>
      <button onClick={() => onUpdate(data.id)}>Update</button>
    </div>
  );
}

// With React.memo - only re-renders when props change
const MemoizedExpensiveComponent = React.memo(ExpensiveComponent);

// Custom comparison function
const CustomMemoizedComponent = React.memo(ExpensiveComponent, (prevProps, nextProps) => {
  // Return true if props are equal (don't re-render)
  // Return false if props are different (re-render)
  return prevProps.data.id === nextProps.data.id && 
         prevProps.data.title === nextProps.data.title;
});

// Parent component
function ParentComponent() {
  const [count, setCount] = useState(0);
  const [data, setData] = useState({
    id: 1,
    title: 'Sample Title',
    description: 'Sample Description'
  });
  
  const handleUpdate = useCallback((id) => {
    setData(prev => ({ ...prev, title: 'Updated Title' }));
  }, []);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      
      {/* This won't re-render when count changes */}
      <MemoizedExpensiveComponent 
        data={data} 
        onUpdate={handleUpdate} 
      />
    </div>
  );
}
```

### 27. What is useMemo and how does it optimize performance?

**Answer:** `useMemo` memoizes the result of a computation and only recalculates it when its dependencies change. It's useful for expensive calculations.

```jsx
function ExpensiveCalculation({ items, filter, sortBy }) {
  // Expensive calculation that only runs when dependencies change
  const processedItems = useMemo(() => {
    console.log('Processing items...');
    
    let filtered = items.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
    
    filtered.sort((a, b) => {
      if (sortBy === 'name') return a.name.localeCompare(b.name);
      if (sortBy === 'price') return a.price - b.price;
      return 0;
    });
    
    return filtered;
  }, [items, filter, sortBy]);
  
  // Another expensive calculation
  const statistics = useMemo(() => {
    console.log('Calculating statistics...');
    
    return {
      total: processedItems.length,
      averagePrice: processedItems.reduce((sum, item) => sum + item.price, 0) / processedItems.length,
      categories: [...new Set(processedItems.map(item => item.category))].length
    };
  }, [processedItems]);
  
  return (
    <div>
      <h3>Statistics</h3>
      <p>Total items: {statistics.total}</p>
      <p>Average price: ${statistics.averagePrice.toFixed(2)}</p>
      <p>Categories: {statistics.categories}</p>
      
      <ul>
        {processedItems.map(item => (
          <li key={item.id}>
            {item.name} - ${item.price} - {item.category}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### 28. What is useCallback and how does it prevent unnecessary re-renders?

**Answer:** `useCallback` returns a memoized version of a callback function that only changes if one of its dependencies has changed. It's useful for preventing child components from re-rendering unnecessarily.

```jsx
// Without useCallback - function recreated on every render
function ParentWithoutCallback() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  // This function is recreated on every render
  const handleClick = () => {
    console.log('Button clicked');
  };
  
  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
        placeholder="Name"
      />
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      
      {/* Child re-renders every time parent re-renders */}
      <ExpensiveChild onClick={handleClick} />
    </div>
  );
}

// With useCallback - function only recreated when dependencies change
function ParentWithCallback() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  // Memoized callback - only recreated when count changes
  const handleClick = useCallback(() => {
    console.log('Button clicked, count:', count);
  }, [count]);
  
  // Memoized callback with no dependencies
  const handleReset = useCallback(() => {
    setCount(0);
    setName('');
  }, []);
  
  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
        placeholder="Name"
      />
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={handleReset}>Reset</button>
      
      {/* Child only re-renders when handleClick changes */}
      <ExpensiveChild onClick={handleClick} />
    </div>
  );
}

const ExpensiveChild = React.memo(({ onClick }) => {
  console.log('ExpensiveChild rendered');
  
  return (
    <div>
      <button onClick={onClick}>Click me</button>
    </div>
  );
});
```

### 29. What is code splitting and how to implement it in React?

**Answer:** Code splitting is a technique that allows you to split your code into smaller chunks that can be loaded on demand. This improves the initial loading time of your application.

**Methods of code splitting:**
1. **Route-based splitting** (most common)
2. **Component-based splitting**
3. **Library splitting**

```jsx
import { lazy, Suspense } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

// Lazy load components
const Home = lazy(() => import('./components/Home'));
const About = lazy(() => import('./components/About'));
const Contact = lazy(() => import('./components/Contact'));
const Dashboard = lazy(() => import('./components/Dashboard'));

// Loading component
function LoadingSpinner() {
  return (
    <div className="loading">
      <div className="spinner"></div>
      <p>Loading...</p>
    </div>
  );
}

// Main App component
function App() {
  return (
    <Router>
      <div className="app">
        <nav>
          <Link to="/">Home</Link>
          <Link to="/about">About</Link>
          <Link to="/contact">Contact</Link>
          <Link to="/dashboard">Dashboard</Link>
        </nav>
        
        <Suspense fallback={<LoadingSpinner />}>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/contact" element={<Contact />} />
            <Route path="/dashboard" element={<Dashboard />} />
          </Routes>
        </Suspense>
      </div>
    </Router>
  );
}

// Component-based code splitting
function LazyModal() {
  const [showModal, setShowModal] = useState(false);
  const [ModalComponent, setModalComponent] = useState(null);
  
  const openModal = async () => {
    if (!ModalComponent) {
      const { default: Modal } = await import('./components/Modal');
      setModalComponent(() => Modal);
    }
    setShowModal(true);
  };
  
  return (
    <div>
      <button onClick={openModal}>Open Modal</button>
      {showModal && ModalComponent && (
        <ModalComponent onClose={() => setShowModal(false)} />
      )}
    </div>
  );
}

// Library splitting with dynamic imports
function ChartComponent() {
  const [Chart, setChart] = useState(null);
  const [loading, setLoading] = useState(false);
  
  const loadChart = async () => {
    setLoading(true);
    try {
      const { Chart } = await import('chart.js');
      setChart(() => Chart);
    } catch (error) {
      console.error('Failed to load chart library:', error);
    } finally {
      setLoading(false);
    }
  };
  
  useEffect(() => {
    loadChart();
  }, []);
  
  if (loading) return <div>Loading chart...</div>;
  if (!Chart) return <div>Chart library not available</div>;
  
  return <div>Chart component loaded</div>;
}
```

### 30. What is virtualization and when to use it?

**Answer:** Virtualization is a technique that renders only the visible items in a large list, improving performance by reducing the number of DOM nodes.

**When to use virtualization:**
- Large lists (1000+ items)
- Complex list items
- Performance issues with scrolling
- Memory constraints

```jsx
import { FixedSizeList as List } from 'react-window';

// Virtualized list component
function VirtualizedList({ items }) {
  const Row = ({ index, style }) => (
    <div style={style}>
      <div className="list-item">
        <h3>{items[index].name}</h3>
        <p>{items[index].description}</p>
        <span>ID: {items[index].id}</span>
      </div>
    </div>
  );
  
  return (
    <List
      height={600}        // Height of the visible area
      itemCount={items.length}  // Total number of items
      itemSize={120}      // Height of each item
      width="100%"        // Width of the list
    >
      {Row}
    </List>
  );
}

// Custom virtualized list with dynamic heights
import { VariableSizeList as List } from 'react-window';

function DynamicVirtualizedList({ items }) {
  const getItemSize = (index) => {
    // Return different heights based on content
    const item = items[index];
    const baseHeight = 60;
    const descriptionHeight = Math.ceil(item.description.length / 50) * 20;
    return baseHeight + descriptionHeight;
  };
  
  const Row = ({ index, style }) => (
    <div style={style}>
      <div className="dynamic-list-item">
        <h3>{items[index].name}</h3>
        <p>{items[index].description}</p>
        <div className="metadata">
          <span>ID: {items[index].id}</span>
          <span>Category: {items[index].category}</span>
        </div>
      </div>
    </div>
  );
  
  return (
    <List
      height={600}
      itemCount={items.length}
      itemSize={getItemSize}
      width="100%"
    >
      {Row}
    </List>
  );
}

// Usage example
function App() {
  const [items, setItems] = useState([]);
  
  useEffect(() => {
    // Generate large dataset
    const generateItems = () => {
      return Array.from({ length: 10000 }, (_, index) => ({
        id: index,
        name: `Item ${index}`,
        description: `This is a description for item ${index}. It contains some detailed information about the item.`,
        category: ['Category A', 'Category B', 'Category C'][index % 3]
      }));
    };
    
    setItems(generateItems());
  }, []);
  
  return (
    <div>
      <h1>Virtualized List Example</h1>
      <VirtualizedList items={items} />
    </div>
  );
}
```

---

*[The guide continues with Advanced Topics, Forms & Validation, and Data Fetching & API sections, each containing detailed explanations, code examples, and best practices for React development. This comprehensive guide covers all essential React concepts needed for technical interviews.]*
