.. _reactjs-env-setup:

.. rst-class:: title-center h1
   
Setup ReactJS Environment

##################################################################################################
Install ReactJS on Windows
##################################################################################################

**************************************************************************************************
Setup Nodejs Environment
**************************************************************************************************

#. Download the LTS (Long Term Support) version for Windows
#. Run the Installer
#. Verify Node.js Installation ::
    
    # check the Node.js version
    node -v
    # check the npm version
    npm -v
    

**************************************************************************************************
Install ReactJS
**************************************************************************************************

- Create project folder:
    
    - Create Directory for React Projects::
        
        mkdir <new-react-project-folder>
    - Move inside the folder::
        
        cd  <new-react-project-folder>

- Create ReactJS App
    
    - Option 1: Using Create-React-App (CRA) ::
        
        # Install CRA Globally
        npm install -g create-react-app
        # Verify the installation
        create-react-app --version
        # Create the React App, The app name must be in lowercase
        create-react-app <new-react-app-name>
        
    - Option 2: Using npx ::
        
        # Create the React App, The app name must be in lowercase
        npx create-react-app <new-react-app-name>
        
    - Option 3: Using npm ::
        
        # Create the React App, The app name must be in lowercase
        npm init react-app <new-react-app-name>
        
    - Option 4: Using Vite::
        
        # Use the following command If using Vite:
        npm create vite@latest <new-react-app-name> -- --template react
        
    - Option 5: Using yarn ::
        
        # Install yarn
        npm install -g yarn
        # Create the React App Using yarn, The app name must be in lowercase
        yarn create react-app <new-react-app-name>
    
    
- Resolving Dependency Conflicts in Node.js if any
  
  .. code-block:: sh
    :linenos:
    
    # Use --legacy-peer-deps flag: 
    npm install --legacy-peer-deps
    # Use --force flag: 
    npm install --force
    # Manually install peer dependencies: 
    npm install react@15.7.0
    # Switch to Yarn: 
    yarn install
    # Clear npm cache and reinstall: 
    npm cache clean --force && rm -rf node_modules package-lock.json && npm install
    

**************************************************************************************************
Build and Run
**************************************************************************************************
  
  .. code-block:: sh
    :linenos:
    
    # Move inside the <new-react-app-name> folder
    cd  <new-react-app-name>
    # Run: npm start <or> yarn start 
    npm start 
    # Building the React App: npm run build <or> yarn build
    npm run build
    

**************************************************************************************************
Test ReactJS Env Setup
**************************************************************************************************

#. Create a test react-app project:
    
    - folder-name: react-app
    - app-name: env-test-app
    
#. Run the test app
#. Run command::
    
    # Create Directory <react-app> for the test React Project
    mkdir react-app
    # Move inside the folder
    cd react-app
    # Create the React App <env-test-app>
    npx create-react-app env-test-app
    # Move inside the folder
    cd env-test-app
    # Run
    npm start
    # Building the React App
    npm run build
    
    

##################################################################################################
Install ReactJS on Linux
##################################################################################################

`How to Install ReactJS on Linux <https://www.geeksforgeeks.org/how-to-install-reactjs-on-linux/>`_

**************************************************************************************************
Installation of Node.js
**************************************************************************************************

- Update System Package List
- Install Node.js
- Installation verification
- Install npm (Node Package Manager) if not Installed

  .. code-block:: sh
    :linenos:
    
    # Update System Package List
    sudo apt update
    # Install Node.js 
    sudo apt install nodejs 
    # nodejs Installation verification
    node -v 
    # Install npm (Node Package Manager) if not Installed
    sudo apt install npm
    # npm Installation verification
    npm -v 
    
**************************************************************************************************
Install ReactJS using Create React App
**************************************************************************************************

Create React App is a tool that allows you to set up a React project with a single command. It sets up a modern web development environment with a good default configuration.

- Create a new React applications, ``npx create react-app my-app``
- Navigate to Your Desired Directory for the React Application ``cd my-app``
- Starting the server ``npm start``
- open your browser and go to http://localhost:3000 to see your React app running

  .. code-block:: sh
    :linenos:
    
    # create a folder called my-app with all the files and configurations required for a React project
    npx create react-app my-app
    cd my-app 
    npm start
    

##################################################################################################
Install ReactJS on macOS
##################################################################################################

- `How to Install ReactJS on MacOS <https://www.geeksforgeeks.org/how-to-install-reactjs-on-macos/>`_
- `How to Install ReactJS on MacOS? <https://dev.to/code_jedi/how-to-install-reactjs-on-macos-4hio>`_

**************************************************************************************************
Installation of Node.js
**************************************************************************************************

- Download Node.js
    
    - Visit the official Node.js website.
    - Download the LTS (Long Term Support) version for macOS.
    
- Install Node.js and npm
    
    - Double-click on the .pkg file to open it
    - Simply follow the on-screen instructions to complete the installation.
    
- add /usr/local/bin to your $PATH on macOS, 
    
    - temporarily update your $PATH for the current session: ``export PATH=/usr/local/bin:$PATH``
    - To make the change permanent, add the line to your shell configuration file (e.g., .zshrc or .bash_profile) using a text editor. Then reload the shell configuration
    
- Verify Installation
  
  .. code-block:: sh
    :linenos:
    
    # nodejs Installation verification
    node -v 
    # npm Installation verification
    npm -v 
    
**************************************************************************************************
Install ReactJS using Create React App
**************************************************************************************************

Create React App is a tool that allows you to set up a React project with a single command. It sets up a modern web development environment with a good default configuration.

- in your project's directory by running: ``npm install --save react react-dom``
- Create a new React applications, ``npx create-react-app my-app``
- Navigate to Your Desired Directory for the React Application ``cd my-app``
- Starting the server ``npm start``
- open your browser and go to http://localhost:3000 to see your React app running

  .. code-block:: sh
    :linenos:
    
    # create a folder called my-app with all the files and configurations required for a React project
    npx create react-app my-app
    cd my-app 
    npm start
    
