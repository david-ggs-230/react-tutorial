.. _install-python:

.. rst-class:: title-center h1
   
##################################################################################################
Install Python
##################################################################################################


**************************************************************************************************
Install python
**************************************************************************************************

#. 访问 Python 官方下载页面，挑选一个适合的版本下载。
#. 双击安装程序，按照屏幕上的提示操作。别忘了勾选「Add Python to PATH」选项，自动将 Python 路径添加到 PATH 环境变量中。
#. 可以直接点击「Install Now」进行标准安装；要定制安装选项，包括选择安装路径以及设置其他高级选项，就选择「Customize installation」。

    .. code-block:: bat
       :linenos:
       
       # 验证 Python 安装
       python --version
       python -V
    

**************************************************************************************************
Install Python PIP
**************************************************************************************************

#. Download the get-pip.py (https://bootstrap.pypa.io/get-pip.py) file
#. Run `python get-pip.py`
    
    
    .. code-block:: bat
       :linenos:
       
       # Install PIP
       python get-pip.py
       
       # PIP Verification
       pip -V
       pip --version
       
       # Update PIP
       python -m pip install --upgrade pip
       
       
##################################################################################################
虚拟环境管理
##################################################################################################


**************************************************************************************************
使用venv创建虚拟隔离环境
**************************************************************************************************

#. Create the <project> folder.
#. Navigate to the <project> folder.
#. 使用venv创建虚拟隔离环境.
    
    .. code-block:: sh
       :linenos:
       
       # 在当前目录下创建.venv目录
       python -m venv .venv  #create a Python virtual environment
       

**************************************************************************************************
激活虚拟环境
**************************************************************************************************
    
    .. code-block:: sh
       :linenos:
       
       # windows
       .venv\Scripts\activate.bat # activate the Python virtual environment
       

**************************************************************************************************
在虚拟环境下安装包，启动项目
**************************************************************************************************
    
    .. code-block:: sh
       :linenos:
       
       # windows
       pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U sphinx sphinx_rtd_theme myst-parser sphinx-autobuild sphinx-design # Installing py packages
       

##################################################################################################
自动生成环境配置文件requirements.txt
##################################################################################################


**************************************************************************************************
Python环境依赖的所有第三方库requirements.txt
**************************************************************************************************

#. Open Terminal
#. Navigate to the any folder
#. 生成本地环境所有依赖
#. pip freeze > requirements.txt
    
    .. code-block:: sh
       :linenos:
       
       # open terminal
       pip freeze > requirements.txt
       

**************************************************************************************************
Python当前项目依赖的所有第三方库requirements.txt
**************************************************************************************************

#. Open Terminal
#. Navigate to the <project> folder
#. 在导出当前项目使用的类库时，先定位到项目根目录，然后调用 pipreqs ./ --encoding=utf8 命令，该命令避免编码错误，并自动在根目录生成 requirements.txt 文件。
#. pipreqs ./
    
    .. code-block:: sh
       :linenos:
       
       # Install pipreqs package
       pip install pipreqs
       # 当前项目使用的类库导出生成为requirements.txt。
       pipreqs ./
       # 该命令避免编码错误，
       pipreqs ./ --encoding=utf8
       
       

**************************************************************************************************
安装环境配置文件requirements.txt
**************************************************************************************************


#. 最好先建一个新环境，做好环境隔离
#. pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple 
    
    .. code-block:: sh
       :linenos:
       
       # Install requirements.txt
       pip install -r requirements.txt 
       # OR
       pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple 
       
**************************************************************************************************
Tutorial: Creating and maintaining a requirements.txt file
**************************************************************************************************

==================================================================================================
Activate Your Virtual Environment
==================================================================================================

    .. code-block:: sh
       :linenos:
       
       # Create a virtual environment 
       python -m venv myenv
       
       # Activate the virtual environment
       
       # Windows
       myenv\Scripts\activate
       # macOS and Linux
       source myenv/bin/activate
       

==================================================================================================
Install Dependencies
==================================================================================================

    .. code-block:: sh
       :linenos:
       
       # Install Dependencies
       pip install package-name
       # i.e. pip install pandas
       

==================================================================================================
Generate the requirements.txt File
==================================================================================================

    .. code-block:: sh
       :linenos:
       
       # Generate the requirements.txt File
       pip freeze > requirements.txt
       

==================================================================================================
Review your requirement.txt file
==================================================================================================

#. Open the requirement.txt in a text editor
#.

==================================================================================================
Generate requirements.txt in Python Using pipreqs
==================================================================================================
    pipreqs is a tool that generates a requirements.txt file for your Python project based on imports in your project and not just the packages installed in your Python environment. This often results in a cleaner and more accurate requirements.txt file.
    
--------------------------------------------------------------------------------------------------
Installing pipreqs
--------------------------------------------------------------------------------------------------

    .. code-block:: sh
       :linenos:
       
       # Installing pipreqs
       pip install pipreqs
       
--------------------------------------------------------------------------------------------------
Generating requirements.txt with pipreqs
--------------------------------------------------------------------------------------------------

    .. code-block:: sh
       :linenos:
       
       # Generating requirements.txt with pipreqs
       pipreqs /path/to/project
       
       # Force ignore .venv
       pipreqs --ignore .venv --force
       
==================================================================================================
Install Packages Using PIP With requirements.txt File in Python
==================================================================================================

    .. code-block:: sh
       :linenos:
       
       # Installing packages
       pip install -r requirements.txt -i https://xxxx
       

