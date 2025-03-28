.. _tut08-react-router:


.. role:: custom-color-primary
   :class: sd-text-primary
   
.. role:: custom-color-primary-underline
   :class: sd-text-primary sd-text-decoration-line-underline
   
.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold

.. rst-class:: title-center h1
   
React Router

##################################################################################################
Tut08-React Router
##################################################################################################

**************************************************************************************************
Create Test App Folder Structure
**************************************************************************************************

- Move inside a project folder:
- Create React App <tut08-react-router> ::
    
    yarn create react-app tut08-react-router
    
- Move inside the ReactJS App/src folder <tut08-react-router/src> ::
    
    cd tut08-react-router/src
    
- Install React Router ::
    
    # yarn add react-router-dom or npm install react-router-dom --save
    yarn add -D react-router-dom
    
- Disable the unit test: open the file ``App.test.js``, make modifications ::
    
    import { render, screen } from '@testing-library/react';
    import App from './App';
    
    test('renders learn react link', () => {
      //render(<App />);
      //const linkElement = screen.getByText(/learn react/i); 
      //expect(linkElement).toBeInTheDocument();
    });
    
- open the file ``App.js``, and make modifications.
- Run the ReactJS App <tut08-react-router> ::
    
    yarn start
    
- open your browser and go to http://localhost:3000 to see your React app running

**************************************************************************************************
React Router
**************************************************************************************************

React Router provides several components to help manage navigation and routing in a React application. The primary components for handling routing and navigation are:
    
    - BrowserRouter (or Router for custom history) - Router is th top level component. It encloses the entire application.
    - Route − The Route component is used to define which components to render based on the current URL path ::
        
        <Route path="/home" element={<Home />} />
        
    - Link - The Link component is used to create navigational links in the app that change the URL when clicked, without causing a full page reload. It's a replacement for the traditional <a> tag for navigation in a React SPA. ::
        
        # Here, to attribute is used to set the target url.
        <Link to="/">Home</Link>
        
    - Routers - Routers is used to group Route components, rendering the first Route or Redirect that matches the current location.  ::
        
        <Routers>
          <Route path="/home" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/not-found" element={<NotFound />} /> 
          {/* Fallback route for 404 */}
          <Route path="*" element={<NotFound />} /> 
        </Routers>
        
    - Redirect - Redirects the user to a different route when a certain condition is met (e.g., after a login).
    - useHistory, useLocation, useParams, useRouteMatch - These hooks allow you to access the history, location, route parameters, and match data in functional components.
    
    
==================================================================================================
Top Level Routing
==================================================================================================

To create an application with multiple page routes, let's first start with the file structure.

Within the src folder, we'll create a folder named pages with several files and each file will contain a very basic React component.

Routing Components structure :
    
    - Home
    - About
    - NotFound
    
- Move inside the ReactJS App/src folder <tut08-react-router/src> ::
    
    cd tut08-react-router/src
    
- Create the file ``./pages/About.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function About() {
      return <h2 className='App'>About Page</h2>;
    }
    
    export default About;
    
- Create the file ``./pages/Home.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function Home() {
      return <h2 className='App'>Home Page</h2>;
    }
    
    export default Home;
    
- Create the file ``./pages/NotFound.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function NotFound() {
      return <h2 className='App'>Page Not Found</h2>;
    }
    
    export default NotFound;
    
- Edit the file ``App.js`` ::
    
    import React from 'react';
    import { BrowserRouter, Route, Routes, Link } from 'react-router-dom';
    import Home from './pages/Home';
    import About from './pages/About';
    import NotFound from './pages/NotFound';
    
    function App() {
      return (
        <BrowserRouter>
          <div>
            <nav>
            <ul style={{ listStyle: "none" }}>
                <li><Link to="/">Home</Link></li>
                <li><Link to="/about">About</Link></li>
                <li><Link to="/non-existent">Non-existent</Link></li>
              </ul>
            </nav>
    
            <Routes>
              {/* Define routes */}
              <Route exact path="/" element={<Home />} /> 
              <Route path="/about" element={<About />} /> 
              <Route path="/non-existent" element={<NotFound />} /> 
              {/* Fallback route for 404 */}
              <Route path="*" element={<NotFound />} /> 
            </Routes>
          </div>
        </BrowserRouter>
      );
    }
    
    export default App;
    
- Screenshot
    
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-top-level-routing-home.png
               :align: center
               :class: sd-mb-1
               :alt: Home Page
               
               :custom-color-primary-bold:`Home Page`, Click :custom-color-primary-underline:`Home` link to show
            
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-top-level-routing-about.png
               :align: center
               :class: sd-my-0
               :alt: About Page
               
               :custom-color-primary-bold:`About Page`, Click :custom-color-primary-underline:`About` link to show
            
    
