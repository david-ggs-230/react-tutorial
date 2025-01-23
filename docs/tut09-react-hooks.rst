.. _tut09-react-hooks:


.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-green
   :class: sd-text-success
    
.. role:: custom-color-red
   :class: sd-text-danger
    
.. role:: custom-color-black
   :class: sd-text-black
   
.. role:: custom-color-primary-underline
   :class: sd-text-primary sd-text-decoration-line-underline
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold

.. rst-class:: title-center h1
   
React Hooks

##################################################################################################
Tut09-React Hooks
##################################################################################################

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut09-react-hooks> ::
    
    yarn create react-app tut09-react-hooks
    
- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Install React Router ::
    
    # yarn add react-router-dom or npm install react-router-dom --save
    yarn add -D react-router-dom
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut09-react-hooks> ::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
React Hooks
**************************************************************************************************

Hooks were added to React in version 16.8. React hooks are a powerful feature that allow you to use state, lifecycle methods, and other React features in functional components. 

Hook Rules: 
    
    - Hooks can only be called inside React function components.
    - Hooks can only be called at the top level of a component.
    - Hooks cannot be conditional
    
The main hooks include useState, useEffect, useContext, useReducer, useCallback, useMemo, useRef, and useImperativeHandle, among others. These hooks provide ways to access React features, allowing you to better organize and reuse your code.

==================================================================================================
useState
==================================================================================================

useState is a basic React hook, which allows a function component to maintain its own state and re-render itself based on the state changes. The signature of the useState is as follows ::
    
    const [ <state>, <setState> ] = useState( <initialValue> )
    # initialValue − Initial value of the state. state can be specified in any type (number, string, array and object).
    # state − Variable to represent the value of the state.
    # setState − Function variable to represent the function to update the state returned by the useState.
    # useState accepts a function parameter instead of initial value and execute the function only 
    #    once during initial rendering of the component. This will help to improve the performance, 
    #    if the computation of initial value is expensive.
    #    signature: const [ <state>, <setState> ] = useState(() => { ... ; return <initialValue>; })
    
The signature of the setState function is as follows ::
    
    setState( <valueToBeUpdated> )
    
The sample usage to set and update the user's name is as follows ::
    
    // initialize the state
    const [name, setName] = useState('John')
    
    // update the state
    setName('Peter)
    
useState with Function Parameter ::
    
    const [val, setVal] = useState(() => {
       var initialValue = null
       // expensive calculation of initial value
       return initialValue
    })
    
Batches multiple state updates − Multiple state updates are batched and processed by React internally. If multiple state update has to be done immediately, then the special function flushSync provided by React can be used, which will immediately flush all the state changes. ::
    
    flushSync(() => setName('Peter'))
    

- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Create the file ``./UseStateComponent.js`` ::
    
    import React, { useState } from 'react';
    
    function UseStateComponent() {
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <h2>React Hooks- useState</h2>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
      );
    }
    
    export default UseStateComponent;
    
- Edit the file ``App.js`` ::
    
    import UseStateComponent from './UseStateComponent';
    import './App.css';
    
    function App() {
      return (
        <div className="App">
          <UseStateComponent />
        </div>
      );
    }
    
    export default App;

    
- Screenshot
    
    .. figure:: images/tut09/tut09-react-hooks-usestate.png
       :align: center
       :class: sd-mb-1
       :alt: React Hooks- useState
       
       :custom-color-primary-bold:`React Hooks- useState`, Click :bdg-secondary-line:`Click Me` button to change the internal ``count`` state
    

==================================================================================================
useEffect
==================================================================================================

React provides useEffect to do side-effects in a component. Some of the side effects are as follows ::
    
    - Fetching data from external source & updating the rendered content.
    - Updating DOM elements after rendering.
    - Subscriptions
    - Using Timers
    - Logging
    
In class based components, these side effects are done using life cycle components. So, useEffect hook is an effect replacement for below mentioned life cycle events. ::
    
    - componentDidMount − Fires after the rendering is done for the first time.
    - componentDidUpdate − Fires after the rendering is updated due to prop or state changes.
    - componentWillUnmount − Fires after the rendered content is unmounted during destruction of component.
    
The signature of useEffect is as follows ::
    
    useEffect( <update function>, <dependency> )
    # the signature of the update function is:
    #    {
    #       // code
    #       return <clean up function>
    #    }
    
