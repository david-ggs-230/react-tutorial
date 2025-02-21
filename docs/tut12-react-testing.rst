.. _tut12-react-testing:


.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-green
   :class: sd-text-success
   
.. role:: custom-color-red
   :class: sd-text-danger
   
.. role:: custom-color-black
   :class: sd-text-black
   
.. role:: custom-color-black-bold
   :class: sd-text-black sd-font-weight-bold
   
.. role:: custom-color-primary-underline
   :class: sd-text-primary sd-text-decoration-line-underline
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold
   
.. rst-class:: title-center h1
   
React Unit Testing

##################################################################################################
Tut12-React Unit Testing
##################################################################################################

Unit Testing with Jest and React Testing Library
    
    - Jest is a JavaScript testing framework maintained by Facebook, designed with a focus on simplicity and support for large JavaScript applications, especially React. It offers built-in utilities like test runners, mocking, snapshot testing, and code coverage reporting. Jest is preinstalled in a Create React App project and configured to look for tests in files with particular extensions. These file extensions are .test.ts for tests on pure functions and .test.tsx for tests on components. Alternatively, a .spec.* file extension could be used.
    - React Testing Library (RTL) is a lightweight solution for testing React components. RTL promotes testing components in a way that closely resembles how users interact with them. Instead of focusing on testing the internal implementation, RTL emphasizes testing the UI behaviour and user interactions. React Testing Library is a popular companion library for testing React components. It provides functions to render components and then select internal elements. Those internal elements can then be checked using special matchers provided by another companion library called jest-dom.
    

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut12-react-testing> ::
    
    yarn create react-app tut12-react-testing
    
- Move inside the ReactJS App/src folder <tut12-react-testing/src> ::
    
    cd tut12-react-testing/src
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut12-react-testing> ::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Testing Functions with Jest
**************************************************************************************************

Jest is a Node-based runner. This means that the tests always run in a Node environment and not in a real browser. This lets us enable fast iteration speed and prevent flakiness. Jest is intended to be used for unit tests of your logic and your components rather than the DOM quirks.

At a high level, Jest provides the describe, it, test, and expect functions to organize and execute tests. You can think of the describe function as a test suite. Use the describe function to group related tests for specific components. The it and test functions are for specific tests. The it and test functions are interchangeable functions used to house and run the code for individual test cases. Use the expect function to assert the expected output. Jest also provides mock functions to handle code outside the realm of tests and coverage reporting. A test written with Jest can be as simple as testing the output of a pure function.

Install Jest ::
    
    # npm
    npm install --save-dev jest react-test-renderer
    # yarn
    yarn add --dev jest react-test-renderer
    # run npm test, Jest will launch in watch mode
    npm test
    


Testing functions

A test is defined using Jest’s test function ::
    
    # normal function
    test('test name', () => {
        // test implementation
    });
    
    # Asynchronous function
    test('test name', async () => {
        // test implementation
    });
    
==================================================================================================
Testing functions
==================================================================================================

    - function ::
        
        class Calculator {
          add (a, b) {
            if(typeof a  !== 'number' || typeof b  !== 'number' ){
             throw new TypeError("Parameters must be of type number!");
            } 
            return Number(a + b); 
          }
        }
        export default Calculator;
        
    - test function ::
        
        describe ('add', () => {
            it ('should add 1 and 1 and return 2', () => {
              const calculator = new Calculator ();
              const result = calculator.add (1, 1);
              expect (result).toBe (2);
            });
            test ('should add 1 and -9 and return -8', () => {
              const calculator = new Calculator ();
              const result = calculator.add (1, -9);
              expect (result).toBe (-8);
            });
            test ('should add 1 and Number.MAX_VALUE and return Infinity', () => {
              const calculator = new Calculator ();
              expect (calculator.add (234, 1e309)).toBe (Number.POSITIVE_INFINITY);
            });
        });
        
    - test error ::
        
        describe ('add', () => {
            test ('should add 1 and "abc" and return Error("invalid argument type")', () => {
              const calculator = new Calculator ();
              expect (() => calculator.add (1, 'abc')).toThrow (
                /Parameters must be of type number!/i
              );
              expect (() => calculator.add (1, 'abc')).toThrow (
                new TypeError ('Parameters must be of type number!')
              );
              expect (calculator.add (1, Number.NaN)).toBeNaN ();
              
              const testFunction = () => calculator.add( 1, 'bcd');
              expect(testFunction).toThrow();
              expect(testFunction).toThrow(Error);
              expect(testFunction).toThrow('Parameters must be of type number!');
              expect(testFunction).toThrow(/type number/);
            });
        });
        
