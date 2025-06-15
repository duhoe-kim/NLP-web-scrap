<!-- PROJECT TITLE -->
<h1 id="toc" align="center">NLP & Web Scraping <br/> for Software Developer Role Analysis</h1>

<!-- TABLE OF CONTENTS -->
<h2>Table of Contents</h2>
<ol>
  <li><a href="#about-the-project">About The Project</a></li>
  <ul>
    <li><a href="#built-with">Built With</a></li>
    <li><a href="#project-description">Project Description</a></li>
  </ul>
  <li><a href="#features">Features</a></li>
  <li><a href="#overview">Overview</a></li>
</ol>


<!-- ABOUT THE PROJECT -->
<h2 id="about-the-project">About The Project</h2>
<h3 id="built-with">Built With</h3>

<p>Languages : </p>

[![Python][Python.img]][Python-url]

<p>Development Env : </p>

[![Jupyter][Jupyter.img]][Jupyter-url]

<p>Libraries : </p>

[![Nltk][Nltk.img]][Nltk-url]
[![Selenium][Selenium.img]][Selenium-url]
[![Pandas][Pandas.img]][Pandas-url]
[![Regex][Regex.img]][Regex-url]
[![Matplotlib][Matplotlib.img]][Matplotlib-url]

<h3 id="project-description">Project Description</h3>

<p>
  This project aims to identify popular skillsets for software developers by analyzing job postings scraped from LinkedIn, Jobstreet, and Indeed. The collected data is cleaned, processed, and then analysed to extract frequently requested skills.
With a primary focus on natural language processing (NLP), this project details the extraction and cleaning of data obtained from websites. The following chapters will provide an in-depth explanation and overview of these crucial steps, alongside resources and references. 
  
  Implemented in Python using Jupyter, the project is presented as a report containing code. To gain a comprehensive understanding of the implementation pipeline and the reasoning behind the code, readers are advised to consult the accompanying .ipynb file.
</p>

<p align="right">(<a href="#toc">back to top</a>)</p>


<!-- FEATURES -->
<h2 id="features">Features</h2>

<h3>Data Extraction</h3>
<p>
  This project leverages Selenium for browser automation, enabling the creation of a controlled browser environment where a bot can interact with web elements. Consequently, the bot can perform actions like clicking buttons, entering text, and utilizing website features. A key aspect is the need to explicitly code every bot action.

  To streamline data extraction, the process is segmented into manageable steps, with each step encapsulated within a dedicated function. This modular approach enhances code organization and maintainability.
 
  The initial stage involves accessing and navigating the target website to reach the desired data. This stage is facilitated by the  open<WebsiteName>Page() function. This function opens and sets up the browser environment.<br>
  
  Internally, $\color{Green}{\textsf{open<'WebsiteName'>Page()}}$ utilizes smaller functions that operate on the same browser instance (passed as an argument) to navigate to the desired data:

  <ul>
    <li>
      $\color{Green}{\textsf{loginTo<'WebsiteName'>(browser)}}$ : <br>
      Logs into the website by finding and filling the ID and password fields, then clicking the login button
    </li>
    <li>
      $\color{Green}{\textsf{searchJobandLocation(browser)}}$ : <br>
      Searches for "software developer" jobs in "singapore," enabling focused data extraction 
      for a specific role andlocation, leading to more consistent results.
    <li>
      $\color{Green}{\textsf{filterDate<'WebsiteName'>(browser)}}$ : <br>
      Filters out older job listings.
    </li>
    <li>
      $\color{Green}{\textsf{filterJobType<'WebsiteName'>(browser)}}$ : <br>
       Applies another filter to extract more relevant job data.
    </li>
  </ul>
        
  The second phase involves extracting job posting data from the website's search results. This is managed by the extractDataFrom<WebsiteName>(browser) function.

  <ul>
    <li>
      $\color{Green}{\textsf{extractDataFrom<'WebsiteName'>(browser)}}$ : <br>
      This function systematically navigates through the website's pages, accessing up to 1000 job postings. 
      It utilizes the $\color{Green}{\textsf{extractDataFrom<WebsiteName>Page(browser)}}$ function to 
      retrieve data from each individual post.
    </li>
    <li>
      $\color{Green}{\textsf{extractDataFrom<'WebsiteName'>Page(browser)}}$ : <br>
      This function first identifies the total number of job postings and then accesses each one. 
      From each accessed post, it extracts the job title and detailed job information.
    </li>
  </ul>
</p>

