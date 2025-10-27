# 100 React.js Interview Questions & Answers

## Fundamentals (1-15)

### 1. What is React and why use it?
React is a JavaScript library for building user interfaces with reusable components. Benefits include efficient rendering, unidirectional data flow, strong community support, and easier state management.

### 2. What is JSX?
```jsx
// JSX
const element = <h1>Hello, {name}!</h1>;

// Transpiles to:
const element = React.createElement('h1', null, `Hello, ${name}!`);
```

### 3. What is the difference between functional and class components?
```jsx
// Functional Component
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Class Component
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### 4. What are props?
Props are read-only data passed to components. They enable component reusability and data flow from parent to child.

```jsx
function Greeting({ name, age }) {
  return <p>{name} is {age} years old</p>;
}

<Greeting name="John" age={25} />
```

### 5. What is state?
State is mutable data managed within a component that triggers re-renders when updated.

```jsx
const [count, setCount] = useState(0);
return <button onClick={() => setCount(count + 1)}>{count}</button>;
```

### 6. Difference between state and props?
- Props: immutable, passed from parent to child
- State: mutable, local to component, triggers re-renders when changed

### 7. What are keys in lists?
Keys help React identify which items have changed, been added, or been removed.

```jsx
{items.map((item) => <div key={item.id}>{item.name}</div>)}
```

### 8. What is the virtual DOM?
The virtual DOM is a lightweight JavaScript representation of the real DOM. React uses it to calculate optimal updates before applying them to the actual DOM.

### 9. What is reconciliation?
Reconciliation is React's algorithm for comparing the new virtual DOM with the previous one and updating only changed elements.

### 10. What is a controlled component?
```jsx
function TextInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

### 11. What is an uncontrolled component?
```jsx
function TextInput() {
  const ref = useRef();
  return <input ref={ref} />;
}
```

### 12. What is the difference between controlled and uncontrolled components?
- Controlled: React state manages input values
- Uncontrolled: DOM manages input values directly

### 13. What are synthetic events?
React's cross-browser wrapper around the browser's native event system. They're pooled for performance.

```jsx
<button onClick={(e) => console.log(e.type)}>Click</button>
```

### 14. What is the React Fragment?
A wrapper to return multiple elements without adding extra nodes to the DOM.

```jsx
<>
  <h1>Title</h1>
  <p>Content</p>
</>
```

### 15. What are higher-order components (HOC)?
```jsx
function withLogProps(WrappedComponent) {
  return (props) => {
    console.log(props);
    return <WrappedComponent {...props} />;
  };
}

const Enhanced = withLogProps(MyComponent);
```

---

## Hooks (16-35)

### 16. What are React Hooks?
Functions that let you use state and other React features in functional components.

### 17. What is useState?
```jsx
const [state, setState] = useState(initialValue);
```

### 18. What is useEffect?
```jsx
useEffect(() => {
  console.log('Component mounted or dependency changed');
  return () => console.log('Cleanup');
}, [dependency]);
```

### 19. What is the dependency array in useEffect?
- `[]`: Effect runs once after mount
- `[dep]`: Effect runs when dep changes
- No array: Effect runs after every render

### 20. What is useContext?
```jsx
const theme = useContext(ThemeContext);
```

### 21. What is useReducer?
```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

### 22. useReducer vs useState?
useState is for simple state, useReducer is for complex state logic with multiple sub-values.

### 23. What is useRef?
```jsx
const inputRef = useRef();
inputRef.current.focus();
```

### 24. What is useCallback?
```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

### 25. What is useMemo?
```jsx
const memoizedValue = useMemo(() => expensiveCalculation(a, b), [a, b]);
```

### 26. useCallback vs useMemo?
useCallback memoizes functions, useMemo memoizes values.

### 27. What is useLayoutEffect?
Fires synchronously after DOM mutations but before the browser paints. Use for animations.

