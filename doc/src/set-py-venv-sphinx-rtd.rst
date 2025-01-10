.. _set-py-venv-sphinx-rtd:

.. rst-class:: title-center h1
   
Set Sphinx Doc Environment

##################################################################################################
Create Sphinx Doc Project
##################################################################################################

**************************************************************************************************
Install sphinx packages
**************************************************************************************************

#. Create the doc folder.
#. Navigate to the doc folder.
#. Install py packages.
    
    .. code-block:: sh
       :linenos:
       
       python -m venv .venv  #create a Python virtual environment
       .venv\Scripts\activate.bat # activate the Python virtual environment
       pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U sphinx sphinx_rtd_theme myst-parser sphinx-autobuild sphinx-design # Installing py packages
    
**************************************************************************************************
Creating the documentation layout
**************************************************************************************************

    .. code-block:: sh
       :linenos:
       
       sphinx-quickstart docs
       cd docs && make html # Or sphinx-build -M html docs/source/ docs/build/
    
##################################################################################################
Sphinx rtd-theme configuration
##################################################################################################

**************************************************************************************************
Configure the conf.py file
**************************************************************************************************

    .. code-block:: cfg
       :caption: contents of the conf.py file
       :linenos:
       
       # contents of the conf.py file
       
       #!/usr/bin/env python3
       # -*- coding: utf-8 -*-
       
       # Configuration file for the Sphinx documentation builder.
       #
       # For the full list of built-in configuration values, see the documentation:
       # https://www.sphinx-doc.org/en/master/usage/configuration.html
       import sphinx_rtd_theme
       
       
       # -- Project information -----------------------------------------------------
       # https://www.sphinx-doc.org/en/master/usage/configuration.html#project-information
       
       project = 'Sphinx Doc Environment'
       copyright = '2024, Sphinx Doc'
       author = 'Sphinx Doc'
       release = '1.0.0'
       
       # -- General configuration ---------------------------------------------------
       # https://www.sphinx-doc.org/en/master/usage/configuration.html#general-configuration
       
       #extensions = []
       extensions = [
               'myst_parser',
               'sphinx_rtd_theme',
               "sphinx_design"
           ]
       
       templates_path = ['_templates']
       exclude_patterns = []
       myst_enable_extensions = ["colon_fence"]
       numfig = True
       
       # -- Options for HTML output -------------------------------------------------
       # https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-html-output
       
       #html_theme = 'alabaster'
       #html_static_path = ['_static']
       
       html_theme = "sphinx_rtd_theme"
       #html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
       #html_theme_path = ["."]
       html_static_path = ['_static']
       html_show_sourcelink = False
       html_css_files = [
           'css/custom-theme.css' 
           # 'css/bootstrap.min.css'
       ]
       html_js_files = [
           # 'css/bootstrap.min.js'
       ]
       html_theme_options = {
           # 'analytics_id': 'G-XXXXXXXXXX',  #  Provided by Google in your dashboard
           # 'analytics_anonymize_ip': False,
           
           
           'logo_only': False,
           #'display_version': True,
           'prev_next_buttons_location': 'bottom',
           'style_external_links': True,
           'vcs_pageview_mode': '',
           #'style_nav_header_background': 'white',
           # Toc options
           'collapse_navigation': True,
           'sticky_navigation': True,
           'navigation_depth': 6,
           'includehidden': True,
           'titles_only': False
       }
       
       html_context = {
           'display_github': False
       }
    

**************************************************************************************************
Configure the custom-theme.css file
**************************************************************************************************

    .. code-block:: cfg
       :caption: contents of the _static/css/custom-theme.css file
       :linenos:
       
       # contents of the _static/css/custom-theme.css file
       
       
       .wy-nav-content {
          max-width: 90%;
          background: #fcfcfc;
       }
       .wy-nav-content-wrap {
          background: #fcfcfc;
       }
       .rst-content {
           background-color: transparent;
       }
       .title-center h1 {
           font-size: 250%; 
           margin-top: 0;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
           text-align: center;
       }
       
       p.title-center.h2 {
           font-size: 200%;  
           margin-top: 0;
           text-align: center;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
       }
       
       p.title-center.h1 {
           font-size: 250%; 
           margin-top: 0;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
           text-align: center;
       }
       
       p.title-center.h6 {
           font-size: 100%;  
           margin-top: 0;
           text-align: center;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
       }
       
       
       p.title-left.h2 {
           font-size: 200%;  
           margin-top: 0;
           text-align: left;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
       }
       
       p.title-left.h1 {
           font-size: 250%; 
           margin-top: 0;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
           text-align: left;
       }
       
       p.title-left.h3 {
           font-size: 150%;  
           margin-top: 0;
           text-align: left;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
       }
       
       
       p.title-left.h4 {
           font-size: 125%;  
           margin-top: 0;
           text-align: left;
           font-weight: 700;
           font-family: Roboto Slab,ff-tisa-web-pro,Georgia,Arial,sans-serif;
       }
       
       
       .rst-content div.code-block-caption {
           text-align: left;
       }
       
       img.sd-svg-primary { filter: invert(.5) sepia(0.5) saturate(80) hue-rotate(208deg); }
       
       span.sd-text-decoration-line-underline {
           text-decoration-line: underline;
       }
       
       
