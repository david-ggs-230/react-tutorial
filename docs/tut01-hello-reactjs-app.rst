.. _tut01-hello-reactjs-app:

.. rst-class:: title-center h1
   
Hello ReactJS App

##################################################################################################
Tut01-Hello ReactJS App
##################################################################################################
    
**************************************************************************************************
Setup ReactJS App Environment
**************************************************************************************************

- Move inside a project folder:
- Create a ReactJS App <tut01-hello-reactjs-app>::
    
    yarn create react-app tut01-hello-reactjs-app
    
- Move inside the ReactJS App folder <tut01-hello-reactjs-app>::
    
    cd tut01-hello-reactjs-app
    
- Run the ReactJS App <tut01-hello-reactjs-app>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running
    
    .. figure:: images/tut01/tut01-reactjs-app-init.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        
    
**************************************************************************************************
Modify the React Application
**************************************************************************************************

- Move inside the ReactJS App folder <tut01-hello-reactjs-app/src>::
    
    cd tut01-hello-reactjs-app/src
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //Disable test
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- open the file ``App.js``, Replace all the content inside the <div className="App"> with a <h1> element. ::
    
    import logo from './logo.svg';
    import './App.css';
    
    function App() {
      return (
        <div className="App">
            <h1>Hello ReactJS App!</h1>
        </div>
      );
    }
    
    export default App;
    
- Run the ReactJS App <tut01-hello-reactjs-app>::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running
    
    .. figure:: images/tut01/tut01-hello-reactjs-app.png
        :align: center
        :class: sd-mb-2
        :width: 80%
        