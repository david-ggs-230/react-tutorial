.. _tut07-react-component-styling:

.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold


.. rst-class:: title-center h1
   
React Component Styling

##################################################################################################
Tut07-React Component Styling
##################################################################################################

In general, React allows component to be styled using CSS class through className attribute. Since, the React JSX supports JavaScript expression, a lot of common CSS methodology can be used. Some of the top options are as follows
    
    - CSS stylesheet − Normal CSS styles along with className
    - Inline styling − CSS styles as JavaScript objects along with camelCase properties.
    - CSS Modules − Locally scoped CSS styles.
    - Sass stylesheet − Supports Sass based CSS styles by converting the styles to normal css at build time.
    

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut07-react-component-styling>::
    
    yarn create react-app tut07-react-component-styling
    
- Move inside the ReactJS App/src folder <tut07-react-component-styling/src>::
    
    cd tut07-react-component-styling/src
    
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
- Run the ReactJS App <tut07-react-component-styling>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
Component Styling
**************************************************************************************************

==================================================================================================
CSS Stylesheet
==================================================================================================

CSS stylesheet is usual, common and time-tested methodology. Simply create a CSS stylesheet for a component and enter all your styles for that particular component. Then, in the component, use className to refer the styles.

    
Structure:
    
    - Create a parent component <App />
    - Create a child component <StylingComponentCssStylesheet />
    - Create css stylesheet file <ItemsCssStyleSheet.css>
    - Child component show the styling effects
    
- Move inside the ReactJS App/src folder <tut07-react-component-styling/src>::
    
    cd tut07-react-component-styling/src
    
- Create the file ``ItemsCssStyleSheet.css`` (CSS StyleSheet) ::
    
    div.itemStyle {
      color: brown;
      font-size: 14px;
    }
    
    div.itemStyle.A {
      color: red;
      font-size: 16px;
    }
    
    div.itemStyle.B {
      color: black;
      font-size: 12px;
    }
    
    div.itemStyle.C {
      color: green;
      font-size: 16px;
    }
    
