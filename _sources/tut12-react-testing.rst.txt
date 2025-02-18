.. _tut12-react-testing:


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
    npm run jest
    


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

==================================================================================================
DOM Testing Library
==================================================================================================

The DOM Testing Library makes it easier to test the UI of applications like real users to gain confidence that the application works as expected for users. There are no methods to get the component's state value or directly invoke component methods.

The library encourages you to select DOM elements in ways that are available to all users. The library's API includes accessibility-focused query methods allowing you to interact with the DOM like users with disabilities who require tools such as screen readers or other forms of assistive technology to navigate applications. 

For the following element in the test
    
    - Element ::
        
        <label for="firstname">First name:</label>
        <input
            type="text"
            id="firstname"
            name="firstname"
            placeholder="first name..."
        >
        
    - Select the input: The getByPlaceholderText method is used from the screen object to select the DOM element by its placeholder value in the following code. ::
        
        screen.getByPlaceholderText(/first name/i)
        
    - Select the input: The screen.getByRole method is used from the screen object to select the element by its role of a textbox with the name 'first name:' by a label element and an accessible name attribute. ::
        
        screen.getByRole('textbox', {
            name: /first name:/i
        })
        
    - Use the render method of the React Testing Library to place the component into an element attached to the DOM ::
        
        render(<SomeComponent />);
        







