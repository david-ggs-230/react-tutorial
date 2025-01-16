.. _tut05-react-event:

.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold


.. rst-class:: title-center h1
   
React Event

##################################################################################################
Tut05-React Event
##################################################################################################

Events are just some actions performed by a user to interact with any application. They can be the smallest of actions, like hovering a mouse pointer on an element that triggers a drop-down menu, resizing an application window, or dragging and dropping elements to upload them etc. Events in React are divided into three categories:
    
    - Mouse Events − onClick, onDrag, onDoubleClick
    - Keyboard Events − onKeyDown, onKeyPress, onKeyUp
    - Focus Events − onFocus, onBlur
    

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut05-react-event>::
    
    yarn create react-app tut05-react-event
    
- Move inside the ReactJS App/src folder <tut05-react-event/src>::
    
    cd tut05-react-event/src
    
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
- Run the ReactJS App <tut05-react-event>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Event Management
**************************************************************************************************

React event handling is very similar to DOM events with little changes. In JavaScript, when an event is specified, you will be dealing with a react event type called a synthetic event instead of regular DOM events. SyntheticEvent is expensive in terms of CPU resources as every synthetic event created needs to be garbage-collected. Every synthetic event object has the following attributes:
    
    - boolean bubbles
    - boolean cancelable
    - DOMEventTarget currentTarget
    - boolean defaultPrevented
    - number eventPhase
    - boolean isTrusted
    - DOMEvent nativeEvent
    - void preventDefault()
    - boolean isDefaultPrevented()
    - void stopPropagation()
    - boolean isPropagationStopped()
    - void persist()
    - DOMEventTarget target
    - number timeStamp
    - string type
    
==================================================================================================
Event Handler in Class Component
==================================================================================================

Define an event handler method to handle the given event:
    
    - using regular function
        
        - Define the event handler ::
            
            # Passing no argument
            eventHandlerMethod() { 
               .... 
            }
            
            # Passing an event argument
            eventHandlerMethod(e) { 
               .... 
            }
            
            # Passing extra arguments 
            eventHandlerMethod(extra, e) { 
               .... 
            }
            
        - Use the event handler
            
            - must bind the event handler method in the constructor of the component ::
                
                constructor(props) { 
                   ... 
                   this.eventHandlerMethod = this.eventHandlerMethod.bind(this); 
                }
                
            - Handle event on element ::
                
                # Passing no argument
                <tag onClick={this.eventHandlerMethod}> ... </tag>
                
                #Passing an event argument
                <tag onClick={this.eventHandlerMethod}> ... </tag>
                
                #Passing extra arguments 
                <tag onClick={this.eventHandlerMethod.bind(this, extra)}> ... </tag>
                <tag onClick={(e)=>this.eventHandlerMethod(extra, e)}> ... </tag>
                
    - using lambda function
        
        - Define the event handler ::
            
            # Passing no argument
            eventHandlerMethod = () => { 
               .... 
            }
            
            # Passing an event argument
            eventHandlerMethod = (e) => { 
               .... 
            }
            
            # Passing extra arguments 
            eventHandlerMethod = (extra, e) => { 
               .... 
            }
            
        - Use the event handler
            
            - in lambda syntax, binding is not needed. this keyword will be automatically bound to the event handler method ::
                
                constructor(props) { 
                   ... 
                   //this.eventHandlerMethod = this.eventHandlerMethod.bind(this);  # not needed
                }
                
            - Handle event on element ::
                
                # Passing no argument
                <tag onClick={this.eventHandlerMethod}> ... </tag>
                
                #Passing an event argument
                <tag onClick={this.eventHandlerMethod}> ... </tag>
                
                #Passing extra arguments 
                <tag onClick={(e)=>this.eventHandlerMethod(extra, e)}> ... </tag>
                

--------------------------------------------------------------------------------------------------
Event Handler (Pass no argument)
--------------------------------------------------------------------------------------------------

Here’s an example of a ReactJS class component that handles both button and div clicks to update a message list:
    
    - Button click, add 'Button was clicked!' to LogMessageList
    - Div click, add 'Div was clicked!' to LogMessageList
    
Structure:
    
    - Create a parent component <App />
    - Create a child component <EventHandlerComponent />
    - Three elements in  <EventHandlerComponent />, LogMessage, Button and Div
    - Child component update information when button is clicked
    
- Move inside the ReactJS App/src folder <tut05-react-event/src>::
    
    cd tut05-react-event/src
    
