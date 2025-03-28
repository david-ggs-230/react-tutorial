.. _tut03-react-props:

.. rst-class:: title-center h1
   
React Props

##################################################################################################
Tut03-React Props
##################################################################################################

Every component can have attributes similar to HTML attributes and each attribute's value can be accessed inside the component using properties (props). Props are used to pass data between components. 
    
    - ReactJS Props
    - ReactJS Props Validation
    
React properties supports attribute's value of different types. They are as follows: 
    
    - String
    - Number
    - Datetime
    - Array
    - List
    - Objects
    

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut03-react-props>::
    
    yarn create react-app tut03-react-props
    
- Move inside the ReactJS App/src folder <tut03-react-props/src>::
    
    cd tut03-react-props/src
    
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
- Run the ReactJS App <tut03-react-props>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Passing Props to Components
**************************************************************************************************

==================================================================================================
Passing Props to Function Components
==================================================================================================

React components use props to communicate with each other. Every parent component can pass some information to its child components by giving them props. Props might remind you of HTML attributes, but you can pass any JavaScript value through them, including objects, arrays, and functions.

    - Create a parent component <App />
    - Create a child component <Person />
    - Parent component pass some information to its child components by giving them props

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut03-react-props/src>::
    
    cd tut03-react-props/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import './App.css';
    
    function Person(props) {
      return (
        <div className="App">
            <h2>{props.name}</h2>
            <p>Age: {props.age}</p>
            <p>Location: {props.location}</p>
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
          <h1>Hello, Function-Component Props!</h1>
          <Person name='Mary' age='25' location='New York' />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut03/tut03-react-props-function-component.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        
    
==================================================================================================
Passing Props to Class Components
==================================================================================================

Every component can have attributes similar to HTML attributes and each attribute's value can be accessed inside the component using properties (props).

For example, Hello component with a name attribute can be accessed inside the component through this.props.name variable ::
    
    <Hello name="React" />
    // value of name will be "React"
    // accessed inside the component through props.name
    

When we need immutable data in our component, we can just add props to render() function inside the Class Component.

    - Create a parent component <App />
    - Create a child component <Person />
    - Parent component pass some information to its child components by giving them props

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut03-react-props/src>::
    
    cd tut03-react-props/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import React, { Component } from 'react';
    import './App.css';
    
    class Person extends Component {
        render() {
            return (
              <div className="App">
                <h2>{this.props.name}</h2>
                <p>Age: {this.props.age}</p>
                <p>Location: {this.props.location}</p>
              </div>
            );
        }
    }
    
    export default Person;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import React, { Component } from 'react';
    import './App.css';
    import Person from './Person';
    
    class App extends Component {
        render() {
            return (
              <div className="App">
                  <h1>Hello, Class-Component Props!</h1>
                  <Person name='Kate' age='23' location='New Haven' />
              </div>
            );
        }
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut03/tut03-react-props-class-component.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        

**************************************************************************************************
Setting Default Props to Components
**************************************************************************************************

==================================================================================================
Setting Default Props to Function Components
==================================================================================================

    - Create a parent component <App />
    - Create a child component <Person />
    - Parent component pass some information to its child components by giving them props

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut03-react-props/src>::
    
    cd tut03-react-props/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import './App.css';
    
    function Person({name='Nancy', age='19',location='Houston'}) {
      return (
        <div className="App">
            <h2>{name}</h2>
            <p>Age: {age}</p>
            <p>Location: {location}</p>
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
          <h1>Hello, Function-Component Props!</h1>
          <Person name='Lucy'/>
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut03/tut03-react-props-function-component-default.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        
==================================================================================================
Setting Default Props to Class Components
==================================================================================================

    - Create a parent component <App />
    - Create a child component <Person />
    - Parent component pass some information to its child components by giving them props

**Step-by-Step Tutorial**

- Move inside the ReactJS App/src folder <tut03-react-props/src>::
    
    cd tut03-react-props/src
    
- Create the file ``Person.js`` (Child Component)::
    
    import React, { Component } from 'react';
    import './App.css';
    
    class Person extends Component {
        render() {
            return (
              <div className="App">
                <h2>{this.props.name}</h2>
                <p>Age: {this.props.age}</p>
                <p>Location: {this.props.location}</p>
              </div>
            );
        }
    }
    
    Person.defaultProps = {
        name: "Default Name",
        age:"Default Age",
        location:"Default Location"
    }
    
    export default Person;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import React, { Component } from 'react';
    import './App.css';
    import Person from './Person';
    
    class App extends Component {
        render() {
            return (
              <div className="App">
                  <h1>Hello, Class-Component Props!</h1>
                  <Person name='Peter' />
              </div>
            );
        }
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut03/tut03-react-props-class-component-default.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        