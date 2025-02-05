.. _tut10-react-form:


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
   
React Form

##################################################################################################
Tut10-React Form
##################################################################################################

The nature of form programming needs the state to be maintained and the input field information will get changed as the user interacts with the form. React provides two types of components to support form programming.
    
    - Controlled component − In controlled component, React provides a special attribute, value for all input elements and controls the input elements. The value attribute can be used to get and set the value of the input element. It has to be in sync with state of the component.
    - Uncontrolled component − In uncontrolled component, React provides minimal support for form programming. It has to use Ref concept (another react concept to get a DOM element in the React component during runtime) to do the form programming.
    
**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut10-react-form> ::
    
    yarn create react-app tut10-react-form
    
- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    //import { render, screen } from '@testing-library/react';
    //import App from './App';
    
    //test('renders learn react link', () => {
      //render(<App />);
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    //});
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut10-react-form> ::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
React Form
**************************************************************************************************

The nature of form programming needs the state to be maintained and the input field information will get changed as the user interacts with the form. React provides two types of components to support form programming.
    
    - Controlled component − In controlled component, React provides a special attribute, value for all input elements and controls the input elements. The value attribute can be used to get and set the value of the input element. It has to be in sync with state of the component.
    - Uncontrolled component − In uncontrolled component, React provides minimal support for form programming. It has to use Ref concept (another react concept to get a DOM element in the React component during runtime) to do the form programming.
    
==================================================================================================
Controlled Component
==================================================================================================

In controlled component, React provides a special attribute, value for all input elements and controls the input elements, and use the useState Hook to keep track of each inputs value. React control the values of more than one input field by adding a name attribute to each element.

The sample usage to set and update the user's form input is as follows ::
    
    const [inputs, setInputs] = useState({});
    
    <input 
        type="text" 
        name="fieldname" 
        value={inputs.fieldname || ""} 
        onChange={handleChange}
    />
    
    // update the state
    const handleChange = (event) => {
      const name = event.target.name;
      const value = event.target.value;
      setInputs(values => ({...values, [name]: value}))
    }
    
    // Handle form submit
    const handleSubmit = (event) => {
      event.preventDefault();
      ...
    }
    
--------------------------------------------------------------------------------------------------
Controlled Form Component
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Create the file ``./ReactFormControlledComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    
    class ReactFormControlledComponent extends React.Component {
      constructor (props) {
        super (props);
        this.state = {name: '', age: '', location: ''};
      }
      changeHandler = e => {
        this.setState (prevState => {
          const name = e.target.name;
          const value = e.target.value;
          return {...prevState, [name]: value};
        });
      };
    
      handleSubmit = e => {
        e.preventDefault ();
        alert (JSON.stringify (this.state));
      };
      render () {
        return (
          <div>
            <div className="App">
              <form onSubmit={e => this.handleSubmit (e)}>
                <div style={{marginTop: 10}}>
                    <label for="name" style={{marginRight: '1.5rem'}}>Name</label>
                    <input
                        type="text"
                        id="name"
                        name="name"
                        placeholder="Enter name"
                        value={this.state.name}
                        onChange={this.changeHandler}
                    />
                </div>
                <div style={{marginTop: 10}}>
                    <label for="age" style={{marginRight: '2.25rem'}}>Age</label>
                    <input
                        type="number"
                        id="age"
                        name="age"
                        placeholder="Enter age"
                        value={this.state.age}
                        onChange={this.changeHandler}
                    />
                </div>
                <div style={{marginTop: 10}}>
                    <label for="location" style={{marginRight: '0.25rem'}}>Location</label>
                    <input
                        type="text"
                        id="location"
                        name="location"
                        placeholder="Enter location"
                        value={this.state.location}
                        onChange={this.changeHandler}
                    />
                </div>
                <div style={{marginTop: 10}}>
                    <input type="submit" value="Submit" />
                </div>
              </form>
            </div>
            <div>
              <h2>Name: {this.state.name}</h2>
              <p>Age: {this.state.age}</p>
              <p>Location: {this.state.location}</p>
            </div>
          </div>
        );
      }
    }
    
    export default ReactFormControlledComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import ReactFormControlledComponent from './ReactFormControlledComponent';
    
    function App() {
      return (
        <div className="App">
            <ReactFormControlledComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-controlled-component-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Form - Controlled Component
               
               :custom-color-primary-bold:`React Form - Controlled Component`, homepage
            
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-controlled-component-input.png
               :align: center
               :class: sd-my-0
               :alt: React Form - Controlled Component
               
               :custom-color-primary-bold:`React Form - Controlled Component`, form input
            