==================================================================================================
Async function
==================================================================================================
    
    - function './AsyncFunction.js' ::
        
        class AsyncFunction {
          callbackfunc=(value)=>{};
          withCallback=(callbackfunc)=>{
              setTimeout(() => callbackfunc("Hello World"), 1000);
          }
          withPromise=()=>{
              return new Promise((resolve)=>{
                  setTimeout(() => resolve("Hello World"), 1000);
              });
          }
        }
        export default AsyncFunction ;
        
    - test async function ::
        
        import AsyncFunction from './AsyncFunction';
        
        describe ('AsyncFunction', () => {
          let asyncFunction;
          beforeEach (() => {
            asyncFunction = new AsyncFunction ();
          });
          it ('should work with callback', done => {
            asyncFunction.withCallback (value => {
              expect (value).toBe ('Hello World');
              done ();
            });
          });
          it ('should work with promises', () => {
            return asyncFunction.withPromise ().then (value => {
              expect (value).toBe ('Hello World');
            });
          });
          it ('should work with resolves', () => {
            const promise = asyncFunction.withPromise ();
            return expect (promise).resolves.toBe ('Hello World');
          });
          it ('should work with async functions', async () => {
            const data = await asyncFunction.withPromise ();
            expect (data).toBe ('Hello World');
          });
        });
        
==================================================================================================
Mock function
==================================================================================================
    
    - function './MockFunction.js' ::
        
        function getNumber () {
          return Math.floor (Math.random () * 10);
        }
        export default getNumber;
        
    - test mock function ::
        
        import getNumber from './MockFunction';
        
        describe ('getNumber', () => {
          it ('should return a valid number', () => {
            const originalRandom = global.Math.random;
            global.Math.random = jest.fn ().mockReturnValue (0.41);
            const result = getNumber ();
            expect (result).toBe (4);
            expect (global.Math.random).toHaveBeenCalled ();
            global.Math.random = originalRandom;
          });
        });
        

**************************************************************************************************
Testing Components with React Testing Library (RTL)
**************************************************************************************************

React Testing Library (RTL) is a lightweight and easy-to-use tool for testing the Document Object Model (DOM) output of components. It abstracts a lot of boilerplate code, allowing you to write code that is easier to read, and allows you to test the code. The library encourages you to move away from testing implementation details, to avoid many false negative and false positive test cases. Instead, the library's API of tools makes it easy for you to write tests that simulate actual users' behaviors with your components, yielding confidence that the application works as expected for users.

Testing Library encourages you to avoid testing implementation details like the internals of a component you're testing. The guiding principles of this library emphasize a focus on tests that closely resemble how users interact with your web pages.

You may want to avoid testing the following implementation details:
    
    -Internal state of a component
    -Internal methods of a component
    -Lifecycle methods of a component
    -Child components
    
==================================================================================================
Install React Testing Library
==================================================================================================

React Testing Library (RTL) by Kent C. Dodds got released as alternative to Airbnb's Enzyme. While Enzyme gives React developers utilities to test internals of React components, React Testing Library takes a step back and questions us "how to test React components to get full confidence in our React components": Rather than testing a component's implementation details, React Testing Library puts the developer in the shoes of an end user of an React application. React Testing Library builds on top of DOM Testing Library by adding APIs for working with React components. It provides light utility functions on top of react-dom and react-dom/test-utils, in a way that encourages better testing practices.



Reference: 
    
    - `React Testing Library Tutorial <https://www.robinwieruch.de/react-testing-library/>`_ , November 22, 2022 by Robin Wieruch
    - `Using the React Testing Library debug method <https://blog.logrocket.com/using-react-testing-library-debug-method/>`_ , Nov 3, 2023 by Ibadehin Mojeed
    
- Install React Testing Library ::
    
    # npm
    npm install --save-dev @testing-library/react @testing-library/dom @testing-library/jest-dom @testing-library/user-event
    # yarn
    yarn add --dev @testing-library/react @testing-library/dom @testing-library/jest-dom @testing-library/user-event
    # run npm test, Jest will launch in watch mode
    npm test
    # run yarn test, Jest will launch in watch mode
    yarn test
    