### 28. What is useImperativeHandle?
```jsx
useImperativeHandle(ref, () => ({
  focus: () => inputRef.current.focus(),
}));
```

### 29. What is useDebugValue?
```jsx
useDebugValue(isOnline ? 'Online' : 'Offline');
```

### 30. Can you call hooks conditionally?
No. Hooks must be called at the top level and in the same order every render.

### 31. Can you use hooks in classes?
No. Hooks are only for functional components. Use class lifecycle methods instead.

### 32. What is a custom hook?
```jsx
function useFormInput(initialValue) {
  const [value, setValue] = useState(initialValue);
  return {
    value,
    onChange: (e) => setValue(e.target.value),
  };
}
```

### 33. What is a custom hook with API call?
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);
  return data;
}
```

### 34. How to fetch data with useEffect?
```jsx
useEffect(() => {
  fetch('/api/data')
    .then(res => res.json())
    .then(data => setData(data))
    .catch(err => setError(err));
}, []);
```

### 35. How to cleanup async operations in useEffect?
```jsx
useEffect(() => {
  let isMounted = true;
  fetch('/api/data').then(data => {
    if (isMounted) setData(data);
  });
  return () => (isMounted = false);
}, []);
```

---

## Component Lifecycle (36-50)

### 36. What are class component lifecycle methods?
mounting, updating, unmounting, and error handling phases.

### 37. What is componentDidMount?
```jsx
componentDidMount() {
  console.log('Component mounted');
  this.fetchData();
}
```

### 38. What is componentDidUpdate?
```jsx
componentDidUpdate(prevProps, prevState) {
  if (prevProps.id !== this.props.id) {
    this.fetchData();
  }
}
```

### 39. What is componentWillUnmount?
```jsx
componentWillUnmount() {
  console.log('Component unmounting');
  clearTimeout(this.timer);
}
```

### 40. What is shouldComponentUpdate?
```jsx
shouldComponentUpdate(nextProps, nextState) {
  return nextProps.id !== this.props.id;
}
```

### 41. What are static getDerivedStateFromProps?
```jsx
static getDerivedStateFromProps(props, state) {
  if (props.id !== state.id) {
    return { id: props.id };
  }
  return null;
}
```

### 42. What is getSnapshotBeforeUpdate?
```jsx
getSnapshotBeforeUpdate(prevProps, prevState) {
  return { scrollPosition: window.scrollY };
}
```

### 43. How to handle errors with componentDidCatch?
```jsx
componentDidCatch(error, errorInfo) {
  console.log(error, errorInfo);
  this.setState({ hasError: true });
}
```

### 44. What is an Error Boundary?
```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  componentDidCatch(error, errorInfo) {
    console.log(error);
  }
  render() {
    if (this.state.hasError) return <h1>Error</h1>;
    return this.props.children;
  }
}
```

### 45. What is React.StrictMode?
```jsx
<React.StrictMode>
  <App />
</React.StrictMode>
```
Helps identify potential problems in development.

### 46. Lifecycle in functional components with hooks?
```jsx
// Mount
useEffect(() => {}, []);

// Update
useEffect(() => {}, [dep]);

// Unmount
useEffect(() => () => {}, []);
```

### 47. What is Suspense?
```jsx
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

### 48. What is React.lazy?
```jsx
const LazyComponent = React.lazy(() => import('./Component'));
```

### 49. What are fragments and when to use them?
Use to return multiple elements without adding DOM nodes.

### 50. What is memo?
```jsx
const MyComponent = React.memo(function Component(props) {
  return <div>{props.value}</div>;
});
```
Prevents re-renders if props haven't changed.

---

## State Management (51-65)

### 51. What is Context API?
```jsx
const MyContext = React.createContext();

<MyContext.Provider value={{ name: 'John' }}>
  <Child />
</MyContext.Provider>

const { name } = useContext(MyContext);
```

### 52. How to avoid Context re-rendering all consumers?
```jsx
const value = useMemo(() => ({ data }), [data]);
<Context.Provider value={value}>{children}</Context.Provider>
```

