# React

## Concepts:

```bash
Component based
JSX and HTML
Updates on change of props

component lifecycle:
1. component is mounted (componentDidMount())
2. component state can update (componentDidUpdate())
3. component is destroyed (componentWillUnmount())
```

## Components:

```tsx
function Item(props){
	return <p>{props.text}</p>
}
```

## Hooks:

```tsx
// Love level primitives 
// only called at top level of functional component
```

## useState()

```tsx
// useState
const [count, setCount] = useState(0);
// count changes and UI rerenders
```

## useEffect()

```tsx
// useEffect
useEffect(
	() => {
		alert('side effect') // Runs when mounted and when state changes
		return () => alert('destroying component') // runs when a component is destroyed
	}, 
	[count]  // dependencies to watch for effect running
)

```

## useContext()

```tsx
// useContext (context API)
const moods = { happy: ':)', sad: ':(' }
const MoodContext = createContext(moods);

function App(props){
	
	return (
		// Scopes the context into the children nodes
		<MoodContext.Provider value={moods.happy}>
			<MoodEmoji/>
		</MoodContext.Provider>
	);
}

// Consumes the context from the provider
function MoodEmoji(){
	const mood = useContext(MoodContext);
	return <p>{ mood }</p>
}

```

## useRef()

```tsx
// useRef as a reference value
function App() {

	const count = useRef(0);

	return (
		// Mutable value will not update the view of the UI
		<button onClick={() => count.current++}>
			{count.current} 
		</button>
	);
}

// useRef grabbing elements from the DOM
function App() {

	const myBtn = useRef(null);

	const clickIt = () => myBtn.current.click();

	return (
		// Mutable value will not update the view of the UI
		<button ref={myBtn}></button>
	);
}
```

## useReducer()

```tsx
// useReducer (Redux pattern)
// Action -> Reducer function -> Store next state
function App(){
	
	// Reducer function used to select action
	function reducer(state, action){
		switch(action.type){
			case 'increment':
				return state + 1;
			case 'decrement':
				return state - 1;
			default:
				throw new Error();
		}
	}

	// Takes reducer function and initial state
	const [state] = useReducer(reducer, 0);
	
	// Control state according to buttons
	return(
		<>
			Count: {state}
			<button onClick={() => dispatch({type: 'decrement'})}> - </button>
			<button onClick={() => dispatch({type: 'increment'})}> + </button>
		</>
	);
}
```

## useMemo()

```tsx
// useMemo (memoization-> cache result of a a function call)
function App(){

	const [count, setCount] = useState(60);

	// Optimises expensive computation
	const expensiveCount = useMemo(
		() =>{
			return count ** 2;
		},
		[count]
	)

	return <></>;
}
```

## useCallback()

```tsx
// useCallback (memoization for entire function)
// new function object created for every rerender

function App(){

	const [count, setCount] = useState(60);

	// Wrap function to ensure a single object is used
	const showCount = useCallback(() => {
		alert(`Count ${count}`)
	}, [count])
	
	// children wil use the sinle instance
	return <> <SomeChild handler={showCount}/> </>;
}
```

## useImperativeHandle()

```tsx
// useImperativeHandle
// Building component library, access underlying DOM element

function App() {
	const ref= useRef(null);

	return <NewButton ref={ref}></NewButton>
}

function NewButton(props, ref){
	
	const myBtn = useRef(null);

	// modifies the ref exposed by the App function
	useImpreativeHandle(ref, () => ({
		click: () => {
			console.log('clicking button');
			myBtn.current.click();
		}
	}))	;

	return (
		<button ref={myBtn}></button>
	);
}

// Make reference available
NewButton = forwardRef(NewButton);
```

## useLayoutEffect()

```tsx
// useLayoutEffect
// Works like useEffect but runs after render and before painting to screen
// Blocks UI update as long as not done running

function App() {

		const myBtn = useRef(null);
		
		useLayoutEffect(() =>{
			const rect = myBtn.current.getBoundingClientRect();
			console.log(rect.height)
		});

		return <> <button ref={myBtn}></button> </>
}
```

## useDebugValue()

```tsx
// useDebugValue()
// permits custom labels in react dev tools in browser when building custom hooks

function App() {
	
	const	displayName = useDisplayName();

	return <button>{displayName}</button>
}

// Custom hook
function useDisplayName(){

	// Custom logic to implement (when rerender sets displayName from database)
	const [displayName, setDisplayName] = useState('');
	useEffect(() => {
		const data = fetchFromDb(props.userId)
		setDisplayName(data.displayName);
	}, []);

	// shows the displayname in browser components
	useDebugValue(displayName ?? 'loading...')	

	return displayName;
}
```

## Other React stuff

```tsx
Static site -> Gatsby
Server Side Rendering -> Next.JS
Animation -> Spring
Forms -> Formik

https://github.com/enaqx/awesome-react
```