- HiddenMessage Component ::
    
    import './App.css';
    import { useState } from 'react';
    
    function HiddenMessage() {
        const [showMessage, setShowMessage] = useState(false);
      
        const toggleMessage = () => {
          setShowMessage(!showMessage);
        };
      
        return (
          <div className="App" style={{ marginTop: 40 }}>
            <h1>Show/Hide Message</h1>
            <button onClick={toggleMessage}>
              {showMessage ? 'Hide' : 'Show'} Message
            </button>
            {showMessage && <p>This is a toggled message!</p>}
          </div>
        );
      }
      
    export default HiddenMessage;
    

- UserSearchComponent ::
    
    import React from 'react';
    import SearchComponent from './SearchComponent';
    
    function UserSearchComponent () {
      const [search, setSearch] = React.useState ('');
      const [user, setUser] = React.useState (null);
    
      const handleChange = async event => {
        setSearch (event.target.value);
      };
      const getUser = () => {
        return new Promise (function (resolve) {
          setTimeout (function () {
            resolve ({id: '1', name: 'Robin'});
          }, 5000);
        });
      };
      React.useEffect (() => {
        const loadUser = async () => {
          const user = await getUser ();
          setUser (user);
        };
    
        loadUser ();
      }, []);
      return (
        <div>
          {user && <p>Signed in as {user.name}</p>}
          <SearchComponent value={search} onChange={handleChange}>
            Search:
          </SearchComponent>
    
          <p>Searches for {search ? search : '...'}</p>
        </div>
      );
    }
    
    export default UserSearchComponent;
    
- SearchComponent ::
    
    import * as React from 'react';
    
    function SearchComponent({value, onChange, children}) {
      return (
        <div style={{marginTop: 40}}>
          <label htmlFor="search">{children}</label>
          <input
            id="search"
            type="text"
            value={value}
            onChange={onChange}
            style={{marginLeft: 10}}
          />
        </div>
      );
    }
    
    export default SearchComponent;
    

==================================================================================================
Rendering a React component
==================================================================================================

    
- imports ::
    
    import { render, screen, logRoles, prettyDOM} from '@testing-library/react';
    // import Component
    import HiddenMessage from './HiddenMessage';
    
- render Component ::
    
    const { msgDOMContainer } = render(<HiddenMessage />);
    
- show debug, prettyDOM(container, maxLength, options) helps format and display the DOM structure in a more readable way. ::
    
    console.log(prettyDOM(msgDOMContainer));
    
- Complete code './HiddenMessage.test.js' ::
    
    import {render, screen, logRoles, prettyDOM} from '@testing-library/react';
    
    import HiddenMessage from './HiddenMessage';
    
    test ('renders <HiddenMessage /> component', () => {
      const {msgDOMContainer} = render (<HiddenMessage />);
      console.log (prettyDOM (msgDOMContainer));
    });
    
==================================================================================================
Selecting a React component element
==================================================================================================

Conveniently getBy throws an error by default if the element cannot be found. However, this makes it difficult to check for elements which shouldn't be there. The getByText function accepts a string as argument, as we are using it right now, but also a regular expression. Whereas a string argument is used for the exact match, a regular expression can be used for a partial match which is often more convenient. 
    
    - getByText
    - getByRole
    - getByLabelText
    - getByPlaceholderText
    - getByAltText
    - getByDisplayValue
    
Every time you are asserting that an element isn't there, use queryBy. queryBy with all its search types:
    
    - queryByText
    - queryByRole
    - queryByLabelText
    - queryByPlaceholderText
    - queryByAltText
    - queryByDisplayValue
    
The findBy search variant is used for asynchronous elements which will be there eventually. findBy with all its search types. 
    
    - findByText
    - findByRole
    - findByLabelText
    - findByPlaceholderText
    - findByAltText
    - findByDisplayValue
    
Multiple elements:
    
    - getAllBy
    - queryAllBy
    - findAllBy
    
Assertive Functions, all these assertive functions come in an extra package ``@testing-library/jest-dom`` :
    
    - toBeDisabled
    - toBeEnabled
    - toBeEmpty
    - toBeEmptyDOMElement
    - toBeInTheDocument
    - toBeInvalid
    - toBeRequired
    - toBeValid
    - toBeVisible
    - toContainElement
    - toContainHTML
    - toHaveAttribute
    - toHaveClass
    - toHaveFocus
    - toHaveFormValues
    - toHaveStyle
    - toHaveTextContent
    - toHaveValue
    - toHaveDisplayValue
    - toBeChecked
    - toBePartiallyChecked
    - toHaveDescription
    