- Create the file ``EventHandlerComponent.js`` (Child Component)::
    
    import React, {Component} from 'react';
    import './App.css';
    
    class EventHandlerComponent extends Component {
      constructor (props) {
        super (props);
        // Initialize state with a list of messages
        this.state = {messages: []};
        this.handleDivClick = this.handleDivClick.bind (this);
      }
    
      // Event handler for button click
      // class property, using lambda function to define event handler. autobind.
      handleButtonClick = () => {
        this.setState (prevState => ({
          messages: [...prevState.messages, 'Button was clicked!'],
        }));
      };
    
      // Event handler for div click,
      // Class method, must bind the event handler method in the constructor of the component.
      handleDivClick () {
        this.setState (prevState => ({
          messages: [...prevState.messages, 'Div was clicked!'],
        }));
      }
      render () {
        return (
          <div>
            <h4>React Event Handler Example (Class Component)</h4>
            <div
              onClick={this.handleDivClick}
              style={{
                marginTop: '20px',
                padding: '20px',
                /*backgroundColor: '#f0f0f0',*/
                cursor: 'pointer',
              }}
            >
              Click Me (Div)
            </div>
            {/* Button that triggers button click handler */}
            <button onClick={this.handleButtonClick}>Click Me (Button)</button>
    
            <div className="App">
              <h5>LogMessages</h5>
              {/* Display the list of messages */}
              <ul>
                {this.state.messages.map ((message, index) => (
                  <li key={index}>{message}</li>
                ))}
              </ul>
            </div>
          </div>
        );
      }
    }
    
    export default EventHandlerComponent;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import EventHandlerComponent from './EventHandlerComponent';
    
    function App() {
      return (
        <div className="App">
          <EventHandlerComponent />
        </div>
      );
    }
    
    export default App;
    
    
- Screenshot
    
    .. figure:: images/tut05/tut05-react-event-class-component.png
       :align: center
       :class: sd-my-2
       :alt: Event Handler (Pass no argument)
       
       :custom-color-primary-bold:`Event Handler (Pass no argument)`, Click :custom-color-primary:`Click Me (Div)` or :bdg-secondary-line:`Click Me (Button)` to update logMessages
    

--------------------------------------------------------------------------------------------------
Event Handler (Pass extra argument)
--------------------------------------------------------------------------------------------------

Here’s an example of a ReactJS class component that handles both button and div clicks to update a message list:
    
    - Button click, add 'Button was clicked!' to LogMessageList
    - Div click, add 'Div was clicked!' to LogMessageList
    
Structure:
    
    - Create a parent component <App />
    - Create a child component <EventHandlerComponentWithExtraArgs />
    - Three elements in  <EventHandlerComponentWithExtraArgs />, LogMessage, Button and Div
    - Child component update information when button is clicked
    
- Move inside the ReactJS App/src folder <tut05-react-event/src>::
    
    cd tut05-react-event/src
    