==================================================================================================
Nested Routing
==================================================================================================

In React Router v6 and beyond, the concept of "outlets" is introduced for handling nested routes in a more intuitive way. An outlet is used in a parent component to render its child routes when their path matches. 

Nested Routing Components structure :
    
    - Home
    - About
    - Dashboard
        
        - Profile
        - Settings
        
    - NotFound
    
- Move inside the ReactJS App/src folder <tut08-react-router/src> ::
    
    cd tut08-react-router/src
    
- Create the file ``./pages/About.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function About() {
      return <h2 className='App'>About Page</h2>;
    }
    
    export default About;
    
- Create the file ``./pages/Home.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function Home() {
      return <h2 className='App'>Home Page</h2>;
    }
    
    export default Home;
    
- Create the file ``./pages/NotFound.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function NotFound() {
      return <h2 className='App'>Page Not Found</h2>;
    }
    
    export default NotFound;
    
- Create the file ``./pages/Navigate.js`` ::
    
    import React from "react";
    import { Outlet, Link } from "react-router-dom";
    
    function Navigate() {
      return (
        <div>
          <ul style={{ listStyle: "none" }}>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
                <Link to="/dashboard">Dashboard</Link>
            </li>
            <li>
              <Link to="/not-found">Not Found</Link>
            </li>
          </ul>
        
          <Outlet />
        </div>
      );
    }
    export default Navigate;
    
- Create the file ``./pages/Dashboard.js`` ::
    
    import React from 'react';
    import { Link, Outlet } from 'react-router-dom';
    import './../App.css';
    
    const Dashboard = () => {
      return (
        <div className='App'>
          <h2>Dashboard</h2>
          <nav>
            <ul style={{ listStyle: "none" }}>
              <li>
                <Link to="profile">Profile</Link>
              </li>
              <li>
                <Link to="settings">Settings</Link>
              </li>
            </ul>
          </nav>
          <Outlet />
        </div>
      );
    };
    
    export default Dashboard;
    
- Create the file ``./pages/Profile.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    const Profile = () => {
      return <h2 className='App'>Profile</h2>;
    };
    
    export default Profile;
    
- Create the file ``./pages/Settings.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    const Settings = () => {
      return <h2 className='App'>Settings</h2>;
    };
    
    export default Settings;
    
- Edit the file ``App.js`` ::
    
    import React from 'react';
    import { BrowserRouter, Route, Routes } from 'react-router-dom';
    import Home from './pages/Home';
    import About from './pages/About';
    import Dashboard from './pages/Dashboard';
    import Profile from './pages/Profile';
    import Settings from './pages/Settings';
    import NotFound from './pages/NotFound';
    import Navigate from './pages/Navigate';
    
    function App() {
      return (
        <BrowserRouter>
            <Routes>
              {/* Define routes */}
              <Route path="/" element={<Navigate />}>
                {/* Nested Routes */}
                <Route path="/" element={<Home />} /> 
                <Route path="/about" element={<About />} /> 
                <Route path="/dashboard" element={<Dashboard />}>
                  {/* Nested Routes */}
                  <Route path="profile" element={<Profile />} />
                  <Route path="settings" element={<Settings />} />
                </Route>
                <Route path="/non-existent" element={<NotFound />} /> 
                {/* Fallback route for 404 */}
                <Route path="*" element={<NotFound />} /> 
              </Route>
            </Routes>
        </BrowserRouter>
      );
    }
    
    export default App;
    
- Screenshot
    
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-nested-routing-dashboard.png
               :align: center
               :class: sd-mb-1
               :alt: Dashboard Page
               
               :custom-color-primary-bold:`Dashboard Page`, Click :custom-color-primary-underline:`Dashboard` link to show
            
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-nested-routing-profile.png
               :align: center
               :class: sd-my-0
               :alt: Dashboard/Profile Page
               
               :custom-color-primary-bold:`Dashboard/Profile Page`, Click :custom-color-primary-underline:`Profile` link to show
            
    
==================================================================================================
Dynamic Routing
==================================================================================================

React Router allows you to dynamically render components based on the URL, which is essential for creating dynamic, parameterized routes. Configure dynamic routes by using React Router’s Route component, where the path can include dynamic parameters, such as :productId, which will be captured and passed to the component.

Dynamic Routing Components structure :
    
    - Home
    - About
    - Dashboard
        
        - Profile
        - Settings
        
    - Products
        
        - Product 1
        - Product 2
        - Product 3
        
    - NotFound
    
- Move inside the ReactJS App/src folder <tut08-react-router/src> ::
    
    cd tut08-react-router/src
    
- Create the file ``./pages/About.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function About() {
      return <h2 className='App'>About Page</h2>;
    }
    
    export default About;
    
