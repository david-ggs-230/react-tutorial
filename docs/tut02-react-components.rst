.. _tut02-react-components:

.. rst-class:: title-center h1
   
React Components

##################################################################################################
Tut02-React Components
##################################################################################################

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut02-react-components>::
    
    npx create-react-app tut02-react-components
    
- Move inside the ReactJS App/src folder <tut02-react-components/src>::
    
    cd tut02-react-components/src
    
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
- Run the ReactJS App <tut02-react-components>::
    
    npm run start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
React Components
**************************************************************************************************

There are two types of components in React: 
    - Function Components
    - Class Components
    

==================================================================================================
Function Components
==================================================================================================

Functional Components:
    - They are JavaScript functions that return React elements.
    - Stateless or Stateful: Can manage state using React Hooks.
    - Simpler Syntax: Ideal for small and reusable components.
    - Performance: Generally faster since they don’t require a ‘this’ keyword.

- Move inside the ReactJS App/src folder <tut02-react-components/src>::
    
    cd tut02-react-components/src
    
- Edit the file ``App.js``::
    
    import './App.css';
    
    function App() {
      return (
        <div className="App">
            <h1>Hello, My React-Function-Component App!</h1>
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut02/tut02-react-components-function.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        

==================================================================================================
Class Components
==================================================================================================

Class Components:
    - Class components are ES6 classes that extend React.Component. 
    - Include features like state management and lifecycle methods.
        
        - State Management: State is managed using the this.state property.
        - Lifecycle Methods: Includes methods like componentDidMount, componentDidUpdate, etc.

- Move inside the ReactJS App/src folder <tut02-react-components/src>::
    
    cd tut02-react-components/src
    
- Edit the file ``App.js``::
    
    import React, { Component } from 'react';
    import './App.css';
    
    class App extends React.Component {
        render() {
            return (
              <div className="App">
                  <h1>Hello, My React-Class-Component App!</h1>
              </div>
            );
        }
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut02/tut02-react-components-class.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        

**************************************************************************************************
React Nested Components
**************************************************************************************************

A nested component in React is a component that is related to an another component. You can also consider it as a child component inside a parent component; but they are not linked together using the inheritance concept but with the composition concept. 

    - Create a parent component <App />
    - Create a child component <Person />
    - Parent component <App /> contains child components <Person />


**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut02-react-components/src>::
    
    cd tut02-react-components/src
    
- Create the file ``Person1.js`` (Child Component)::
    
    import './App.css';
    
    function Person1() {
      return (
        <li className="App">
            <h2>Nancy</h2>
            <p>Age: 25</p>
            <p>Location: New York</p>
        </li>
      );
    }
    
    export default Person1;
    
- Create the file ``Person2.js`` (Child Component)::
    
    import React, { Component } from 'react';
    import './App.css';
    
    class Person2 extends Component {
        render() {
            return (
              <li className="App">
                <h2>Alan Boyer</h2>
                <p>Age: 35</p>
                <p>Location: Boston</p>
              </li>
            );
        }
    }
    
    export default Person2;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import React, { Component } from 'react';
    import Person1 from './Person1';
    import Person2 from './Person2';
    
    class App extends Component {
      render() {
          return (
            <div className="App">
                <h1>Hello, My React-Components App!</h1>
                <ol>
                  <Person1 />
                  <Person2 />
                </ol>
            </div>
          );
      }
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut02/tut02-react-components-nested.png
        :align: center
        :class: sd-mb-2
        :width: 80%
    