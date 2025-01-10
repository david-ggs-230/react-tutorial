.. _set-py-venv-scrapy:

.. rst-class:: title-center h1
   
Set Scrapy Environment

##################################################################################################
Create Scrapy Project
##################################################################################################

**************************************************************************************************
Install scrapy packages
**************************************************************************************************

#. Create the <project> folder.
#. Navigate to the <project> folder.
#. Install py scrapy packages.::
    
    # create a Python virtual environment
    python -m venv .venv
    # activate the Python virtual environment
    .venv\Scripts\activate.bat
    # Update pip
    python -m pip install -U pip -i https://pypi.tuna.tsinghua.edu.cn/simple
    # Installing py packages
    pip install -U scrapy -i https://pypi.tuna.tsinghua.edu.cn/simple
    # Upgrade Scrapy
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U scrapy 
    
**************************************************************************************************
Check Scrapy Python Version
**************************************************************************************************

    ::
    
        # Using the Command Line
        pip show scrapy
        
        # Checking Installed Packages
        # Windows
        pip list | findstr Scrapy
        # Linux
        pip list | grep Scrapy
    
**************************************************************************************************
Creates a new Scrapy project
**************************************************************************************************

    ::
    
        # Using the Command Line
        # Installing py packages
        pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U scrapy
        # Creates a new Scrapy project
        scrapy startproject <projectname>
        # Navigate to the <projectname> folder
        # Generate a spider
        scrapy genspider <name> <domain> 
        

##################################################################################################
Test Scrapy Env Setup
##################################################################################################

#. Create the <project> folder.
#. Navigate to the <project> folder.
#. Creates a new Scrapy project::
    
    # Using the Command Line
    python -m venv .venv
    .venv\Scripts\activate.bat
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U scrapy
    scrapy startproject <projectname>
    # Navigate to the <projectname> folder
    cd <projectname>
    # Generate a spider
    # scrapy genspider <name> <domain>
    scrapy genspider books books.toscrape.com

#. Spider source code (books_spider.py)
  
  .. code-block:: python
    :caption: books_spider.py
    :linenos:
    
    # -*- coding: utf-8 -*-
    import scrapy
    
    class BookSpider(scrapy.Spider):
        name = "books"
    
        def start_requests(self):
            urls = [ 
                        "https://books.toscrape.com" 
                   ]
            for url in urls:
                yield scrapy.Request(url=url, callback=self.parse)
            
        def parse(self, response):
            # <li>
            #     <article class="product_pod">
            #         <h3>
            #            <a href="catalogue/a-light-in-the-attic_1000/index.html" title="A Light in the Attic">
            #               A Light in the Attic
            #            </a>
            #          </h3>
            #          <div class="product_price">
            #               <p class="price_color">£51.77</p>
            #               <p class="instock availability">
            #                   <i class="icon-ok"></i> In stock
            #               </p>
            #          </div>
            #
    
            for book in response.css('li article.product_pod'):
                name = book.xpath('./h3/a/@title').extract_first()
                price = book.css('p.price_color::text').extract_first()
    
                yield {
                    'name': name,
                    'price': price
                }
    
            #
            # <ul class="pager">
            #      <li class="current">Page 1 of 50</li>
            #      <li class="next"><a href="catalogue/page-2.html">next</a></li>
            # </ul>
    
            next_url = response.css('ul.pager li.next a::attr(href)').extract_first()
            if next_url:
                next_url = response.urljoin(next_url)
                yield scrapy.Request(next_url, callback=self.parse)
    
5. Run the project::
    
    # Using the Command Line
    scrapy crawl books
    

##################################################################################################
Save Scrapy Project
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

