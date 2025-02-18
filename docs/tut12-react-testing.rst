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
Running tests with Jest
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
    

**************************************************************************************************
Testing pure functions
**************************************************************************************************

A pure function has a consistent output value for a given set of parameter values. These functions depend only on the function parameters and nothing outside the function, and also don’t change any argument values passed into them. 

A test is defined using Jest’s test function ::
    
    # normal function
    test('test name', () => {
        // test implementation
    });
    
    # Asynchronous function
    test('test name', async () => {
        // test implementation
    });
    
    
    - Step 1: Install JSON-Server ::
        
        # npm install
        npm install json-server@0.17.3
        # yarn add  json-server@0.17.3
        
    - Step 2: Create a JSON Data File <db.json> ::
        
        {
            "posts": [
                {
                    "id": 1,
                    "title": "JSON-Server",
                    "author": "Amit"
                },
                {
                    "id": 2,
                    "title": "Node.js",
                    "author": "Mohit"
                }
            ],
            "comments": [
                {
                    "id": 1,
                    "body": "Great post!",
                    "postId": 1
                },
                {
                    "id": 2,
                    "body": "Informative!",
                    "postId": 2
                }
            ],
            "profile": {
                "name": "Amit Kumar"
            }
        }
        
    - Step 3: Start JSON-Server ::
        
        json-server --watch db.json --port 3001 --delay 2000
        
    
**************************************************************************************************
Make API Requests in React
**************************************************************************************************

==================================================================================================
The Fetch API
==================================================================================================

The Fetch API is a modern interface for making HTTP requests in the browser. It provides a more powerful and flexible way to handle network requests compared to older techniques like XMLHttpRequest. The fetch function is used to make a GET request to the specified API endpoint, and the response is converted to JSON using response.json().

- Making GET Requests
    
    - GET request ::
        
        const [data, setData] = useState([]);
        
        useEffect(() => {
          const fetchData = async () => {
            try {
              const response = await fetch('http://localhost:3001/posts');
              const result = await response.json();
              setData(result);
            } catch (error) {
              console.error('Error fetching data:', error);
            }
          };  
          fetchData();
        }, []);
        
    - GET request with query parameters ::
        
        const [data, setData] = useState([]);
        const [loading, setLoading] = useState(true);
        
        // with setTimeout
        useEffect(() => {
          const fetchData = async () => {
            try {
              // Simulating a delay to show loading state
              setTimeout(async () => {
                const response = await fetch('http://localhost:3001/posts?id=1');
                const result = await response.json();
                setData(result);
                setLoading(false);
              }, 1000);
            } catch (error) {
              console.error('Error fetching data:', error);
              setLoading(false);
            }
          };
        
          fetchData();
        }, []);
        
        
    - GET request with query parameters ::
        
        const [data, setData] = useState([]);
        const [loading, setLoading] = useState(true);
        
        useEffect(() => {
          const fetchData = async () => {
            fetch('http://localhost:3001/posts?id=1')
                    .then((response) => response.json())
                    .then((result) => {
                        setData(result);
                        setLoading(false);
                    })
                    .catch((err) => {
                        console.error('Error fetching data:', error);
                        setLoading(false);
                    });
          };
          
          fetchData();
        }, []);
        
- Making POST Requests
    
    - POST request ::
        
        const [posts, setPosts] = useState ([]);
        const [title, setTitle] = useState('');
        const [body, setBody] = useState('');
        // ...
        const addPosts = async (title, body) => {
           await fetch('http://localhost:3001/posts', {
              method: 'POST',
              body: JSON.stringify({
                 title: title,
                 body: body,
                 userId: Math.random().toString(36).slice(2),
              }),
              headers: {
                 'Content-type': 'application/json; charset=UTF-8',
              },
           })
              .then((response) => response.json())
              .then((data) => {
                 setPosts((posts) => [data, ...posts]);
                 setTitle('');
                 setBody('');
              })
              .catch((err) => {
                 console.log(err.message);
              });
        };
        
        const handleSubmit = (e) => {
           e.preventDefault();
           addPosts(title, body);
        };    
        
--------------------------------------------------------------------------------------------------
Making GET Requests
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut12-react-testing/src> ::
    
    cd tut12-react-testing/src
    
