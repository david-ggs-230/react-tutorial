.. _tut06-react-component-life-cycle:

.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold


.. rst-class:: title-center h1
   
React Component Life Cycle

##################################################################################################
Tut06-React Component Life Cycle
##################################################################################################

Each React component has three distinct stages:
    
    - Mounting − Mounting represents the rendering of the React component in the given DOM node.
        
        - constructor()
            
            Invoked during the initial construction phase of the React component. Used to set initial state and properties of the component.
            
        - getDerivedStateFromProps()
            
            Invoked during both initial and update phase and just before the render() method. It is mostly used in animation context where the various state of the component is needed to do smooth animation. The signature of the API is: :custom-color-primary-bold:`static getDerivedStateFromProps(props, state)`
                
                - props − current properties of the component
                - state − Current state of the component
                
            
        - render()
            
            It renders the component in the virtual DOM instance. This is specified as mounting of the component in the DOM tree.
            
        - componentDidMount()
            
            Invoked after the initial mounting of the component in the DOM tree.
            
        
    - Updating − Updating represents the re-rendering of the React component in the given DOM node during state changes / updates.
        
        - shouldComponentUpdate()
            
            Invoked during the update phase. Used to specify whether the component should update or not. The signature of the API is: :custom-color-primary-bold:`shouldComponentUpdate(nextProps, nextState)`
                
                - nextProps − Upcoming properties of the component
                - nextState − Upcoming state of the component
                
            
        - getDerivedStateFromProps()
            
            Invoked during both initial and update phase and just before the render() method. It is mostly used in animation context where the various state of the component is needed to do smooth animation. The signature of the API is: :custom-color-primary-bold:`static getDerivedStateFromProps(props, state)`
                
                - props − current properties of the component
                - state − Current state of the component
                
            
        - render()
            
            It renders the component in the virtual DOM instance. 
            
        - getSnapshotBeforeUpdate()
            
            Invoked just before the rendered content is commited to DOM tree. The data returned by this method will be passed to ComponentDidUpdate() method. The signature of the API is: :custom-color-primary-bold:`getSnapshotBeforeUpdate(prevProps, prevState)`
                
                - prevProps − Previous properties of the component.
                - prevState − Previous state of the component.
                
            
            
        - componentDidUpdate()
            
            Invoked during the update phase. The signature of the API is: :custom-color-primary-bold:`componentDidUpdate(prevProps, prevState, snapshot)`
                
                - prevProps − Previous properties of the component.
                - prevState − Previous state of the component.
                - snapshot − Current rendered content.
                
            
        
    - Unmounting − Unmounting represents the removal of the React component.
        
        - componentWillUnmount() 
            
            Invoked after the component is unmounted from the DOM. This is the good place to clean up the object.
            
        

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut06-react-component-life-cycle>::
    
    yarn create react-app tut06-react-component-life-cycle
    
- Move inside the ReactJS App/src folder <tut06-react-component-life-cycle/src>::
    
    cd tut06-react-component-life-cycle/src
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //Disable test
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut06-react-component-life-cycle>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Component Life Cycle Management
**************************************************************************************************

Here’s an example of a ReactJS component showing component life cycle stages
    
    - Showing life cycle stages
    - State: {count: number}, record button click count
    - Button click, update state {count}
    
Structure:
    
    - Create a parent component <App />
    - Create a child component <LifeCycleManagementComponent />
    - Child component update information when button is clicked
    
==================================================================================================
Life Cycle Management in Class Component
==================================================================================================

- Move inside the ReactJS App/src folder <tut06-react-component-life-cycle/src>::
    
    cd tut06-react-component-life-cycle/src
    