- get Component element ::
    
    const headingElement = screen.getByText(/Show\/Hide Message/i);
    expect(headingElement).toBeInTheDocument();
    const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
    expect (buttonElement).toBeInTheDocument ();
    
- logRoles can log an element’s ARIA role or a list of roles applied to elements within the DOM tree. ::
    
    logRoles(headingElement);
    logRoles (buttonElement);
    
- Complete code './HiddenMessage.test.js' ::
    
    import {render, screen, logRoles, prettyDOM} from '@testing-library/react';
    
    import HiddenMessage from './HiddenMessage';
    
    test ('renders <HiddenMessage /> component', () => {
      const {msgDOMContainer} = render (<HiddenMessage />);
      console.log (prettyDOM (msgDOMContainer));
      const headingElement = screen.getByText (/Show\/Hide Message/i);
      expect (headingElement).toBeInTheDocument ();
      logRoles (headingElement);
      const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
      expect (buttonElement).toBeInTheDocument ();
      logRoles (buttonElement);
    });
    
==================================================================================================
Firing events
==================================================================================================

We can use RTL's fireEvent and waitFor functions to simulate interactions of an end user. The fireEvent function takes an element (here the input field by textbox role) and an event (here an event which has the value "JavaScript"). 

React Testing Library comes with an extended user event library which builds up on top of the fireEvent API. The userEvent API mimics the actual browser behavior more closely than the fireEvent API. For example, a fireEvent.change() triggers only a change event whereas userEvent.type triggers a change event, but also keyDown, keyPress, and keyUp events.

Whenever possible, use userEvent over fireEvent when using React Testing Library. At the time of writing this, userEvent doesn't include all the features of fireEvent, however, this may change in the future.

React Testing Library has a fireEvent function that can raise events on DOM elements. The following example raises a click event on a Save button: ::
    
    render(<button>Save</button>);
    fireEvent.click(screen.getByText('Save'));
    
The following example raises a mousedown event on a Save button: :: 
    
    render(<button>Save</button>);
    fireEvent.mouseDown(screen.getByText('Save'));
    
The following example raises a click event or mousedown event on a Save button: :: 
    
    const user = userEvent.setup();
    render(<button>Save</button>);
    await user.click(screen.getByText('Save'));
    
--------------------------------------------------------------------------------------------------
fireEvent
--------------------------------------------------------------------------------------------------

- imports ::
    
    import { render, screen, logRoles, prettyDOM, fireEvent } from '@testing-library/react';
    // import Component
    import HiddenMessage from './HiddenMessage';
    
- render Component ::
    
    render(<HiddenMessage />);
    
- get Component element ::
    
    const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
    expect (buttonElement).toBeInTheDocument ();
    
- fireEvent ::
    
    fireEvent.click (buttonElement);
    
- Complete code './HiddenMessage.test.js' ::
    
    import {render, screen, logRoles, prettyDOM} from '@testing-library/react';
    
    import HiddenMessage from './HiddenMessage';
    
    test ('<HiddenMessage /> button fireEvent', () => {
        render (<HiddenMessage />);
        const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
        fireEvent.click (buttonElement);
        console.log (prettyDOM (buttonElement));
        expect (buttonElement).toHaveTextContent ('Hide Message');
    });
    
--------------------------------------------------------------------------------------------------
Asynchronous fireEvent
--------------------------------------------------------------------------------------------------


- imports ::
    
    import {render, screen, fireEvent, prettyDOM} from '@testing-library/react';
    
    import '@testing-library/jest-dom/extend-expect';
    import UserSearchComponent from './UserSearchComponent';
    
- render Component ::
    
    render (<UserSearchComponent />);
    const user = await screen.findByText (/Signed in as/,{},{
        timeout: 10000,
        interval: 100,
    });
    console.log (prettyDOM (user));
    expect (user).toBeInTheDocument ();
    
- get Component element ::
    
    const inputElement = screen.getByRole ('textbox');
    console.log (prettyDOM (inputElement));
    
- fireEvent ::
    
    fireEvent.change (inputElement, {target: {value: 'JavaScript'}});
    await screen.findByText (/Searches for/i);
    
