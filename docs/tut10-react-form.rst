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
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
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
                    <label htmlFor="name" style={{marginRight: '1.5rem'}}>Name</label>
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
                    <label htmlFor="age" style={{marginRight: '2.25rem'}}>Age</label>
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
                    <label htmlFor="location" style={{marginRight: '0.25rem'}}>Location</label>
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
            
    
--------------------------------------------------------------------------------------------------
Controlled Form Child Component
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Create the file ``./ReactFormControlledChildComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    class ReactFormControlledChildComponent extends React.Component {
      render () {
        return (
          <div style={{marginTop: 10}}>
            <label htmlFor={this.props.name} style={{display: 'inline-block', width: '3rem', marginRight: '1.5rem'}}>
              {this.props.label}
            </label>
            <input
              type={this.props.type}
              id={this.props.name}
              name={this.props.name}
              placeholder={this.props.placeholder}
              value={this.props.value}
              onChange={this.props.changeHandler}
            />
          </div>
        );
      }
    }
    
    export default ReactFormControlledChildComponent;
    
- Create the file ``./ReactFormControlledParentComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    import ReactFormControlledChildComponent from './ReactFormControlledChildComponent';
    
    class ReactFormControlledParentComponent extends React.Component {
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
                <ReactFormControlledChildComponent
                  type="text"
                  label="Name"
                  name="name"
                  placeholder="Enter name"
                  value={this.state.name}
                  changeHandler={this.changeHandler}
                />
                <ReactFormControlledChildComponent
                  type="number"
                  label="Age"
                  name="age"
                  placeholder="Enter age"
                  value={this.state.age}
                  changeHandler={this.changeHandler}
                />
                <ReactFormControlledChildComponent
                  type="text"
                  label="Location"
                  name="location"
                  placeholder="Enter location"
                  value={this.state.location}
                  changeHandler={this.changeHandler}
                />
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
    
    export default ReactFormControlledParentComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import ReactFormControlledParentComponent from './ReactFormControlledParentComponent';
    
    function App() {
      return (
        <div className="App">
            <ReactFormControlledParentComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-controlled-child-component-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Form - Controlled Child Component
               
               :custom-color-primary-bold:`React Form - Controlled Child Component`, homepage
            
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-controlled-child-component-input.png
               :align: center
               :class: sd-my-0
               :alt: React Form - Controlled Child Component
               
               :custom-color-primary-bold:`React Form - Controlled Child Component`, form input
            
    
==================================================================================================
Uncontrolled Component
==================================================================================================

In uncontrolled components, React does not manage the state of input elements and doesn't track the value of the input fields. Instead, it allows the DOM to handle the input's state. React provides a ref attribute for all its DOM element and a corresponding api, React.createRef() to create a new reference (this.ref). The newly created reference can be attached to the form element and the attached form element's value can be accessed using this.ref.current.value whenever necessary.

The sample usage to do form programming in uncontrolled component:
    
    - Step 1 − Create a reference ::
        
        this.inputRef = React.createRef();
        
    - Step 2 − Create a form element ::
        
        <input type="text" name="username" />
        
    - Step 3 − Attach the already created reference in the form element ::
        
        <input type="text" name="username" ref={this.inputRef} />
        
    - Step 4 − Get the input value using this.inputRef.current.value during validation and submission ::
        
        <div> input: {this.inputRef.current.value} </div> 
        
    
--------------------------------------------------------------------------------------------------
Uncontrolled Form Component
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Create the file ``./ReactFormUncontrolledComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    class ReactFormUncontrolledComponent extends React.Component {
      constructor (props) {
        super (props);
        //this.nameInputRef = React.createRef();
        //this.ageInputRef = React.createRef();
        //this.locationInputRef = React.createRef();
        this.labelNameRef = React.createRef();
        this.labelAgeRef = React.createRef();
        this.labelLocationRef = React.createRef();
      }
    
      handleSubmit = e => {
        e.preventDefault ();
        alert (JSON.stringify ({name:this.labelNameRef.current.innerText, 
                      age:this.labelAgeRef.current.innerText, 
                      location:this.labelLocationRef.current.innerText }));
      };
    
      handleChange = (e) => {
        let name=e.target.name;
        if(name === 'name') {
          this.labelNameRef.current.innerText=e.target.value;
        }else if(name === 'age'){
          this.labelAgeRef.current.innerText=e.target.value;  
        }else if(name === 'location'){
          this.labelLocationRef.current.innerText=e.target.value;  
        }
      };
    
      render () {
        return (
          <div>
            <div className="App">
              <form onSubmit={e => this.handleSubmit (e)}>
                <div style={{marginTop: 10}}>
                  <label htmlFor='name' style={{display: 'inline-block', width: '3rem', marginRight: '1.5rem'}}>
                    Name
                  </label>
                  <input
                    type='text'
                    id='name'
                    name='name'
                    placeholder='Enter name'
                    //ref={this.nameInputRef}
                    onChange={this.handleChange}
                  />
                </div>
                <div style={{marginTop: 10}}>
                  <label htmlFor='age' style={{display: 'inline-block', width: '3rem', marginRight: '1.5rem'}}>
                    Age
                  </label>
                  <input
                    type='number'
                    id='age'
                    name='age'
                    placeholder='Enter age'
                    //ref={this.ageInputRef}
                    onChange={this.handleChange}
                  />
                </div>
                <div style={{marginTop: 10}}>
                  <label htmlFor='location' style={{display: 'inline-block', width: '3rem', marginRight: '1.5rem'}}>
                    Location
                  </label>
                  <input
                    type='text'
                    id='location'
                    name='location'
                    placeholder='Enter location'
                    //ref={this.locationInputRef}
                    onChange={this.handleChange}
                  />
                </div>
                <div style={{marginTop: 10}}>
                    <input type="submit" value="Submit" />
                </div>
              </form>
            </div>
            <div>
              <h2>Name: <span ref={this.labelNameRef}></span></h2>
              <p>Age: <span ref={this.labelAgeRef}></span></p>
              <p>Location: <span ref={this.labelLocationRef}></span></p>
            </div>
          </div>
        );
      }
    }
    
    export default ReactFormUncontrolledComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import ReactFormUncontrolledComponent from './ReactFormUncontrolledComponent';
    
    function App() {
      return (
        <div className="App">
            <ReactFormUncontrolledComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-uncontrolled-component-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Form - Uncontrolled Component
               
               :custom-color-primary-bold:`React Form - Uncontrolled Component`, homepage
            
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-uncontrolled-component-input.png
               :align: center
               :class: sd-my-0
               :alt: React Form - Uncontrolled Component
               
               :custom-color-primary-bold:`React Form - Uncontrolled Component`, form input
            
    
--------------------------------------------------------------------------------------------------
Uncontrolled Form Child Component
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Create the file ``./ReactFormUncontrolledChildComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    class ReactFormUncontrolledChildComponent extends React.Component {
      render () {
        return (
          <div style={{marginTop: 10}}>
            <label htmlFor={this.props.name} style={{display: 'inline-block', width: '3rem', marginRight: '1.5rem'}}>
              {this.props.label}
            </label>
            <input
              type={this.props.type}
              id={this.props.name}
              name={this.props.name}
              placeholder={this.props.placeholder}
              onChange={this.props.changeHandler}
              ref={this.props.ref}
            />
          </div>
        );
      }
    }
    
    export default ReactFormUncontrolledChildComponent;
    
- Create the file ``./ReactFormUncontrolledParentComponent.js`` ::
    
    import React from 'react';
    import './App.css';
    import ReactFormUncontrolledChildComponent from './ReactFormUncontrolledChildComponent';
    
    class ReactFormUncontrolledParentComponent extends React.Component {
      constructor (props) {
        super (props);
        this.nameInputRef = React.createRef();
        this.ageInputRef = React.createRef();
        this.locationInputRef = React.createRef();
        this.labelNameRef = React.createRef();
        this.labelAgeRef = React.createRef();
        this.labelLocationRef = React.createRef();
      }
    
      changeHandler = e => {
        let name=e.target.name;
        if(name === 'name') {
          this.labelNameRef.current.innerText=e.target.value;
        }else if(name === 'age'){
          this.labelAgeRef.current.innerText=e.target.value;  
        }else if(name === 'location'){
          this.labelLocationRef.current.innerText=e.target.value;  
        }
      };
      handleSubmit = e => {
        e.preventDefault ();
        alert (JSON.stringify ({name:this.labelNameRef.current.innerText, 
              age:this.labelAgeRef.current.innerText, 
              location:this.labelLocationRef.current.innerText }));
      };
      render () {
        return (
          <div>
            <div className="App">
              <form onSubmit={e => this.handleSubmit (e)}>
                <ReactFormUncontrolledChildComponent
                  type="text"
                  label="Name"
                  name="name"
                  placeholder="Enter name"
                  ref={this.nameInputRef}
                  changeHandler={this.changeHandler}
                />
                <ReactFormUncontrolledChildComponent
                  type="number"
                  label="Age"
                  name="age"
                  placeholder="Enter age"
                  ref={this.ageInputRef}
                  changeHandler={this.changeHandler}
                />
                <ReactFormUncontrolledChildComponent
                  type="text"
                  label="Location"
                  name="location"
                  placeholder="Enter location"
                  ref={this.locationInputRef}
                  changeHandler={this.changeHandler}
                />
                <div style={{marginTop: 10}}>
                  <input type="submit" value="Submit" />
                </div>
              </form>
            </div>
            <div>
              <h2>Name: <span ref={this.labelNameRef}></span></h2>
              <p>Age: <span ref={this.labelAgeRef}></span></p>
              <p>Location: <span ref={this.labelLocationRef}></span></p>
            </div>
          </div>
        );
      }
    }
    
    export default ReactFormUncontrolledParentComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import ReactFormUncontrolledParentComponent from './ReactFormUncontrolledParentComponent';
    
    function App() {
      return (
        <div className="App">
            <ReactFormUncontrolledParentComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-uncontrolled-child-component-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Form - Uncontrolled Child Component
               
               :custom-color-primary-bold:`React Form - Uncontrolled Child Component`, homepage
            
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-form-uncontrolled-child-component-input.png
               :align: center
               :class: sd-my-0
               :alt: React Form - Uncontrolled Child Component
               
               :custom-color-primary-bold:`React Form - Uncontrolled Child Component`, form input
            

**************************************************************************************************
React Hook Form
**************************************************************************************************

React Hook Form is a React library for building forms. It is very flexible and can be used for simple forms as well as large forms with complex validation and submission logic. It is also very performant and optimised not to cause unnecessary re-renders.
    
    - install the react-hook-form library ::
        
        # npm install the react-hook-form library 
        npm install react-hook-form
        # yarn install the react-hook-form library 
        yarn add react-hook-form
        
    - import the useForm hook from the library ::
        
        # import the useForm hook
        import { useForm } from "react-hook-form";
        
    - use the useForm hook ::
        
        # destructure the register and handleSubmit properties
        const { register, handleSubmit, formState: {errors, isSubmitting, isSubmitSuccessful} } = useForm();
        
    - register an input element ::
        
        # register an input element with a variable name. This spread operator syntax is a new implementation to 
        #    the library that enables strict type checking in forms with TypeScript. 
        <input type="text" name="firstName" {...register('firstName')} />
        # React Hook Form versions older than v7 had the register method attached to the ref attribute as such:
        #    <input type="text" name="firstName" ref={register} />
        
    - form submission. The handleSubmit method can handle two functions as arguments. The first function passed as an argument will be invoked when the form validation is successful. The second function is called with errors when the validation fails ::
        
        # create onSubmit and onErrors methods to handle form submission
        const onFormSubmit  = data => console.log(data);
        const onErrors = errors => console.error(errors);
        <form onSubmit={handleSubmit(onFormSubmit, onErrors)}>
            {/* ... */}
        </form>
        
==================================================================================================
Basic Form with React Hook Form
==================================================================================================

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
- Create the file ``./ReactHookFormUseFormFunctionComponent.js`` ::
    
    import React, { useRef } from "react";
    import { useForm } from "react-hook-form";
    import "./App.css";
    
    const ReactHookFormUseFormFunctionComponent = () => {
      const {
        register,
        handleSubmit
      } = useForm();
    
      const labelNameRef = useRef(null);
      const labelAgeRef = useRef(null);
      const labelLocationRef = useRef(null);
    
      const onFormSubmit = (data) => {
        alert(
          JSON.stringify({
            name: labelNameRef.current.innerText,
            age: labelAgeRef.current.innerText,
            location: labelLocationRef.current.innerText,
          })
        );
      };
    
      const handleChange = (e) => {
        let name = e.target.name;
        if (name === "name") {
          labelNameRef.current.innerText = e.target.value;
        } else if (name === "age") {
          labelAgeRef.current.innerText = e.target.value;
        } else if (name === "location") {
          labelLocationRef.current.innerText = e.target.value;
        }
      };
    
      return (
        <div>
          <div className="App">
            <form onSubmit={handleSubmit(onFormSubmit)}>
              <div style={{ marginTop: 10 }}>
                <label
                  htmlFor="name"
                  style={{
                    display: "inline-block",
                    width: "3rem",
                    marginRight: "1.5rem",
                  }}
                >
                  Name
                </label>
                <input
                  type="text"
                  id="name"
                  name="name"
                  placeholder="Enter name"
                  {...register('name')} 
                  onChange={handleChange}
                />
              </div>
              <div style={{ marginTop: 10 }}>
                <label
                  htmlFor="age"
                  style={{
                    display: "inline-block",
                    width: "3rem",
                    marginRight: "1.5rem",
                  }}
                >
                  Age
                </label>
                <input
                  type="number"
                  id="age"
                  name="age"
                  placeholder="Enter age"
                  {...register('age')}
                  onChange={handleChange}
                />
              </div>
              <div style={{ marginTop: 10 }}>
                <label
                  htmlFor="location"
                  style={{
                    display: "inline-block",
                    width: "3rem",
                    marginRight: "1.5rem",
                  }}
                >
                  Location
                </label>
                <input
                  type="text"
                  id="location"
                  name="location"
                  placeholder="Enter location"
                  {...register('location')}
                  onChange={handleChange}
                />
              </div>
              <div style={{ marginTop: 10 }}>
                <input type="submit" value="Submit" />
              </div>
            </form>
          </div>
          <div>
            <h2>
              Name: <span ref={labelNameRef}></span>
            </h2>
            <p>
              Age: <span ref={labelAgeRef}></span>
            </p>
            <p>
              Location: <span ref={labelLocationRef}></span>
            </p>
          </div>
        </div>
      );
    };
    
    export default ReactHookFormUseFormFunctionComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import ReactHookFormUseFormFunctionComponent from './ReactHookFormUseFormFunctionComponent';
    
    function App() {
      return (
        <div className="App">
            <ReactHookFormUseFormFunctionComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-hook-form-use-form-component-home.png
               :align: center
               :class: sd-mb-1
               :alt: React Hook Form - useForm Component
               
               :custom-color-primary-bold:`React Hook Form - useForm Component`, homepage
            
        .. grid-item::
            
            .. figure:: images/tut10/tut10-react-hook-form-use-form-component-input.png
               :align: center
               :class: sd-my-0
               :alt: React Hook Form - useForm Component
               
               :custom-color-primary-bold:`React Hook Form - useForm Component`, form input
            
    
        
==================================================================================================
Validate Form with React Hook Form
==================================================================================================

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