- Create the file ``LifeCycleManagementComponent.js`` (Child Component) ::
    
    import React, {Component} from 'react';
    import './App.css';
    
    class LifeCycleManagementComponent extends Component {
      static logMessages = [];
      /* Life Cycle Stage
          - Mounting
            - constructor()
            - getDerivedStateFromProps()
            - render()
            - componentDidMount()
        - Updating
            - shouldComponentUpdate()
            - getDerivedStateFromProps()
            - render()
            - getSnapshotBeforeUpdate()
            - componentDidUpdate()
        - Unmounting
            - componentWillUnmount()
      */
      constructor (props) {
        super (props);
        // Initialize state with a list of messages
        this.state = {count: 0, messages: []};
        LifeCycleManagementComponent.logMessages.push ('constructor ();');
      }
      static getDerivedStateFromProps = (props, state) => {
        LifeCycleManagementComponent.logMessages.push (
          'getDerivedStateFromProps();'
        );
        return null;
      };
      componentDidMount = () => {
        LifeCycleManagementComponent.logMessages.push ('componentDidMount();');
      };
    
      shouldComponentUpdate = (nextProps, nextState) => {
        LifeCycleManagementComponent.logMessages.push ('shouldComponentUpdate();');
        return true;
      };
      getSnapshotBeforeUpdate (prevProps, prevState) {
        LifeCycleManagementComponent.logMessages.push (
          'getSnapshotBeforeUpdate();'
        );
        return null;
      }
      componentDidUpdate = (prevProps, prevState, snapshot) => {
        LifeCycleManagementComponent.logMessages.push ('componentDidUpdate();');
      };
      componentWillUnmount = () => {
        LifeCycleManagementComponent.logMessages.push ('componentWillUnmount ();');
      };
      // Event handler for button click
      // class property, using lambda function to define event handler. autobind.
      handleButtonClick = () => {
        this.setState (prevState => ({
          count: prevState.count + 1,
          messages: [...prevState.messages, 'Button was clicked!'],
        }));
      };
    
      render () {
        LifeCycleManagementComponent.logMessages.push ('render ();');
        return (
          <div>
            <h4>Life Cycle Management (Class Component)</h4>
            {/* Button that triggers button click handler */}
            <button onClick={this.handleButtonClick}>INCREMENT</button>
    
            <div className="App">
              <h5>LogMessages</h5>
              {/* Display the list of messages */}
              <p>Count: {this.state.count} </p>
              <h5>Life Cycle Stages</h5>
              <ul>
                {LifeCycleManagementComponent.logMessages.map ((message, index) => (
                  <li key={index}>{message}</li>
                ))}
              </ul>
            </div>
          </div>
        );
      }
    }
    
    export default LifeCycleManagementComponent;
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import LifeCycleManagementComponent from './LifeCycleManagementComponent';
    
    function App () {
      return (
        <div className="App">
          <LifeCycleManagementComponent />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. figure:: images/tut06/tut06-react-class-component-life-cycle.png
       :align: center
       :class: sd-my-2
       :alt: React Component Life Cycle (Class Component)
       
       :custom-color-primary-bold:`React Component Life Cycle (Class Component)`, Click :bdg-secondary-line:`INCREMENT` to update state
    

==================================================================================================
Life Cycle Management in Function Component
==================================================================================================

In React functional components, lifecycle methods from class components do not have a direct equivalent, but similar behavior can be achieved using the useEffect hook. 

- componentDidMount: In class components, componentDidMount is called once the component is mounted (i.e., after the component is rendered to the screen).
    
    - In functional components, you can use useEffect with an empty dependency array ([]) to replicate this behavior. This ensures the effect runs only once when the component mounts. ::
        
        useEffect(() => {
          // This runs once, after the component mounts
          console.log("Component mounted");
        }, []); // Empty array means it runs only once
        
- componentDidUpdate: In class components, componentDidUpdate is called after every update, i.e., whenever the component re-renders due to a change in state or props.
    
    - In functional components, you can achieve this using useEffect with specific dependencies. The effect will run whenever any of the dependencies change. ::
        
        useEffect(() => {
          // This runs after every update (re-render)
          console.log("Component updated");
        }, [count]); // Runs whenever 'count' changes
        
- componentWillUnmount: In class components, componentWillUnmount is called right before a component is unmounted and destroyed.
    
    - In functional components, you can achieve this behavior by returning a cleanup function from the useEffect hook. This cleanup function will run when the component unmounts. ::
        
        useEffect(() => {
          // This is the effect setup code
          return () => {
              // This cleanup code runs when the component unmounts
              console.log("Component will unmount");
          };
        }, []); // Empty array means the effect runs once (on mount) and cleanup runs on unmount
        
- getDerivedStateFromProps: This method is used in class components to update state based on props changes.
    
    - In functional components, you generally manage state changes directly with useState, and you can conditionally update the state based on props or any other factors. ::
        
        function MyComponent({ propValue }) {
          const [stateValue, setStateValue] = useState(propValue);
        
          useEffect(() => {
            // Similar to getDerivedStateFromProps
            setStateValue(propValue);
          }, [propValue]); // Only updates when 'propValue' changes
        
          return <div>{stateValue}</div>;
        }
        
- shouldComponentUpdate: In class components, shouldComponentUpdate() is used to determine whether a component should re-render when its props or state change. It returns a boolean value (true to re-render, false to prevent re-render).
    
    - In React functional components, there is no direct equivalent to the shouldComponentUpdate() lifecycle method that exists in class components. However, you can achieve similar behavior by using React.memo and the useEffect hook. ::
        
        import React, { useState } from 'react';
        
        const MyComponent = React.memo(({ count }) => {
          console.log('Rendering MyComponent');
          return <div>{count}</div>;
        }, (prevProps, nextProps) => {
          // Only re-render if 'count' prop changes
          return prevProps.count === nextProps.count;
          // Return true if props are equal and re-render should be prevented
          // Return false if props are different and re-render should occur
        });
        
        export default MyComponent;
        
    - In the example above:
        
        - React.memo wraps the functional component.
        - The second argument to React.memo is a function that compares the previous and next props. If the function returns true, the component will not re-render. If it returns false, the component will re-render.
        

- Move inside the ReactJS App/src folder <tut06-react-component-life-cycle/src> ::
    
    cd tut06-react-component-life-cycle/src
    
- Create the file ``LifeCycleManagementComponent.js`` (Child Component) ::
    
    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function LifeCycleManagementComponent (props) {
      const [count, setCount] = useState (0);
    
      if (typeof LifeCycleManagementComponent.logMessages == 'undefined') {
        LifeCycleManagementComponent.logMessages = [];
      }
    
      // This will run once when the component is first mounted
      useEffect (() => {
        LifeCycleManagementComponent.logMessages.push ('Component mounted');
        return () => {
          // Cleanup function - equivalent to componentWillUnmount
          LifeCycleManagementComponent.logMessages.push ('Component unmounted');
        };
      }, []); // Empty dependency array to run only once on initial render
      // Equivalent to componentDidMount and componentDidUpdate
      useEffect (
        () => {
          // This will run after the component mounts and every time `count` changes
          LifeCycleManagementComponent.logMessages.push ('Component mounted or updated, count is:' + count);
          // Cleanup function - equivalent to componentWillUnmount
          return () => {
            // Cleanup function - equivalent to componentWillUnmount
            LifeCycleManagementComponent.logMessages.push ('Cleanup for count:' + count);
          };
      },[count]); // The effect depends on the `count` state
    
      const handleButtonClick = () => {
        setCount (preCount => preCount + 1);
      };
      return (
        <div>
          <h4>Life Cycle Management (Function Component)</h4>
          {/* Button that triggers button click handler */}
          <button onClick={() => handleButtonClick ()}>INCREMENT</button>
    
          <div className="App">
            <h5>LogMessages</h5>
            {/* Display the list of messages */}
            <p>Count: {count} </p>
            <h5>Life Cycle Stages</h5>
            <ul>
              {LifeCycleManagementComponent.logMessages.map ((message, index) => (
                <li key={index}>{message}</li>
              ))}
            </ul>
          </div>
        </div>
      );
    }
    
    export default LifeCycleManagementComponent;
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import LifeCycleManagementComponent from './LifeCycleManagementComponent';
    
    function App () {
      return (
        <div className="App">
          <LifeCycleManagementComponent />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. figure:: images/tut06/tut06-react-function-component-life-cycle.png
       :align: center
       :class: sd-my-2
       :alt: React Component Life Cycle (Function Component)
       
       :custom-color-primary-bold:`React Component Life Cycle (Function Component)`, Click :bdg-secondary-line:`INCREMENT` to update state
    