### 53. What is useReducer vs Redux?
useReducer is built-in for local state, Redux is for global state management.

### 54. How to implement Redux?
```jsx
const reducer = (state, action) => {
  switch(action.type) {
    case 'INCREMENT': return state + 1;
    default: return state;
  }
};
const store = createStore(reducer);
```

### 55. What is Redux middleware?
Middleware intercepts actions before they reach the reducer.

```jsx
store.subscribe(() => console.log(store.getState()));
```

### 56. What is Redux-Thunk?
```jsx
const fetchData = () => async (dispatch) => {
  dispatch({ type: 'LOADING' });
  const data = await fetch('/api');
  dispatch({ type: 'SUCCESS', payload: data });
};
```

### 57. What is Redux-Saga?
Alternative to thunk using generator functions for complex async flows.

### 58. How to connect React to Redux?
```jsx
import { useSelector, useDispatch } from 'react-redux';

function Component() {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();
  return <button onClick={() => dispatch({ type: 'INCREMENT' })}>{count}</button>;
}
```

### 59. What are selectors?
```jsx
export const selectCount = state => state.count;
const count = useSelector(selectCount);
```

### 60. What is Redux Toolkit?
Modern way to write Redux with less boilerplate.

```jsx
import { createSlice } from '@reduxjs/toolkit';
const counterSlice = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: state => state + 1,
  },
});
```

### 61. What is Recoil?
Alternative state management library for React with atoms and selectors.

### 62. What is Zustand?
Lightweight state management library with minimal boilerplate.

### 63. What is Jotai?
Primitive and flexible state management library.

### 64. How to manage form state?
```jsx
const [form, setForm] = useState({ name: '', email: '' });
const handleChange = (e) => {
  setForm({ ...form, [e.target.name]: e.target.value });
};
```

### 65. What are controlled forms vs uncontrolled?
Controlled: React state manages form data. Uncontrolled: DOM manages form data.

---

## Performance (66-80)

### 66. What is React.memo?
```jsx
export default React.memo(MyComponent);
```

### 67. How to optimize re-renders?
Use React.memo, useMemo, useCallback, and production build.

### 68. What is code splitting?
```jsx
const Component = React.lazy(() => import('./Component'));
```

### 69. What is tree shaking?
Removing unused code during build process.

### 70. How to measure performance?
```jsx
console.time('render');
// code
console.timeEnd('render');
```

### 71. What are React DevTools?
Browser extension for debugging React components.

### 72. How to use Profiler API?
```jsx
import { Profiler } from 'react';

function onRenderCallback(id, phase, actualDuration) {
  console.log(`${id} (${phase}) took ${actualDuration}ms`);
}

<Profiler id="App" onRender={onRenderCallback}>
  <App />
</Profiler>
```

### 73. What is lazy loading?
Loading components only when needed.

```jsx
const HeavyComponent = React.lazy(() => import('./Heavy'));
```

### 74. How to optimize images?
Use CDN, compression, lazy loading, and responsive images.

### 75. What is bundle size?
Total size of JavaScript sent to browser. Optimize with code splitting.

### 76. How to analyze bundle size?
Use webpack-bundle-analyzer or similar tools.

### 77. What is tree shaking?
```jsx
// In package.json
"sideEffects": false
```

### 78. How to use web workers?
Offload heavy computation to background thread.

### 79. What is virtual scrolling?
Rendering only visible items in long lists.

### 80. How to optimize animations?
Use CSS animations, transform, opacity, and avoid layout thrashing.

---

## Advanced Topics (81-100)

### 81. What is render props?
```jsx
function MouseTracker() {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={(e) => setPos({ x: e.x, y: e.y })}>
      {props.children(pos)}
    </div>
  );
}
```

