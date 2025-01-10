.. _set-py-venv-selenium:

.. rst-class:: title-center h1
   
Set Selenium Environment

##################################################################################################
Create Selenium Project
##################################################################################################

**************************************************************************************************
Install selenium packages
**************************************************************************************************

#. Create the <project> folder.
#. Navigate to the <project> folder.
#. Install py selenium packages.
    
    .. code-block:: sh
       :linenos:
       
       # create a Python virtual environment
       python -m venv .venv
       # activate the Python virtual environment
       .venv\Scripts\activate.bat
       # Update pip
       python -m pip install -U pip -i https://pypi.tuna.tsinghua.edu.cn/simple
       # Installing py packages
       pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U selenium 
       # Upgrade Selenium
       pip install --upgrade selenium
    
**************************************************************************************************
Check Selenium Python Version
**************************************************************************************************

    .. code-block:: sh
       :linenos:
       
       # Using the Command Line
       pip show selenium
       
       # Checking Installed Packages
       # Windows
       pip list | findstr selenium
       # Linux
       pip list | grep selenium
       
##################################################################################################
Download Chrome Binary and ChromeDriver
##################################################################################################

- Check Selenium Python Version
   
   - ``pip show selenium``
   
- Find supported Chrome Version
   
   - https://github.com/SeleniumHQ/selenium/blob/trunk/py/CHANGES
   - Find the matching Chrome version
       
       .. code-block:: cfg
          :linenos:
          
          Selenium 4.27.0
          * Add CDP for Chrome 131 and remove 128
          * Add Firefox CDP deprecation warnings (#14787)
          * Cleaned up Py doc sphinx warnings/errors and added README (#14191)
          * Added Deprecation of WebElement.get_attribute() per #13334 (#14675)
          * Fix TypeError when init Safari webdriver (#14699)
          * Set user_agent and extra_headers via ClientConfig (#14718)
          * Updated Handling for DetachedShadowRoot Exception (#14677)
          * Support FedCM commands (#14710)
          
- Download matching Chrome binary and Chrome Driver
   
   - https://googlechromelabs.github.io/chrome-for-testing/#stable
   - Find the matching Chrome and chromedriver
   - For Chrome 131 (Selenium 4.27.0), 
       
       - Chrome (Win64): https://storage.googleapis.com/chrome-for-testing-public/131.0.6778.85/win64/chrome-win64.zip
       - ChromeDriver (Win64): https://storage.googleapis.com/chrome-for-testing-public/131.0.6778.85/win64/chromedriver-win64.zip
       
       
##################################################################################################
Test Selenium Env Setup
##################################################################################################
   
   .. code-block:: python
      :linenos:
      
      from selenium import webdriver
      
      def processWebPage(url):
          driver = setup()
          driver.get(url)
      def setup():
          chromedriver_path = r'/path/to/chromedriver/binary'
          service = webdriver.ChromeService(executable_path=chromedriver_path)
      
          chromebinary_path = r'/path/to/chrome/binary'
          options = webdriver.ChromeOptions()
          options.binary_location = chromebinary_path
          options.unhandled_prompt_behavior = 'accept'
          options.page_load_strategy = 'normal'
          options.strict_file_interactability = True
          options.accept_insecure_certs = True
          options.timeouts = { 'script': 300000,
                               'pageLoad': 300000,
                               'implicit': 300000
                               }
      
          options.add_argument(r"--user-data-dir=</path/to/chrome-user-data-profile-folder>")
          options.add_experimental_option("detach", True)
          options.add_experimental_option("excludeSwitches", ["disable-popup-blocking", 'enable-automation'])
          options.add_experimental_option("prefs", {
              "download.default_directory": r'/path/to/download/folder',
              "download.prompt_for_download": False,
              "download.directory_upgrade": True
          })
      
          # Option 2: Set download path
          #     import os
          #     os.environ['DOWNLOAD_PATH'] = '/download/path'
          # Option 3:  Set download path
          #     from selenium.webdriver.chrome.service import Service
          #
      
          # options.add_argument("start-maximized")
          options.add_argument("window-size=1280,960")
          # options.add_argument("--headless")
          options.add_argument("--disable-extensions")
          options.add_argument("--disable-popup-blocking")
          options.add_argument("enable-strict-powerful-feature-restrictions")
          options.add_argument("disable-geolocation")
          options.add_argument("disable-notifications")
          options.add_argument("disable-infobars")
      
          # Pass DesiredCapabilities to ChromeOptions
          # options.set_capability('acceptInsecureCerts', True)
          # options.set_capability('browserName', 'chrome')
          # options.set_capability('unhandledPromptBehavior', 'ignore')
      
          driver = webdriver.Chrome(service=service, options=options)
      
          return driver
      
      def teardown(driver):
          driver.quit()
      
      processWebPage("url")
      
       
##################################################################################################
Save Selenium Project
##################################################################################################

#. Navigate to the <project> folder.
#. Generate the requirements.txt file::

    pip install pipreqs
    pipreqs --ignore .venv --force

#. Copy all .py files and the the requirements.txt file to a <new-project> folder
#. Navigate to the <new-project> folder
#. Install venv and dependencies::

    # create a Python virtual environment
    python -m venv .venv
    # activate the Python virtual environment
    .venv\Scripts\activate.bat
    # Installing py packages
    pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

