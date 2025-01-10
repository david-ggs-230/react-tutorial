.. _subsection-list-character:

.. role:: custom-color-primary-bold
   :class: sd-text-primary sd-font-weight-bold 

.. rst-class:: title-center h1
   
Preface


**************************************************************************************************
Document SubStructures
**************************************************************************************************

#. ``###########`` with overline, for parts
#. ``***********`` with overline, for chapters
#. ``===========`` for sections
#. ``-----------`` for subsections
#. ``^^^^^^^^^^^`` for subsubsections
#. ``"""""""""""`` for paragraphs

**************************************************************************************************
Build Command
**************************************************************************************************
    
    
    .. code-block:: sh
       :linenos:
       
       # Activate .venv
       .venv\Scripts\activate
       # navigate to docs folder
       cd docs
       # clean
       make clean
       # build html
       make html
       # clean and build
       make clean && make html
       