### 82. What is compound components?
```jsx
<Tabs>
  <Tabs.Panel label="Tab1"><div>Content1</div></Tabs.Panel>
  <Tabs.Panel label="Tab2"><div>Content2</div></Tabs.Panel>
</Tabs>
```

### 83. What is prop drilling?
Passing props through many levels. Solved with Context API.

### 84. How to handle modal state?
```jsx
const [isOpen, setIsOpen] = useState(false);
return (
  <>
    <button onClick={() => setIsOpen(true)}>Open</button>
    {isOpen && <Modal onClose={() => setIsOpen(false)} />}
  </>
);
```

### 85. What is authentication in React?
```jsx
function PrivateRoute({ component: Component }) {
  const isAuth = !!localStorage.getItem('token');
  return isAuth ? <Component /> : <Navigate to="/login" />;
}
```

### 86. How to implement infinite scroll?
```jsx
useEffect(() => {
  window.addEventListener('scroll', handleScroll);
  return () => window.removeEventListener('scroll', handleScroll);
}, []);
```

### 87. What is debouncing?
```jsx
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);
  useEffect(() => {
    const timeout = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(timeout);
  }, [value, delay]);
  return debouncedValue;
}
```

### 88. What is throttling?
```jsx
function useThrottle(callback, delay) {
  const ref = useRef(null);
  return (...args) => {
    if (!ref.current) {
      callback(...args);
      ref.current = true;
      setTimeout(() => (ref.current = null), delay);
    }
  };
}
```

### 89. How to implement search with suggestions?
```jsx
const [search, setSearch] = useState('');
const debouncedSearch = useDebounce(search, 300);
useEffect(() => {
  fetch(`/api/search?q=${debouncedSearch}`).then(setResults);
}, [debouncedSearch]);
```

### 90. How to handle errors globally?
```jsx
class ErrorBoundary extends React.Component {
  componentDidCatch(error, errorInfo) {
    logErrorToService(error, errorInfo);
  }
  render() {
    if (this.state.hasError) return <ErrorFallback />;
    return this.props.children;
  }
}
```

### 91. What is SSR?
Server-Side Rendering renders components on server and sends HTML to client.

### 92. What is SSG?
Static Site Generation pre-renders pages at build time.

### 93. What is ISR?
Incremental Static Regeneration updates static pages at intervals.

### 94. How to implement dark mode?
```jsx
const [isDark, setIsDark] = useState(false);
useEffect(() => {
  document.documentElement.setAttribute('data-theme', isDark ? 'dark' : 'light');
}, [isDark]);
```

### 95. How to handle file uploads?
```jsx
function FileUpload() {
  const handleFile = (e) => {
    const file = e.target.files[0];
    const formData = new FormData();
    formData.append('file', file);
    fetch('/upload', { method: 'POST', body: formData });
  };
  return <input type="file" onChange={handleFile} />;
}
```

### 96. How to use Web APIs in React?
```jsx
useEffect(() => {
  navigator.geolocation.getCurrentPosition((pos) => {
    setLocation({ lat: pos.coords.latitude, lng: pos.coords.longitude });
  });
}, []);
```

### 97. How to implement real-time updates with WebSocket?
```jsx
useEffect(() => {
  const ws = new WebSocket('ws://localhost:8000');
  ws.onmessage = (event) => setData(JSON.parse(event.data));
  return () => ws.close();
}, []);
```

### 98. What is internationalization (i18n)?
Using i18n libraries like i18next to support multiple languages.

### 99. What is testing in React?
```jsx
import { render, screen } from '@testing-library/react';
test('renders greeting', () => {
  render(<Greeting name="John" />);
  expect(screen.getByText(/Hello, John/i)).toBeInTheDocument();
});
```

### 100. What is E2E testing?
```jsx
describe('User flow', () => {
  it('should login and view dashboard', () => {
    cy.visit('/');
    cy.get('input[name="email"]').type('test@test.com');
    cy.get('button[type="submit"]').click();
    cy.contains('Dashboard').should('be.visible');
  });
});
```