useEffect( <update function>, <dependency> ):
    
    - Update function − Update function is the function to be executed after each render phase. This corresponds to componentDidMount and componentDidUpdate events
    - Dependency − Dependency is an array with all the variables on which the function is dependent. Specifying the dependency is very important to optimize the effect hook. In general, update function is called after each render. Sometimes it is not necessary to render update function on each render.
    

- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Create the file ``./UseEffectComponent.js`` ::
    
    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function UseEffectComponent () {
      const [count, setCount] = useState(0);
    
      if (typeof UseEffectComponent.logMessages == 'undefined') {
        UseEffectComponent.logMessages = [];
      }
    
      const handleClick=()=>{
        setCount(count + 1);
        UseEffectComponent.logMessages.push("Button was Clicked! Count is "+(count+1)+".");
      }
      useEffect (() => {
        UseEffectComponent.logMessages.push ('Component mounted');
        return () => {
          // Cleanup function - equivalent to componentWillUnmount
          UseEffectComponent.logMessages.push ('Component unmounted');
        };
      }, []); // Empty dependency array to run only once on initial render
      // Equivalent to componentDidMount and componentDidUpdate
      useEffect (
        () => {
          // This will run after the component mounts and every time `count` changes
          UseEffectComponent.logMessages.push ('Component mounted or updated');
          // Cleanup function - equivalent to componentWillUnmount
          return () => {
            // Cleanup function - equivalent to componentWillUnmount
            UseEffectComponent.logMessages.push ('Component unmounted for [count] <dependency>');
          };
      },[count]); // The effect depends on the `count` state
    
      return (
        <div>
          <h2>React Hooks- useEffect</h2>
          <p>You clicked {count} times</p>
          <button onClick={handleClick}>Click me</button>
          <div className="App">
            <h5>LogMessages</h5>
            {/* Display the list of messages */}
            <ul>
              {UseEffectComponent.logMessages.map ((message, index) => (
                <li key={index}>{message}</li>
              ))}
            </ul>
          </div>
        </div>
      );
    }
    
    export default UseEffectComponent;
    
