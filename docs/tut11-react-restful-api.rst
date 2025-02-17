.. _tut11-react-restful-api:


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
   
React and RESTful API

##################################################################################################
Tut11-React and RESTful API
##################################################################################################

Integrating RESTful APIs with React enhances the functionality of web applications by enabling them to fetch and update data dynamically. This integration facilitates a seamless user experience, ensuring that the application remains responsive and up-to-date. 

Make API Requests in React: 
    
    - Using the `fetch` API − The fetch API is a built-in JavaScript method for making network requests.
    - Using `axios` for HTTP Requests − `axios` is a popular library for making HTTP requests.
    
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
Creating a REST API Server
**************************************************************************************************

JSON-Server is an npm(Node Package Manager) module that allows you to create a mock REST API using just a JSON file. It is highly useful for prototyping, testing, or building front-end applications without needing a complex back-end infrastructure. Data is transferred in JSON(JavaScript Object Notation) format between client and server using HTTP methods like GET, POST, PUT, PATCH, and DELETE.

How to Set Up JSON-Server
    
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

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
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

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
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

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
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

- Move inside the ReactJS App/src folder <tut10-react-form/src> ::
    
    cd tut10-react-form/src
    
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
            
    