<h3>Data Preprocessing</h3>
<p>
  The extracted data is stored as CSV files via the Pandas library.

  Several data quality issues impact the job information:
  <ol>
    <li>Varied Posting Styles: Due to the diverse sources (different companies), job postings lack uniformity in how they present candidate requirements.</li>
    <li>Irrelevant Content: The job details contain supplementary information like descriptions and overviews, which, while important, are not the central focus of this project.</li>
    <li>Textual Clutter: The data includes punctuation, special characters, and stopwords that introduce noise and hinder effective analysis.</li>
  </ol>

  The first challenge, inconsistent labeling of job requirements, is tackled by identifying frequently used terms. Each job posting is then analyzed to determine which of these keywords is present, effectively categorizing the requirement information and overcoming the lack of uniformity. 
  
  Second problem is handled with the  $\color{Green}{\textsf{getJobRequirements(df)}}$ function. The identified set of keywords is employed to extract pertinent information. By capturing the strings that follow these keywords, the system isolates the specific job requirements and removes irrelevant content from the initial data extraction. This is achieved by $\color{Green}{\textsf{geJobRequirements(df)}}$ 
  
  Finally, the cleanJobRequirement(df) function processes the data. Leveraging the NLTK library, it removes punctuation, special characters, and stopwords, resulting in a dataset of tokenized words free of irrelevant terms. This cleaning step prepares the data for subsequent analysis.
</p>

<h3>Data Preprocessing</h3>
<p>
  The final feature of this software developer role analysis project is the data analysis itself. To understand the desired programming languages and skills, the scraped job requirements are analyzed. 

  Programming language frequencies are determined by referencing a web-scraped list and visualized as a bar graph using Matplotlib. By counting the occurrences of words within the job requirements, the most sought-after programming languages in the software development field are identified. Similarly, word frequency analysis is applied to skills, presented as a word cloud to highlight the most frequently mentioned requirements.
</p>
<p align="right">(<a href="#toc">back to top</a>)</p>


<!-- OVERVIEW -->
<h2 id="overview">Overview</h2>
<h3>Benefits</h3>
<p>
  The project successfully achieved its goal of identifying desired skills and programming languages among employees. It ensured the reliability of the data analysis by collecting information from diverse websites, which significantly prevented the collection of biased data. This broad approach to data sourcing gives us more confidence in the results of our analysis.
</p>


<h3>Shortcoming</h3>
<p>
  <b>The Fragility of Selenium Automation</b>
  
  Selenium bots interact with web pages by locating specific elements like buttons, text fields, or images. They do this primarily by referencing an element's class name or ID. The problem arises because these class names and IDs are often generated by web developers and can change for many reasons. When a bot tries to find an element using an outdated class or ID, it simply fails to locate the element, leading to an error and stopping the automation process. This means continuous monitoring and updates are needed to keep the bot functioning. <br><br>

  <b>Website Diversity and Non-Reusable Code</b>
  
  The internet is a vast and varied place, and every website is built differently. This presents a significant challenge for automation:
  - <i>Varying Structures</i> : <br> Some websites use complex nested elements, while others are flatter. The way you navigate from one page to another (e.g., clicking a specific link vs. using a search bar) can also differ significantly.
  - <i>Different Technologies</i> : <br> Websites are built using a wide array of programming languages, frameworks, and content management systems. These choices influence how elements are rendered and interacted with.
  - <i>Unique Navigation Patterns</i> : <br> For example, one e-commerce site might require you to click "Add to Cart," then "Proceed to Checkout," while another might have a one-click purchase button. The exact sequence of actions will vary.

  Because of this diversity, a Selenium script written to perform an action on one website will almost certainly not work on another without significant modifications. This means that for every new website needs to automate, it requires a completely new set of functions, making code reuse nearly impossible and development time-consuming. <br><br>

  <b>The Anti-Bot Arms Race</b>

  The landscape of web scraping has evolved into an "arms race" between websites trying to protect their data and bots trying to access it. Companies are investing heavily in sophisticated anti-bot measures to prevent automated access, protect their data, and manage server load. These advanced measures make it much harder to anticipate the actions a bot needs to take. 
  
  Bypassing them often requires:
  - <i>More frequent updates</i> : <br> As anti-bot techniques evolve, bots need constant adjustments to their code to adapt.
  - <i>Increased computational power</i> : <br> Solving CAPTCHAs, managing proxies, and emulating human behavior can be computationally intensive.
  - <i>Significant time investment</i> : <br> Debugging and developing solutions to counter new anti-bot measures can be a very time-consuming process.
</p>

<p align="right">(<a href="#toc">back to top</a>)</p>


<!-- MARKDOWN & IMAGES -->
[Python.img]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[Python-url]: https://www.python.org/
[Jupyter.img]: https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white
[Jupyter-url]: https://jupyter.org/
[Nltk.img]: https://img.shields.io/badge/NLTK-154F5B?style=for-the-badge&logo=python&logoColor=white
[Nltk-url]: https://www.nltk.org/
[Selenium.img]: https://img.shields.io/badge/Selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white
[Selenium-url]: https://www.selenium.dev/
[Pandas.img]: https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white
[Pandas-url]: https://pandas.pydata.org/
[Regex.img]: https://img.shields.io/badge/Regex-70B0E0?style=for-the-badge
[Regex-url]: https://regexr.com/
[Matplotlib.img]: https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge
[Matplotlib-url]: https://matplotlib.org/