- Complete code './UserSearchComponent.test.js' ::
    
    import {render, screen, fireEvent, prettyDOM} from '@testing-library/react';
    
    import '@testing-library/jest-dom/extend-expect';
    import UserSearchComponent from './UserSearchComponent';
    describe ('renders UserSearchComponent waiting for fetchUser', () => {
      beforeAll (() => {
        jest.useFakeTimers ();
      });
    
      afterAll (() => {
        jest.useRealTimers ();
      });
      test ('renders UserSearchComponent and updates search text', async () => {
        render (<UserSearchComponent />);
        const user = await screen.findByText (/Signed in as/,{},{
            timeout: 10000,
            interval: 100,
        });
        console.log (prettyDOM (user));
        expect (user).toBeInTheDocument ();
    
        const inputElement = screen.getByRole ('textbox');
        console.log (prettyDOM (inputElement));
        fireEvent.change (inputElement, {target: {value: 'JavaScript'}});
        expect (inputElement).toHaveValue ('JavaScript');
        console.log (prettyDOM (inputElement));
    
        const paragraphElement = await screen.findByText (/Searches for/i);
        expect (paragraphElement).toHaveTextContent ('Searches for JavaScript');
    
        fireEvent.change (inputElement, {target: {value: 'React'}});
        await screen.findByText (/Searches for/i);
        expect (inputElement).toHaveValue ('React');
        expect (screen.getByText (/Searches for React/i)).toBeInTheDocument ();
      });
    });
    
--------------------------------------------------------------------------------------------------
userEvent
--------------------------------------------------------------------------------------------------

- imports ::
    
    import { render, screen, logRoles, prettyDOM} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    // import Component
    import HiddenMessage from './HiddenMessage';
    
- render Component ::
    
    render(<HiddenMessage />);
    
- get Component element ::
    
    const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
    expect (buttonElement).toBeInTheDocument ();
    
- userEvent ::
    
    userEvent.click (buttonElement);
    
- Complete code './HiddenMessage.test.js' ::
    
    import {render, screen, logRoles, prettyDOM} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import HiddenMessage from './HiddenMessage';
    
    test ('<HiddenMessage /> button userEvent', () => {
        render (<HiddenMessage />);
        const buttonElement = screen.getByRole ('button', {name: 'Show Message'});
        userEvent.click (buttonElement);
        console.log (prettyDOM (buttonElement));
        expect (buttonElement).toHaveTextContent ('Hide Message');
        userEvent.click (buttonElement);
        console.log (prettyDOM (buttonElement));
        expect (buttonElement).toHaveTextContent ('Show Message');
    });
    
--------------------------------------------------------------------------------------------------
Asynchronous userEvent
--------------------------------------------------------------------------------------------------

- imports ::
    
    import {render, screen, fireEvent, prettyDOM} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import '@testing-library/jest-dom/extend-expect';
    import UserSearchComponent from './UserSearchComponent';
    
- render Component ::
    
    render (<UserSearchComponent />);
    const user = await screen.findByText (/Signed in as/,{},{
        timeout: 10000,
        interval: 100,
    });
    console.log (prettyDOM (user));
    expect (user).toBeInTheDocument ();
    
- get Component element ::
    
    const inputElement = screen.getByRole ('textbox');
    console.log (prettyDOM (inputElement));
    
- userEvent ::
    
    userEvent.type(inputElement, 'JavaScript');
    await screen.findByText (/Searches for/i);
    
- Complete code './UserSearchComponent.test.js' ::
    
    import {render, screen, fireEvent, prettyDOM} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import '@testing-library/jest-dom/extend-expect';
    import UserSearchComponent from './UserSearchComponent';
    
    describe ('UserSearchComponent', () => {
      beforeAll (() => {
        jest.useFakeTimers ();
      });
    
      afterAll (() => {
        jest.useRealTimers ();
      });
      
      test ('UserSearchComponent and userEvent', async () => {
        render (<UserSearchComponent />);
        const user = await screen.findByText (/Signed in as/,{},{
            timeout: 10000,
            interval: 100,
        });
        console.log (prettyDOM (user));
        expect (user).toBeInTheDocument ();
    
        const inputElement = screen.getByRole ('textbox');
        console.log (prettyDOM (inputElement));
        userEvent.type(inputElement, 'JavaScript');
        await screen.findByText (/Searches for/i);
        expect (inputElement).toHaveValue ('JavaScript');
        console.log (prettyDOM (inputElement));
    
        const paragraphElement = await screen.findByText (/Searches for/i);
        expect (paragraphElement).toHaveTextContent ('Searches for JavaScript');
        userEvent.clear (inputElement);
        userEvent.type (inputElement, 'React');
        await screen.findByText (/Searches for/i);
        expect (inputElement).toHaveValue ('React');
        expect (screen.getByText (/Searches for React/i)).toBeInTheDocument ();
        console.log (prettyDOM (inputElement));
      });
    });
    