- Create the file ``./pages/Home.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function Home() {
      return <h2 className='App'>Home Page</h2>;
    }
    
    export default Home;
    
- Create the file ``./pages/NotFound.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    function NotFound() {
      return <h2 className='App'>Page Not Found</h2>;
    }
    
    export default NotFound;
    
- Create the file ``./pages/Navigate.js`` ::
    
    import React from "react";
    import { Outlet, Link } from "react-router-dom";
    
    function Navigate() {
      return (
        <div>
          <ul style={{ listStyle: "none" }}>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
                <Link to="/dashboard">Dashboard</Link>
            </li>
            <li>
                <Link to="/products">Products</Link>
            </li>
            <li>
              <Link to="/not-found">Not Found</Link>
            </li>
          </ul>
        
          <Outlet />
        </div>
      );
    }
    export default Navigate;
    
- Create the file ``./pages/Dashboard.js`` ::
    
    import React from 'react';
    import { Link, Outlet } from 'react-router-dom';
    import './../App.css';
    
    const Dashboard = () => {
      return (
        <div className='App'>
          <h2>Dashboard</h2>
          <nav>
            <ul style={{ listStyle: "none" }}>
              <li>
                <Link to="profile">Profile</Link>
              </li>
              <li>
                <Link to="settings">Settings</Link>
              </li>
            </ul>
          </nav>
          <Outlet />
        </div>
      );
    };
    
    export default Dashboard;
    
- Create the file ``./pages/Profile.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    const Profile = () => {
      return <h2 className='App'>Profile</h2>;
    };
    
    export default Profile;
    
- Create the file ``./pages/Settings.js`` ::
    
    import React from 'react';
    import './../App.css';
    
    const Settings = () => {
      return <h2 className='App'>Settings</h2>;
    };
    
    export default Settings;
    
- Create the file ``./pages/Products.js`` ::
    
    import React from 'react';
    import { Link, Outlet } from 'react-router-dom';
    import './../App.css';
    
    const Products = (props) => {
      return (
        <div className='App'>
          <h2>Products</h2>
          <nav>
            <ul style={{ listStyle: "none" }}>
              <li>
                <Link to="/products/1">Product 1</Link>
              </li>
              <li>
                <Link to="/products/2">Product 2</Link>
              </li>
              <li>
                <Link to="/products/3">Product 3</Link>
              </li>
            </ul>
          </nav>
          <Outlet />
        </div>
      );
    };
    
    export default Products;
    
- Create the file ``./pages/ProductDetail.js`` ::
    
    import React from 'react';
    import { useParams } from 'react-router-dom';
    import './../App.css';
    
    function ProductDetail() {
      const { productId } = useParams();
      return <h2 className='App'>Product ID: {productId}</h2>;
    }
    
    export default ProductDetail;
    
- Edit the file ``App.js`` ::
    
    import React from 'react';
    import { BrowserRouter, Route, Routes } from 'react-router-dom';
    import Home from './pages/Home';
    import About from './pages/About';
    import Dashboard from './pages/Dashboard';
    import Profile from './pages/Profile';
    import Settings from './pages/Settings';
    import NotFound from './pages/NotFound';
    import Navigate from './pages/Navigate';
    import Products from './pages/Products';
    import ProductDetail from './pages/ProductDetail';
    
    function App() {
      return (
        <BrowserRouter>
            <Routes>
              {/* Define routes */}
              <Route path="/" element={<Navigate />}>
                <Route path="/" element={<Home />} /> 
                <Route path="/about" element={<About />} /> 
                <Route path="/dashboard" element={<Dashboard />}>
                  {/* Nested Routes */}
                  <Route path="profile" element={<Profile />} />
                  <Route path="settings" element={<Settings />} />
                </Route>
                <Route path="/products" element={<Products />}>
                  {/* Dynamic route */}
                  <Route path="/products/:productId" element={<ProductDetail />} />
                </Route>
                <Route path="/non-existent" element={<NotFound />} /> 
                {/* Fallback route for 404 */}
                <Route path="*" element={<NotFound />} /> 
              </Route>
            </Routes>
        </BrowserRouter>
      );
    }
    
    export default App;
    
- Screenshot
    
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-dynamic-routing-products.png
               :align: center
               :class: sd-mb-1
               :alt: Products Page
               
               :custom-color-primary-bold:`Products Page`, Click :custom-color-primary-underline:`Products` link to show
            
        .. grid-item::
            
            .. figure:: images/tut08/tut08-react-router-dynamic-routing-products-product2.png
               :align: center
               :class: sd-my-0
               :alt: Products/Product 2 Page
               
               :custom-color-primary-bold:`Products/Product 2 Page`, Click :custom-color-primary-underline:`Product 2` link to show
            