- Create the file ``EventHandlerComponentWithExtraArgs.js`` (Child Component)::
    
    import React, {Component} from 'react';
    import './App.css';
    
    class EventHandlerComponentWithExtraArgs extends Component {
      constructor (props) {
        super (props);
        // Initialize state with a list of messages
        this.state = {messages: []};
        this.handleDivClick = this.handleDivClick.bind (this);
      }
    
      // Event handler for button click
      // class property, using lambda function to define event handler. autobind.
      handleButtonClick = (number,e) => {
        this.setState (prevState => ({
          messages: [...prevState.messages, 'Button was clicked! Passed Argument: ['+number+']'],
        }));
      };
    
      // Event handler for div click,
      // Class method, must bind the event handler method in the constructor of the component.
      handleDivClick ( number) {
        this.setState (prevState => ({
          messages: [...prevState.messages, 'Div was clicked! Passed Argument: ['+number+']'],
        }));
      }
      render () {
        return (
          <div>
            <h4>React Event Handler Example (Class Component)</h4>
            <div
              onClick={ this.handleDivClick.bind(this, Math.floor(Math.random() * 20)) } 
              style={{
                marginTop: '20px',
                padding: '20px',
                /*backgroundColor: '#f0f0f0',*/
                cursor: 'pointer',
              }}
            >
              Click Me (Div)
            </div>
            {/* Button that triggers button click handler */}
            <button onClick={(e)=>this.handleButtonClick(Math.floor(Math.random() * 20),e)}>Click Me (Button)</button>
    
            <div className="App">
              <h5>LogMessages</h5>
              {/* Display the list of messages */}
              <ul>
                {this.state.messages.map ((message, index) => (
                  <li key={index}>{message}</li>
                ))}
              </ul>
            </div>
          </div>
        );
      }
    }
    
    export default EventHandlerComponentWithExtraArgs;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import EventHandlerComponentWithExtraArgs from './EventHandlerComponentWithExtraArgs';
    
    function App() {
      return (
        <div className="App">
          <EventHandlerComponentWithExtraArgs />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut05/tut05-react-event-class-component-extra-arg.png
       :align: center
       :class: sd-my-2
       :alt: Event Handler (Pass extra argument)
       
       :custom-color-primary-bold:`Event Handler (Pass extra argument)`, Click :custom-color-primary:`Click Me (Div)` or :bdg-secondary-line:`Click Me (Button)` to update logMessages
    

==================================================================================================
Event Handler in Function Component
==================================================================================================

Define an event handler method to handle the given event:
    
    - using regular function
        
        - Define the event handler ::
            
            # Passing no argument
            eventHandlerMethod() { 
               .... 
            }
            
            # Passing an event argument
            eventHandlerMethod(e) { 
               .... 
            }
            
            # Passing extra arguments 
            eventHandlerMethod(extra, e) { 
               .... 
            }
            
        - Use the event handler ::
            
            # Passing no argument
            <tag onClick={eventHandlerMethod}> ... </tag>
            
            #Passing an event argument
            <tag onClick={eventHandlerMethod}> ... </tag>
            
            #Passing extra arguments 
            <tag onClick={eventHandlerMethod.bind(this, extra)}> ... </tag>
            <tag onClick={(e)=>eventHandlerMethod(extra, e)}> ... </tag>
            
    - using lambda function
        
        - Define the event handler ::
            
            # Passing no argument
            eventHandlerMethod = () => { 
               .... 
            }
            
            # Passing an event argument
            eventHandlerMethod = (e) => { 
               .... 
            }
            
            # Passing extra arguments 
            eventHandlerMethod = (extra, e) => { 
               .... 
            }
            
        - Use the event handler
            
            # Passing no argument
            <tag onClick={eventHandlerMethod}> ... </tag>
            
            #Passing an event argument
            <tag onClick={eventHandlerMethod}> ... </tag>
            
            #Passing extra arguments 
            <tag onClick={eventHandlerMethod.bind(null, extra)}> ... </tag>
            <tag onClick={(e)=>eventHandlerMethod(extra, e)}> ... </tag>
            

--------------------------------------------------------------------------------------------------
Event Handler (Pass no argument)
--------------------------------------------------------------------------------------------------

Here’s an example of a ReactJS function component that handles both button and div clicks to update a message list:
    
    - Button click, add 'Button was clicked!' to LogMessageList
    - Div click, add 'Div was clicked!' to LogMessageList
    
Structure:
    
    - Create a parent component <App />
    - Create a child component <EventHandlerComponent />
    - Three elements in  <EventHandlerComponent />, LogMessage, Button and Div
    - Child component update information when button is clicked
    
- Move inside the ReactJS App/src folder <tut05-react-event/src>::
    
    cd tut05-react-event/src
    
- Create the file ``EventHandlerComponent.js`` (Child Component)::
    
    import React, { useState } from 'react';
    import './App.css';
    
    function  EventHandlerComponent() {
        const [messages, setMessages] = useState([]);
    
        // Regular function to handle div click
        function handleDivClick () {
            setMessages((prevMessages) => [...prevMessages, 'Div was clicked!']);
        };
        // Event handler for button click
        // class property, using lambda function to define event handler. autobind.
        const handleButtonClick = () => {
            setMessages((prevMessages) => [...prevMessages, 'Button was clicked!']);
        };
    
        return (
          <div>
            <h4>React Event Handler Example (Function Component)</h4>
            <div
              onClick={handleDivClick}
              style={{
                marginTop: '20px',
                padding: '20px',
                /*backgroundColor: '#f0f0f0',*/
                cursor: 'pointer',
              }}
            >
              Click Me (Div)
            </div>
            {/* Button that triggers button click handler */}
            <button onClick={handleButtonClick}>Click Me (Button)</button>
    
            <div className="App">
              <h5>LogMessages</h5>
              {/* Display the list of messages */}
              <ul>
                { messages.map ((message, index) => (
                  <li key={index}>{message}</li>
                ))}
              </ul>
            </div>
          </div>
        );
    }
    
    export default EventHandlerComponent;
    
- Edit the file ``App.js`` (Parent Component)::
    
    import './App.css';
    import EventHandlerComponent from './EventHandlerComponent';
    
    function App() {
      return (
        <div className="App">
          <EventHandlerComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut05/tut05-react-event-function-component.png
       :align: center
       :class: sd-my-2
       :alt: Event Handler (Pass no argument)
       
       :custom-color-primary-bold:`Event Handler (Pass no argument)`, Click :custom-color-primary:`Click Me (Div)` or :bdg-secondary-line:`Click Me (Button)` to update logMessages
    