- Create the file ``./PostComponent.js`` ::
    
    import './App.css';
    
    function PostComponent (props) {
      return (
        <div className="App">
          <h2>ID: {props.id}</h2>
          <p>Title: {props.title}</p>
          <p>Author: {props.author}</p>
        </div>
      );
    }
    
    export default PostComponent;
    
- Create the file ``./GetPostListComponent.js`` ::
    
    import './App.css';
    import PostComponent from './PostComponent';
    import React, {useState, useEffect} from 'react';
    
    function GetPostListComponent () {
      const [posts, setPosts] = useState ([]);
      const [isLoading, setLoading] = useState (true);
      useEffect (() => {
        fetch ('http://localhost:3001/posts')
          .then (response => response.json ())
          .then (data => {
            console.log (data);
            setPosts (data);
            setLoading (false);
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      }, []);
      if (isLoading) {
        return (
          <div className="App">
            <h1>Post List</h1>
            <div>Loading ......</div>
          </div>
        );
      }
      return (
        <div className="App">
          <h1>Post List</h1>
          <ul>
            {posts.map (post => {
              return (
                <li key={post.id}>
                  <PostComponent
                    id={post.id}
                    author={post.author}
                    title={post.title}
                  />
                </li>
              );
            })}
          </ul>
    
        </div>
      );
    }
    
    export default GetPostListComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import GetPostListComponent from './GetPostListComponent';
    
    function App () {
      return (
        <div className="App">
          <GetPostListComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-get-home.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch`, loading homepage
            
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-get-list.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch`, post list
            
            
--------------------------------------------------------------------------------------------------
Making POST Requests
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut12-react-testing/src> ::
    
    cd tut12-react-testing/src
    
- Create the file ``./PostComponent.js`` ::
    
    import './App.css';
    
    function PostComponent (props) {
      return (
        <div className="App">
          <h2>ID: {props.id}</h2>
          <p>Title: {props.title}</p>
          <p>Author: {props.author}</p>
        </div>
      );
    }
    
    export default PostComponent;
    
- Create the file ``./PostPostListComponent.js`` ::
    
    import './App.css';
    import PostComponent from './PostComponent';
    import {useForm} from 'react-hook-form';
    import React, {useState, useEffect} from 'react';
    
    function PostPostListComponent () {
      const [posts, setPosts] = useState ([]);
      //const [title, setTitle] = useState ('');
      //const [author, setAuthor] = useState ('');
      const [isLoading, setLoading] = useState (true);
      const {
        register,
        handleSubmit,
        formState: {isSubmitting, isDirty, isValid},
        reset,
      } = useForm ();
      useEffect (() => {
        fetch ('http://localhost:3001/posts')
          .then (response => response.json ())
          .then (data => {
            console.log (data);
            setPosts (data);
            setLoading (false);
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      }, []);
      const addPosts = async (id, title, author) => {
        await fetch ('http://localhost:3001/posts', {
          method: 'POST',
          body: JSON.stringify ({
            id: id,
            title: title,
            author: author,
          }),
          headers: {
            'Content-type': 'application/json; charset=UTF-8',
          },
        })
          .then (response => response.json ())
          .then (data => {
            setPosts (posts => [...posts, data]);
            setLoading (false);
            reset ();
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      };
      const onFormSubmit = data => {
        for (let post of posts) {
          if (Number (data.id) === Number (post.id)) {
            alert ('id:' + data.id + ' already exists!');
            return;
          }
        }
        addPosts (data.id, data.title, data.author);
      };
      return (
        <div className="App">
          <form noValidate onSubmit={handleSubmit (onFormSubmit)}>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="id"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                ID
              </label>
              <input
                type="text"
                id="id"
                name="id"
                placeholder="Enter id"
                {...register ('id')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="title"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                Title
              </label>
              <input
                type="text"
                id="title"
                name="title"
                placeholder="Enter title"
                {...register ('title')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="author"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                Author
              </label>
              <input
                type="text"
                id="author"
                name="author"
                placeholder="Enter author"
                {...register ('author')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <input
                type="submit"
                value="Submit"
                disabled={isSubmitting || !isDirty || !isValid}
              />
            </div>
          </form>
    
          <h1>Post List</h1>
          <ul>
            {isLoading && <p>PostList Loading ......</p>}
            {posts.map (post => {
              return (
                <li key={post.id}>
                  <PostComponent
                    id={post.id}
                    author={post.author}
                    title={post.title}
                  />
                </li>
              );
            })}
          </ul>
        </div>
      );
    }
    
    export default PostPostListComponent;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import PostPostListComponent from './PostPostListComponent';
    
    function App () {
      return (
        <div className="App">
          <PostPostListComponent />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-post-home.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (POST)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (POST)`, post form page
            
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-post-addpost.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (POST)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (POST)`, add post
            
    
==================================================================================================
The axios API
==================================================================================================

Axios is an HTTP client library based on promises that makes it simple to send asynchronous HTTP requests to REST endpoints. 

- Install Axios by running the following command ::
    
    # npm
    npm install axios
    # yarn
    yarn add axios
    
- Create an instance ::
    
    import axios from "axios";
    
    const client = axios.create({
       baseURL: 'http://localhost:3001/posts' 
    });
    
- Perform a GET Request in React With Axios ::
    
    useEffect(() => {
       client.get('?id=10').then((response) => {
          setPosts(response.data);
       });
    }, []);
    
- Perform a POST Request in React With Axios ::
    
    const addPosts = (title, body) => {
       client
          .post('', {
             title: title,
             body: body,
          })
          .then((response) => {
             setPosts((posts) => [response.data, ...posts]);
          });
    };
    
- Perform a DELETE Request in React With Axios ::
    
    const deletePost = (id) => {
       client.delete(`${id}`);
       setPosts(
          posts.filter((post) => {
             return post.id !== id;
          })
       );
    };
    
- Use Async/Await in Axios ::
    
    import React, { useState, useEffect } from 'react';
    
    const App = () => {
       const [title, setTitle] = useState('');
       const [body, setBody] = useState('');
       const [posts, setPosts] = useState([]);
    
       // GET with Axios
       useEffect(() => {
          const fetchPost = async () => {
             let response = await client.get('?_limit=10');
             setPosts(response.data);
          };
          fetchPost();
       }, []);
    
       // Delete with Axios
       const deletePost = async (id) => {
          await client.delete(`${id}`);
          setPosts(
             posts.filter((post) => {
                return post.id !== id;
             })
          );
       };
    
       // Post with Axios
       const addPosts = async (title, body) => {
          let response = await client.post('', {
             title: title,
             body: body,
          });
          setPosts((posts) => [response.data, ...posts]);
       };
    
       const handleSubmit = (e) => {
          e.preventDefault();
          addPosts(title, body);
       };
    
       return (
          // ...
       );
    };
    
    export default App;
    
        
--------------------------------------------------------------------------------------------------
Making GET Requests
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut12-react-testing/src> ::
    
    cd tut12-react-testing/src
    
- Create the file ``./PostComponent.js`` ::
    
    import './App.css';
    
    function PostComponent (props) {
      return (
        <div className="App">
          <h2>ID: {props.id}</h2>
          <p>Title: {props.title}</p>
          <p>Author: {props.author}</p>
        </div>
      );
    }
    
    export default PostComponent;
    
- Create the file ``./PostListComponentAxiosGet.js`` ::
    
    import './App.css';
    import PostComponent from './PostComponent';
    import axios from 'axios';
    import React, {useState, useEffect} from 'react';
    
    function PostListComponentAxiosGet () {
      const [posts, setPosts] = useState ([]);
      const [isLoading, setLoading] = useState (true);
      useEffect (() => {
        axios
          .get ('http://localhost:3001/posts')
          .then (response => {
            console.log (response.data);
            setPosts (response.data);
            setLoading (false);
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      }, []);
      if (isLoading) {
        return (
          <div className="App">
            <h1>Post List</h1>
            <div>Loading ......</div>
          </div>
        );
      }
      return (
        <div className="App">
          <h1>Post List</h1>
          <ul>
            {posts.map (post => {
              return (
                <li key={post.id}>
                  <PostComponent
                    id={post.id}
                    author={post.author}
                    title={post.title}
                  />
                </li>
              );
            })}
          </ul>
    
        </div>
      );
    }
    
    export default PostListComponentAxiosGet;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import PostListComponentAxiosGet from './PostListComponentAxiosGet';
    
    function App () {
      return (
        <div className="App">
          <PostListComponentAxiosGet />
        </div>
      );
    }
    
    export default App;
    

- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-axios-get-home.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (Axios Get)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (Axios Get)`, loading homepage
               
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-axios-get-list.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (Axios Get)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (Axios Get)`, post list
               
            
--------------------------------------------------------------------------------------------------
Making POST Requests
--------------------------------------------------------------------------------------------------

- Move inside the ReactJS App/src folder <tut12-react-testing/src> ::
    
    cd tut12-react-testing/src
    
- Create the file ``./PostComponent.js`` ::
    
    import './App.css';
    
    function PostComponent (props) {
      return (
        <div className="App">
          <h2>ID: {props.id}</h2>
          <p>Title: {props.title}</p>
          <p>Author: {props.author}</p>
        </div>
      );
    }
    
    export default PostComponent;
    
- Create the file ``./PostListComponentAxiosPost.js`` ::
    
    import './App.css';
    import PostComponent from './PostComponent';
    import axios from 'axios';
    import {useForm} from 'react-hook-form';
    import React, {useState, useEffect} from 'react';
    
    function PostListComponentAxiosPost () {
      const [posts, setPosts] = useState ([]);
      //const [title, setTitle] = useState ('');
      //const [author, setAuthor] = useState ('');
      const [isLoading, setLoading] = useState (true);
      const {
        register,
        handleSubmit,
        formState: {isSubmitting, isDirty, isValid},
        reset,
      } = useForm ();
      useEffect (() => {
        axios
          .get ('http://localhost:3001/posts')
          .then (response => {
            console.log (response.data);
            setPosts (response.data);
            setLoading (false);
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      }, []);
      const addPosts = async (id, title, author) => {
        await axios
          .post ('http://localhost:3001/posts', {
            id: id,
            title: title,
            author: author,
          })
          .then (data => {
            setPosts (posts => [
              ...posts,
              {
                id: id,
                title: title,
                author: author,
              },
            ]);
            setLoading (false);
            reset ();
          })
          .catch (err => {
            console.log (err.message);
            setLoading (false);
          });
      };
      const onFormSubmit = data => {
        for (let post of posts) {
          if (Number (data.id) === Number (post.id)) {
            alert ('id:' + data.id + ' already exists!');
            return;
          }
        }
        addPosts (data.id, data.title, data.author);
      };
      return (
        <div className="App">
          <form noValidate onSubmit={handleSubmit (onFormSubmit)}>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="id"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                ID
              </label>
              <input
                type="text"
                id="id"
                name="id"
                placeholder="Enter id"
                {...register ('id')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="title"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                Title
              </label>
              <input
                type="text"
                id="title"
                name="title"
                placeholder="Enter title"
                {...register ('title')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <label
                htmlFor="author"
                style={{
                  display: 'inline-block',
                  width: '3rem',
                  marginRight: '1.5rem',
                }}
              >
                Author
              </label>
              <input
                type="text"
                id="author"
                name="author"
                placeholder="Enter author"
                {...register ('author')}
              />
            </div>
            <div style={{marginTop: 10}}>
              <input
                type="submit"
                value="Submit"
                disabled={isSubmitting || !isDirty || !isValid}
              />
            </div>
          </form>
    
          <h1>Post List</h1>
          <ul>
            {isLoading && <p>PostList Loading ......</p>}
            {posts &&
              posts.map (post => {
                return (
                  <li key={post.id}>
                    <PostComponent
                      id={post.id}
                      author={post.author}
                      title={post.title}
                    />
                  </li>
                );
              })}
          </ul>
        </div>
      );
    }
    
    export default PostListComponentAxiosPost;
    
- Edit the file ``App.js`` ::
    
    import './App.css';
    import PostListComponentAxiosPost from './PostListComponentAxiosPost';
    
    function App () {
      return (
        <div className="App">
          <PostListComponentAxiosPost />
        </div>
      );
    }
    
    export default App;
    
- Screenshot
    
    .. grid:: 1 1 1 2
        
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-axios-post-home.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (Axios Post)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (Axios Post)`, post form page
            
        .. grid-item::
            
            .. figure:: images/tut11/tut11-react-restful-api-post-component-axios-post-addpost.png
               :align: center
               :class: sd-mb-1
               :alt: React RESTful API - Posts Fetch (Axios Post)
               
               :custom-color-primary-bold:`React RESTful API - Posts Fetch (Axios Post)`, add post
            
    