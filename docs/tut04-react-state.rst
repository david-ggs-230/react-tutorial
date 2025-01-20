.. _tut04-react-state:

.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold


.. rst-class:: title-center h1
   
React State

##################################################################################################
Tut04-React State
##################################################################################################

State represents the value of a dynamic properties of a React component at a given instance. React provides a dynamic data store for each component. The internal data represents the state of a React component and can be accessed using this.state member variable of the component. Whenever the state of the component is changed, the component will re-render itself by calling the render() method along with the new state.

React component maintains and expose it's state through this.state of the component. React provides a single API to maintain state in the component. The API is this.setState(). It accepts either a JavaScript object or a function that returns a JavaScript object.

setState() is used to update a component's state object. This is done by scheduling an update to that component's state object. So, when the state changes, this component responds by re-rendering.

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut04-react-state>::
    
    yarn create react-app tut04-react-state
    
- Move inside the ReactJS App/src folder <tut04-react-state/src>::
    
    cd tut04-react-state/src
    
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
- Run the ReactJS App <tut04-react-state>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
State Management
**************************************************************************************************

==================================================================================================
State Management of Class Component
==================================================================================================

React components have a built-in state object. The state object is used to store all the property values that belong to the component in which this state is defined. When the state object changes, the component re-renders.

    - Create a parent component <App />
    - Create a child component <Person />
    - Child component update information when button is clicked

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut04-react-state/src>::
    
    cd tut04-react-state/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import React, { Component } from 'react'
    import './App.css'
    class Person extends Component {
      constructor (props) {
        super(props)
        this.state = { name: 'Nancy', age: '19', location: 'New York' }
      }
      changeUserHandler = () => {
        this.setState(prevState =>
          prevState.name === 'Nancy'
            ? { name: 'Bob', age: '37', location: 'Boston' }
            : { name: 'Nancy', age: '19', location: 'New York' }
        )
      }
      render () {
        return (
          <div>
            <div className='App'>
              <h2>{this.state.name}</h2>
              <p>Age: {this.state.age}</p>
              <p>Location: {this.state.location}</p>
            </div>
            <div className='App'>
              <button onClick={this.changeUserHandler}>Change User</button>
            </div>
          </div>
        )
      }
    }
    
    export default Person;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import Person from './Person';
    
    function App() {
      return (
        <div className="App">
            <h1>Class-Component State!</h1>
            <Person />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut04/tut04-react-state-class-component-01.png
               :align: center
               :class: sd-mb-1
               :alt: User State 1
               
               :custom-color-primary-bold:`User State 1`, Click :bdg-secondary-line:`Change User` to toggle
            
        .. grid-item::
            
            .. figure:: images/tut04/tut04-react-state-class-component-02.png
               :align: center
               :class: sd-my-0
               :alt: User State 2
               
               :custom-color-primary-bold:`User State 2`, Click :bdg-secondary-line:`Change User` to toggle
            
    

==================================================================================================
State Management of Function Component
==================================================================================================

React Hooks are special functions provided by React to handle a specific functionality inside a React functional component. React provides a Hook function for every supported feature. For example, React provides useState() function to manage state in a functional component. When a React functional component uses React Hooks, React Hooks attach itself into the component and provides additional functionality.

The general signature of useState() Hook is as follows ::
    
    const [<state variable>, <state update function>] = useState(<initial value>);
    
Example App Structure:
    
    - Create a parent component <App />
    - Create a child component <Person />
    - Child component update information when button is clicked

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut04-react-state/src>::
    
    cd tut04-react-state/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import './App.css';
    import React, { useState } from 'react';
    
    function Person(props) {
    
        const [user, setUser] = useState({name:'Nancy', age:'19',location:'Houston'});
    
        const changeUserHandler = () => {
              user.name === 'Nancy'
                ? setUser({ name: 'Bob', age: '37', location: 'Boston' })
                : setUser({ name: 'Nancy', age: '19', location: 'New York' })
        }
    
        return (
            <div>
                <div className='App'>
                    <h2>{user.name}</h2>
                    <p>Age: {user.age}</p>
                    <p>Location: {user.location}</p>
                </div>
                <div className='App'>
                    <button onClick={changeUserHandler}>Change User</button>
                </div>
            </div>
        );
    }
    
    export default Person;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import Person from './Person';
    
    function App() {
      return (
        <div className="App">
            <h1>Function-Component State!</h1>
            <Person />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut04/tut04-react-state-function-component-01.png
               :align: center
               :class: sd-mb-1
               :alt: User State 1
               
               :custom-color-primary-bold:`User State 1`, Click :bdg-secondary-line:`Change User` to toggle
            
        .. grid-item::
            
            .. figure:: images/tut04/tut04-react-state-function-component-02.png
               :align: center
               :class: sd-my-0
               :alt: User State 2
               
               :custom-color-primary-bold:`User State 2`, Click :bdg-secondary-line:`Change User` to toggle
            
    

**************************************************************************************************
State Management Example - A Digital Clock
**************************************************************************************************

    - Create a parent component <App />
    - Create a child function component <Clock1 />
    - Create a child class component <Clock2 />
    - Child components update current-time automatically

==================================================================================================
Create Clock App Structure
==================================================================================================

- Move inside a project folder
- Create React App <tut04-react-state-clock>::
    
    yarn create react-app tut04-react-state-clock
    
- Move inside the ReactJS App/src folder <tut04-react-state-clock/src>::
    
    cd tut04-react-state-clock/src
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //Disable test
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- Run the ReactJS App <tut04-react-state>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

==================================================================================================
Create Clock Component
==================================================================================================

- Move inside the ReactJS App/src folder <tut04-react-state-clock/src>::
    
    cd tut04-react-state-clock/src
    
- Create the file ``Clock1.js`` (Child Function Component)::
    
    import './App.css';
    import React, {useState, useEffect} from 'react';
    
    function Clock1 (props) {
      const [datetime, setDatetime] = useState (new Date ());
      useEffect (() => {
        const intervalId = setInterval (() => {
          setDatetime (new Date ());
        }, 1000);
    
        return () => clearInterval (intervalId);
      }, []);
      return (
        <div className="App">
          <h4>Function-Component Clock</h4>
          <p>DateTime: {datetime.toUTCString ()}</p>
        </div>
      );
    }
    
    export default Clock1;
    
    
- Create the file ``Clock2.js`` (Child Class Component)::
    
    import React, {Component} from 'react';
    import './App.css';
    class Clock2 extends Component {
      constructor (props) {
        super (props);
        this.state = {datetime: new Date ()};
      }
      componentDidMount = () => {
        this.setTimeRef = setInterval (
          () => this.setState ({datetime: new Date ()}),
          1000
        );
      };
    
      componentWillUnmount = () => {
        clearInterval (this.setTimeRef);
      }
      render () {
        return (
          <div className="App">
            <h4>Class-Component Clock</h4>
            <p>DateTime: {this.state.datetime.toUTCString ()}</p>
          </div>
        );
      }
    }
    
    export default Clock2;
    
    

==================================================================================================
Create App Component
==================================================================================================

- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import Clock1 from './Clock1';
    import Clock2 from './Clock2';
    
    function App () {
      return (
        <div className="App">
          <h1>A Digital Clock Example!</h1>
          <Clock1 />
          <Clock2 />
        </div>
      );
    }
    
    export default App;
    
==================================================================================================
Screenshot
==================================================================================================

    
    .. figure:: images/tut04/tut04-react-state-clock-example.png
       :align: center
       :class: sd-mb-1
       :alt: A Digital Clock Example
       
       :custom-color-primary-bold:`A Digital Clock Example`
    