==================================================================================================
callback handlers
==================================================================================================

Sometimes you will test React components in isolation as unit tests. Often these components will not have any side-effects or state, but only input (props) and output (JSX, callback handlers). For the Search component, we are using a utility from Vitest (or Jest) to mock the onChange function which is passed to the component. Then, after triggering the user interaction on the input field, we can assert that the onChange callback function has been called. While fireEvent executes the change event by only calling the callback function once, userEvent triggers it for every key stroke.

    
- imports ::
    
    import React from 'react';
    import {render, screen, fireEvent} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import SearchComponent from './SearchComponent';
    
- render Component ::
    
    render (
      <SearchComponent value="test" onChange={() => {}} children="Search:" />
    );
    
    expect (screen.getByLabelText (/search:/i)).toBeInTheDocument ();
    expect (screen.getByDisplayValue (/test/i)).toBeInTheDocument ();
    
- calls the onChange callback handler ::
    
    const handleChange = jest.fn ();
    render (
      <SearchComponent value="" onChange={handleChange} children="Search:" />
    );
    
    fireEvent.change (screen.getByLabelText (/search:/i), {
      target: {value: 'new value'},
    });
    expect (handleChange).toHaveBeenCalledTimes (1);
    await userEvent.type (screen.getByRole ('textbox'), 'JavaScript');
    expect (handleChange).toHaveBeenCalledTimes (11);
    
- Complete code './SearchComponent.test.js' ::
    
    import React from 'react';
    import {render, screen, fireEvent} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import SearchComponent from './SearchComponent';
    
    describe ('SearchComponent callback handler', () => {
      test ('renders the SearchComponent with given props', () => {
        render (
          <SearchComponent value="test" onChange={() => {}} children="Search:" />
        );
    
        expect (screen.getByLabelText (/search:/i)).toBeInTheDocument ();
        expect (screen.getByDisplayValue (/test/i)).toBeInTheDocument ();
      });
    
      test ('calls the onChange callback handler', async () => {
        const handleChange = jest.fn ();
        render (
          <SearchComponent value="" onChange={handleChange} children="Search:" />
        );
    
        fireEvent.change (screen.getByLabelText (/search:/i), {
          target: {value: 'new value'},
        });
        expect (handleChange).toHaveBeenCalledTimes (1);
        await userEvent.type (screen.getByRole ('textbox'), 'JavaScript');
        expect (handleChange).toHaveBeenCalledTimes (11);
      });
    });
    

==================================================================================================
Snapshot test
==================================================================================================

Snapshot tests are provided by Jest and are great to use when you simply want to make sure the HTML output of a component does not change unexpectedly. Suppose a developer does change the component's HTML structure, for example, by adding another paragraph element with static text. In that case, the snapshot test will fail and provide a visual of the changes so you can respond accordingly. 

    
- Complete code './SearchComponent.test.js' ::
    
    import React from 'react';
    import {render, screen, fireEvent} from '@testing-library/react';
    import userEvent from '@testing-library/user-event';
    import SearchComponent from './SearchComponent';
    
    describe ('SearchComponent callback handler', () => {
      
      test ('matches the snapshot', () => {
        const {asFragment} = render (
          <SearchComponent value="test" onChange={() => {}} children="Search:" />
        );
        expect (asFragment ()).toMatchSnapshot ();
      });
    });
    
**************************************************************************************************
Getting code coverage
**************************************************************************************************

To get code coverage, we run the test command with a --coverage option. We also include a
--watchAll=false option that tells Jest not to run in watch mode. So, run the following command
in a terminal to determine code coverage on our app: ::
    
    # npm
    npm run test -- --coverage --watchAll=false
    # yarn 
    yarn test -- --coverage --watchAll=false
    
Here’s an explanation of all the statistic columns:
    
    - **%Stmts** : This is statement coverage, which is how many source code statements have been executed during test execution
    - **%Branch** : This is branch coverage, which is how many of the branches of conditional logic have been executed during test execution
    - **%Funcs** : This is function coverage, which is how many functions have been called during test execution
    - **%Lines** : This is line coverage, which is how many lines of source code have been executed during test execution
    