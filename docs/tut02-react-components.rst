.. _tut02-react-components:

.. rst-class:: title-center h1
   
React Components

##################################################################################################
Tut02-React Components
##################################################################################################

There are two types of components in React: 
    - Function Components
    - Class Components
    

**************************************************************************************************
Create a ReactJS App <tut02-react-components>
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut02-react-components>::
    
    npx create-react-app tut02-react-components
    
- Move inside the ReactJS App/src folder <tut02-react-components/src>::
    
    cd tut02-react-components/src
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut02-react-components>::
    
    npm run start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Function Components
**************************************************************************************************

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
    
    .. figure:: images/tut02-react-components-function.png
        :align: center
        :class: sd-mb-2
        :alt: Hello ReactJS App
        :width: 80%
        
**************************************************************************************************
Class Components
**************************************************************************************************

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
    
    .. figure:: images/tut02-react-components-class.png
        :align: center
        :class: sd-mb-2
        :alt: Hello ReactJS App
        :width: 80%
        