- Edit the file ``App.js`` ::
    
    import UseEffectComponent from './UseEffectComponent'
    import './App.css';
    
    function App() {
      return (
        <div className="App">
          <UseEffectComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut09/tut09-react-hooks-useeffect.png
       :align: center
       :class: sd-mb-1
       :alt: React Hooks- useEffect
       
       :custom-color-primary-bold:`React Hooks- useEffect`, Click :bdg-secondary-line:`Click Me` button to change the internal ``count`` state
    

==================================================================================================
useContext
==================================================================================================

Context is one of the important concept in React. It provides the ability to pass a information from the parent component to all its children to any nested level without passing the information through props in each level. Context will make the code more readable and simple to understand. Context can be used to store information which does not change or have minimal change. Some of the use cases of context are as follows
    
    - Application configuration
    - Current authenticated user information
    - Current user setting
    - Language setting
    - Theme / Design configuration by application / users
    
Context usage through hook
    
    - Creating a new context ::
        
        // Create a Context
        const ThemeContext = React.createContext({
           color: 'black',
           backgroundColor: 'white'
        })
        
    - Setting context provider in the root component ::
        
        <ThemeContext.Provider value={{
           color: 'white',
           backgroundColor: 'green'
        }}>
            <children components.../>
        </ThemeContext.Provider>
        
    - Setting context consumer in the component where we need the context information ::
        
        import ThemeContext from "ThemeContext";
        const theme = useContext(ThemContext)
        
    - Accessing context information and using it in render method ::
        
        let theme = useContext(ThemeContext)
        return (
           <div style={{
              color: theme.color,
              backgroundColor: theme.backgroundColor }}>
                 Hello World
           </div>
        )
        
Updating context: Updating the context will rerender all the child component. React provides an option to update the context by using both useState and useContext hook.
    
    - In the root component, use useState hook to manage the theme information ::
        
        const [theme, setTheme] = useState({...})
        <ThemeContext.Provider value={{ theme, setTheme }}>
            <children components.../>
        </ThemeContext.Provider>
        
    - In the component where we need the context information, use useContext and state update function ::
        
        import ThemeContext from "ThemeContext";
        let { theme, setTheme } = useContext(ThemeContext)
        const handleClick=(color)=>{
          setTheme({color: color});
        }
        

- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Create the file ``./ThemeContext.js`` ::
    
    import React from 'react'
    
    const ThemeContext = React.createContext();
    
    export default ThemeContext;
    
- Create the file ``./UseContextComponent.js`` ::
    
    import React, { useContext } from 'react';
    import ThemeContext from "./ThemeContext";
    
    function UseContextComponent() {
      const { theme, setTheme } = useContext(ThemeContext)
      const handleClick=(color)=>{
        setTheme({color: color});
      }
      return (
        <div>
          <h2>React Hooks- useContext</h2>
          <p>
             Context Color: <span style={{color: theme.color }}>{theme.color} </span> 
          </p>
          <button onClick={() => handleClick('red')}>Red</button>
          <button  style={{marginLeft: '10px'}} onClick={() => handleClick('blue')}>Blue</button>
        </div>
      );
    }
    
    export default UseContextComponent;
    
- Edit the file ``App.js`` ::
    
    import { useState } from 'react'
    import UseContextComponent from './UseContextComponent'
    import ThemeContext from './ThemeContext'
    import './App.css';
    
    function App() {
      const [theme, setTheme] = useState({color: 'green'});
      return (
        <div className='App'>
          <ThemeContext.Provider  value={{ theme, setTheme }} >
              <UseContextComponent />
          </ThemeContext.Provider>
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usecontext-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Hooks- useContext
               
               :custom-color-primary-bold:`React Hooks- useContext`, initial context color: :custom-color-green:`green`
            
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usecontext-red.png
               :align: center
               :class: sd-my-0
               :alt: React Hooks- useContext
               
               :custom-color-primary-bold:`React Hooks- useContext`, Click :bdg-secondary-line:`Red` button to change the context color
            

==================================================================================================
useRef
==================================================================================================

The useRef hook in React is commonly used for accessing and interacting with DOM elements or for storing mutable values that do not trigger a re-render when they change. The useRef hook helps ensure that the component works smoothly with both React’s Virtual DOM and the HTML DOM. 
    
    - Accessing DOM Elements: You can use useRef to directly reference a DOM element and interact with it (e.g., focusing an input field).
    - Storing Mutable Values: You can use useRef to store values that persist across renders, but changes to those values do not cause re-renders.
    
How useRef Works with Virtual DOM and HTML DOM
    
    - Persistent Reference: using useRef allows you to interact with the real HTML DOM directly without causing a re-render or needing to store the value in React state.
    - No Re-rendering on Changes: Unlike state (useState), updating the current property of a useRef does not cause the component to re-render. 
    
The signature of useRef is as follows ::
    
    <refObj> = useRef(<val>)
    # val is the initial value to be set for the returned mutable object, refObj.
    # refObj is the object returned by the hook.
    
To automatically attach a DOM object to the refObj, it should be set in ref props of the element as shown below ::
    
    <input ref={refObj} />
    
To access the attached DOM element, use current property of the refObj as shown below ::
    
    const refElement = refObj.current
    
Use cases of useRef
    
    - Accessing JavaScript DOM API
        
        - Focusing an input element
        - Selecting text
        - play audio or video using media playback API
        
    - Imperative animation − Web Animation API provides a rich set of animation feature through imperative programming rather than declarative programming. To use Web animation API, we need access to the raw DOM.
    - Integration with third party library − Since third party library requires access to raw DOM to do its functionality, it is be mandatory to use useRef to get the DOM reference from react and provide it to third party library.
    

- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Create the file ``./UseRefComponent.js`` ::
    
    import React, {useState, useRef} from 'react';
    import './App.css';
    
    function UseRefComponent () {
      const [inputVal, setInputVal] = useState ('');
      const inputRef = useRef (null);
      const labelRef = useRef(null);
    
      const handleInputChange = () => {
        labelRef.current.innerText=inputRef.current.value;
      };
      const handleClick = () => {
        setInputVal (inputRef.current.value);
      };
      return (
        <div>
          <h2>React Hooks- useRef</h2>
          <p>
            <input ref={inputRef} type="text" placeholder="Enter input field data" onChange={handleInputChange } />
          </p>
          <div>
            <button onClick={() => handleClick ('red')}>Update</button>
          </div>
          <div style={{ marginTop: '10px' }}>
            Input Value in HTML DOM: <span  style={{ color: 'red' }} ref={labelRef } ></span>
          </div>
          <div style={{ marginTop: '10px' }}>
              Input Value in react Virtual DOM: <span  style={{ color: 'red' }}>{inputVal}</span>
          </div>
        </div>
      );
    }
    
    export default UseRefComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import UseRefComponent from './UseRefComponent';
    
    function App() {
      return (
        <div className='App'>
          <UseRefComponent />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-useref-input-dom.png
               :align: center
               :class: sd-mb-1
               :alt: React Hooks - useRef
               
               :custom-color-primary-bold:`React Hooks - useRef`, auto update useRef label when the input changes
            
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-useref-input-react-dom.png
               :align: center
               :class: sd-my-0
               :alt: React Hooks - useRef
               
               :custom-color-primary-bold:`React Hooks - useRef`, Click :bdg-secondary-line:`Update` button to update the inputVal state
            

==================================================================================================
useReducer
==================================================================================================

The useReducer hook in React is a powerful alternative to useState for managing complex state logic. It is often used when the state updates depend on previous states or involve multiple sub-values. Essentially, it allows you to handle state transitions in a more structured way, similar to how Redux works, but at the component level.

The useReducer hook is particularly useful when:
    
    - The state logic is complex (e.g., multiple state variables or conditionally updating state).
    - You need to manage actions (e.g., incrementing, decrementing, resetting a value) in a predictable way.
    - You want to keep state logic separate from the component logic.
    

The useReducer hook accepts a reducer function along with the initial value and returns a dispatcher function. Reducer function will accept the initial state and an action (specific scenario) and then provides logic to update the state based on the action. The dispatcher function accepts the action (and corresponding details) and call the reducer function with provided action. ::
    
    const [<state>, <dispatch function>] = useReducer(<reducer function>, <initial argument>, <init function>);
    # const [state, dispatch] = useReducer(reducer, initialState);
    #     reducer: A function that takes the current state and an action as arguments and returns the new state.
    #     initialState: The initial state for the reducer.
    #     state: The information to be maintained in the state
    

- Move inside the ReactJS App/src folder <tut09-react-hooks/src> ::
    
    cd tut09-react-hooks/src
    
- Create the file ``./UseReducerComponent.js`` ::
    
    import React, { useReducer } from 'react';
    
    const UseReducerComponent = () => {
      // Reducer function that determines how the state changes
      const countReducerFunction = (state, action) => {
        switch (action.type) {
          case 'increment':
            return { ...state, count: state.count + 1, color: 'red' };
          case 'decrement':
            return { ...state, count: state.count - 1, color: 'green' };
          case 'reset':
            return { ...state, count: 0 , color: 'blue' };
          default:
            return state;
        }
      };
      // Using useReducer to manage state
      const [state, dispatch] = useReducer(countReducerFunction, { count: 0 , color: 'black'});
      const handleClick=(type)=>{
        dispatch({ type: type });
      }
      return (
        <div>
          <h2>React Hooks- useReducer</h2>
          <p>
            Count: <span style={{color: state.color, fontWeight: 'bold' }}> {state.count} </span> 
          </p>
          <p>
            <button onClick={() => handleClick('increment') }>Increment</button>
            <button style={{marginLeft: '10px'}} onClick={() => handleClick('decrement') }>Decrement</button>
            <button style={{marginLeft: '10px'}} onClick={() => handleClick('reset') }>Reset</button>
          </p>
        </div>
      );
    };
    
    export default UseReducerComponent;
    
- Edit the file ``App.js`` ::
    
    import UseReducerComponent from './UseReducerComponent';
    import './App.css';
    
    
    function App() {
      return (
        <div className='App'>
          <UseReducerComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usereducer-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Hooks - useReducer
               
               :custom-color-primary-bold:`React Hooks - useReducer`, state with initial values: {count: 0, color: :custom-color-black:`black` }
            
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usereducer-increment.png
               :align: center
               :class: sd-my-0
               :alt: React Hooks - useReducer
               
               :custom-color-primary-bold:`React Hooks - useReducer`, Click :bdg-secondary-line:`Increment` button to update the state { count: xxx, color: :custom-color-red:`red` }
            
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usereducer-decrement.png
               :align: center
               :class: sd-mb-1
               :alt: React Hooks - useReducer
               
               :custom-color-primary-bold:`React Hooks - useReducer`, Click :bdg-secondary-line:`Decrement` button to update the state { count: xxx, color: :custom-color-green:`green` }
            
        .. grid-item::
            
            .. figure:: images/tut09/tut09-react-hooks-usereducer-reset.png
               :align: center
               :class: sd-my-0
               :alt: React Hooks - useReducer
               
               :custom-color-primary-bold:`React Hooks - useReducer`, Click :bdg-secondary-line:`Reset` button to update the state { count: 0, color: :custom-color-primary:`blue` }
               
               