- Create the file ``StylingComponentCssStylesheet.js`` (Child Component) ::
    
    import React, {Component} from 'react';
    import './App.css';
    import './ItemsCssStyleSheet.css';
    
    class StylingComponentCssStylesheet extends Component {
      render () {
        return (
          <div className="App">
            <h4> Styling Component (CSS StyleSheet)</h4>
            <div className="itemStyle">
              <div><b>Item1:</b> <em>Default Style</em></div>
              <div className="itemStyle A"><b>Item2:</b> <em>itemStyle A</em></div>
              <div className="itemStyle B"><b>Item3:</b> <em>itemStyle B</em></div>
              <div className="itemStyle C"><b>Item4:</b> <em>itemStyle C</em></div>
              <div className="itemStyle"><b>Item5:</b> <em>Default Style</em></div>
            </div>
          </div>
        );
      }
    }
    
    export default StylingComponentCssStylesheet;
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import StylingComponentCssStylesheet from './StylingComponentCssStylesheet';
    
    function App () {
      return (
        <div className="App">
          <StylingComponentCssStylesheet />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut07/tut07-react-component-styling-css-stylesheet.png
       :align: center
       :class: sd-my-2
       :alt: Styling Component (CSS StyleSheet)
       
       :custom-color-primary-bold:`Styling Component (CSS StyleSheet)`
    

==================================================================================================
Inline Styling
==================================================================================================

Inline Styling is one of the safest ways to style the React component. It declares all the styles as JavaScript objects using DOM based css properties and set it to the component through style attributes.

Declare a variable of type object and set the styles.  All css properties can be used by representing it in camelCase format. Set style in the component using curly braces {}. Also, style can be directly set inside the component

Structure:
    
    - Create a parent component <App />
    - Create a child component <StylingComponentCssStylesheet />
    - Using Inline Styling in the child component <StylingComponentCssStylesheet />
    - Child component show the styling effects
    
- Move inside the ReactJS App/src folder <tut07-react-component-styling/src>::
    
    cd tut07-react-component-styling/src
    
- Create the file ``StylingComponentCssStylesheet.js`` (Child Component) ::
    
    import React, {Component} from 'react';
    import './App.css';
    
    class StylingComponentCssStylesheet extends Component {
        itemStyleInlineDefault = {
            color: 'brown', 
            fontSize: '14px' 
        }
        itemStyleInlineA = {
            color: 'red',
            fontSize: '16px'
        }
        itemStyleInlineB = {
            color: 'black',
            fontSize: '12x'
        }
        itemStyleInlineC = {
            color: 'green',
            fontSize: '16px'
        }   
    
      render () {
        return (
          <div className="App">
            <h4> Styling Component (Inline Styling)</h4>
            <div style={ this.itemStyleInlineDefault }>
              <div><b>Item1:</b> <em>Default Style</em></div>
              <div style={ this.itemStyleInlineA }><b>Item2:</b> <em>itemStyle A</em></div>
              <div style={ this.itemStyleInlineB }><b>Item3:</b> <em>itemStyle B</em></div>
              <div style={ this.itemStyleInlineC }><b>Item4:</b> <em>itemStyle C</em></div>
              <div style={ this.itemStyleInlineDefault }><b>Item5:</b> <em>Default Style</em></div>
              <div style={{color: 'purple',fontSize: '20px' }}><b>Item6:</b> <em>itemStyle D</em></div>
            </div>
          </div>
        );
      }
    }
    
    export default StylingComponentCssStylesheet;
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import StylingComponentCssStylesheet from './StylingComponentCssStylesheet';
    
    function App () {
      return (
        <div className="App">
          <StylingComponentCssStylesheet />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut07/tut07-react-component-styling-inline-style.png
       :align: center
       :class: sd-my-2
       :alt: Styling Component (Inline Styling)
       
       :custom-color-primary-bold:`Styling Component (Inline Styling)`
    

==================================================================================================
CSS Modules
==================================================================================================

Css Modules provides safest as well as easiest way to define the style. It uses normal css stylesheet with normal syntax. While importing the styles, CSS modules converts all the styles into locally scoped styles so that the name conflicts will not happen. Create a new stylesheet ending with .module.css and write regular css styles. Here, file naming convention is very important. React toolchain will pre-process the css files ending with .module.css through CSS Module. 

Next, open the component .js file and import the styles ending with .module.css, and use the styles as JavaScript expression in the component.

Structure:
    
    - Create a parent component <App />
    - Create a child component <StylingComponentCssStylesheet />
    - Create css module stylesheet file <ItemsCssStyleSheet.module.css>
    - Child component show the styling effects
    
- Move inside the ReactJS App/src folder <tut07-react-component-styling/src>::
    
    cd tut07-react-component-styling/src
    
- Create the file ``ItemsCssStyleSheet.module.css`` (CSS Module StyleSheet) ::
    
    div.itemStyle {
      color: brown;
      font-size: 14px;
    }
    
    div.itemStyle.A {
      color: red;
      font-size: 16px;
    }
    
    div.itemStyle.B {
      color: black;
      font-size: 12px;
    }
    
    div.itemStyle.C {
      color: green;
      font-size: 16px;
    }
    
    div.itemStyle .D {
      color: purple;
      font-size: 20px;
    }
    
    
- Create the file ``StylingComponentCssStylesheet.js`` (Child Component) ::
    
    import React, {Component} from 'react';
    import './App.css';
    import styles from './ItemsCssStyleSheet.module.css';
    
    class StylingComponentCssStylesheet extends Component {
      render () {
        return (
          <div className="App">
            <h4> Styling Component (CSS Modules)</h4>
            <div className={styles.itemStyle}>
              <div><b>Item1:</b> <em>Default Style</em></div>
              <div className={`${styles.itemStyle} ${styles.A}`}><b>Item2:</b> <em>itemStyle A</em></div>
              <div className={`${styles.itemStyle} ${styles.B}`}><b>Item3:</b> <em>itemStyle B</em></div>
              <div className={`${styles.itemStyle} ${styles.C}`}><b>Item4:</b> <em>itemStyle C</em></div>
              <div className="itemStyle"><b>Item5:</b> <em>Default Style</em></div>
              <div className={styles.D}><b>Item6:</b> <em>Default Style</em></div>
            </div>
          </div>
        );
      }
    }
    
    export default StylingComponentCssStylesheet;
    
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import StylingComponentCssStylesheet from './StylingComponentCssStylesheet';
    
    function App () {
      return (
        <div className="App">
          <StylingComponentCssStylesheet />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut07/tut07-react-component-styling-css-modules.png
       :align: center
       :class: sd-my-2
       :alt: Styling Component (CSS Modules)
       
       :custom-color-primary-bold:`Styling Component (CSS Modules)`
    
==================================================================================================
Sass stylesheet
==================================================================================================

Sass (Syntactically Awesome Stylesheets) is a powerful CSS preprocessor that extends CSS with additional features like variables, nesting, partials, and more. Essentially, Sass lets you write cleaner, more maintainable stylesheets, and then it compiles into regular CSS, which browsers can understand.

While CSS is essential for styling web pages, it can become unwieldy as your project grows. Sass simplifies CSS in the following ways:
    
    - Code Reusability: Sass provides variables and mixins to reuse chunks of code.
    - Maintainability: With features like partials and nesting, Sass helps you organize your styles logically.
    - Efficient Development: Sass makes complex styles easier to manage and reduces repetitive code, speeding up the development process.

**Features of Sass**
    
    - Variables ::
        
        // Variables
        $primary-color: #3498db;
        $secondary-color: #2ecc71;
        $font-stack: 'Helvetica, sans-serif';
        
        // Usage
        body {
          font-family: $font-stack;
          background-color: $primary-color;
        }
        
    - Nesting
        
        - Nesting allows you to write CSS in a hierarchical manner ::
            
            .navbar {
              background: $primary-color;
            
              .nav-link {
                color: white;
                &:hover {
                  color: darken(white, 10%);
                }
              }
            }
            
        - The above code compiles to: ::
            
            .navbar {
              background-color: #3498db;
            }
            .navbar .nav-item {
              color: white;
            }
            .navbar .nav-item:hover {
              color: #2ecc71;
            }
            
        
    - Partials and Imports
        
        - Partials in Sass allow you to split your styles into smaller, modular files. These partial files typically start with an underscore (_). This tells Sass not to compile these files on their own; instead, they are imported into a main file.
            
            - Example: File Structure for Partials ::
                
                /src
                /styles
                _variables.scss
                _mixins.scss
                _header.scss
                _footer.scss
                main.scss
                
            - In the _variables.scss file, we’ll define our variables ::
            
                // _variables.scss
                $primary-color: #3498db;
                $secondary-color: #2ecc71;
                $font-stack: 'Helvetica, sans-serif';
                
            
            - In _mixins.scss, we’ll define reusable mixins ::
            
                // _mixins.scss
                @mixin flex-center {
                  display: flex;
                  justify-content: center;
                  align-items: center;
                }
                
            
            - In _header.scss and _footer.scss, we define specific styles for components ::
            
                // _header.scss
                .header {
                  background-color: $primary-color;
                  @include flex-center;
                  height: 100px;
                  color: white;
                }
                
                // _footer.scss
                .footer {
                  background-color: $secondary-color;
                  @include flex-center;
                  height: 60px;
                  color: white;
                }
                
        - By importing all the partials into one main file, you create a single compiled CSS file, keeping your code modular and easy to maintain.
    
    - Mixins: Mixins in Sass allow you to create reusable chunks of code that can be included in other styles ::
        
        // Mixin Definition
        @mixin button-style($color, $bg-color) {
          color: $color;
          background-color: $bg-color;
          padding: 10px 20px;
          border-radius: 5px;
        }
        
        // Using the Mixin
        .button {
          @include button-style(white, $primary-color);
        }
        
        // In this example, the button-style mixin can be reused across different buttons, passing in different color values.
        
    - Inheritance: You can use @extend in Sass to inherit styles from other selectors, reducing redundancy. ::
        
        // Base Style
        .button {
          padding: 10px 20px;
          border-radius: 5px;
        }
        
        // Extend Base Style
        .primary-button {
          @extend .button;
          background-color: $primary-color;
          color: white;
        }
        
    - Operators: Sass supports basic math operations, making dynamic calculations easy in your styles. ::
        
        .container {
          width: 100% / 3;
        }
        
        
Structure:
    
    - Create a parent component <App />
    - Create a child component <StylingComponentCssStylesheet />
    - Create scss file <ItemsCssStyleSheet.scss>
    - Child component show the styling effects
    
- Move inside the ReactJS App/src folder <tut07-react-component-styling/src> ::
    
    cd tut07-react-component-styling/src
    
- Install Sass ::
    
    # yarn add -D sass or npm install --save-dev sass
    yarn add -D sass
    
- Create the file ``ItemsCssStyleSheet.scss`` (SCSS StyleSheet) ::
    
    $myDefaultColor: brown;
    $myItemStyleAColor: red;
    $myItemStyleBColor: black;
    $myItemStyleCColor: green;
    
    div.itemStyle {
      color: $myDefaultColor;
      font-size: 14px;
    }
    
    div.itemStyle.A {
      color: $myItemStyleAColor;
      font-size: 16px;
    }
    
    div.itemStyle.B {
      color: $myItemStyleBColor;
      font-size: 12px;
    }
    
    div.itemStyle.C {
      color: $myItemStyleCColor;
      font-size: 16px;
    }
    
    
- Create the file ``StylingComponentCssStylesheet.js`` (Child Component) ::
    
    import React, {Component} from 'react';
    import './App.css';
    import './ItemsCssStyleSheet.scss';
    
    class StylingComponentCssStylesheet extends Component {
      render () {
        return (
          <div className="App">
            <h4> Styling Component (Sass stylesheet)</h4>
            <div className="itemStyle">
              <div><b>Item1:</b> <em>Default Style</em></div>
              <div className="itemStyle A"><b>Item2:</b> <em>itemStyle A</em></div>
              <div className="itemStyle B"><b>Item3:</b> <em>itemStyle B</em></div>
              <div className="itemStyle C"><b>Item4:</b> <em>itemStyle C</em></div>
              <div className="itemStyle"><b>Item5:</b> <em>Default Style</em></div>
            </div>
          </div>
        );
      }
    }
    
    export default StylingComponentCssStylesheet;
    
    
- Edit the file ``App.js`` (Parent Component) ::
    
    import './App.css';
    import StylingComponentCssStylesheet from './StylingComponentCssStylesheet';
    
    function App () {
      return (
        <div className="App">
          <StylingComponentCssStylesheet />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. figure:: images/tut07/tut07-react-component-styling-sass-style.png
       :align: center
       :class: sd-my-2
       :alt: Styling Component (Sass stylesheet)
       
       :custom-color-primary-bold:`Styling Component (Sass stylesheet)`
    
