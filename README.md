# Sales Email Generator using Gemini genAi RAG

**Project Goal:**

The primary aim of this notebook is to automate the process of creating personalized cold emails for business development. It achieves this by combining web scraping, large language models (LLMs), and a vector database to intelligently extract job details, find relevant past projects, and generate tailored outreach emails.

**Workflow:**

The notebook follows a systematic workflow comprising the following steps:

**Setup & Initialization:**

Essential libraries like groq, langchain, langchain_community, langchain-experimental, langchain-groq, and chromadb are installed.
The Groq client is initialized with an API key to access the LLM.
A webpage containing the job posting is loaded using WebBaseLoader from langchain_community.

**Job Posting Extraction:**

A prompt template named prompt_extract is defined, instructing the LLM to extract key information (role, experience, skills, description) from the webpage content and format it as JSON.
An LLM chain is constructed using the Groq LLM and the prompt.
The chain is invoked with the page content, resulting in the extraction of job data in JSON format.
This JSON output is parsed to access individual job details like role, experience, etc.

**Portfolio Matching:**

A CSV file named my_portfolio.csv, containing details of past projects and their associated tech stacks, is loaded using pandas.
A ChromaDB client is initialized, and a collection named "portfolio" is created or retrieved.
Project data from the CSV is added to the collection, embedding the "Techstack" column for similarity search.
The collection is queried using the skills extracted from the job posting to find the most relevant past projects.
Links to these relevant projects are retrieved from the query results.

**Cold Email Generation:**

A prompt template named prompt_email is defined, guiding the LLM to generate a personalized cold email. This template incorporates placeholders for job description and portfolio links.
A new LLM chain is created using the Groq LLM and the email prompt.
The chain is invoked, passing the extracted job description and the relevant portfolio links as input.
The generated cold email content is printed as output.

**Functionality in Detail:**

Web Scraping: The WebBaseLoader is used to retrieve the HTML content of the target webpage, which contains the job posting.

LLM for Information Extraction: The Groq LLM, accessed via the groq library and langchain-groq, plays a crucial role in extracting structured information from the unstructured webpage content. Prompts are carefully designed to guide the LLM to identify and extract specific job details.

Vector Database for Portfolio Matching: ChromaDB serves as a vector database to store and retrieve past projects based on their relevance to the target job's skills. The "Techstack" column from the portfolio CSV is embedded to represent projects as vectors, enabling similarity search.

LLM for Email Generation: The Groq LLM is further utilized to generate the cold email content. The prompt incorporates details like job description, company introduction, and portfolio links to create a personalized and compelling email.

Langchain for Workflow Orchestration: Langchain acts as the orchestrator, connecting the different components of the workflow. It facilitates the interaction with the LLM, handles prompt management, and chains together the steps of information extraction, portfolio matching, and email generation.

Overall, this Jupyter notebook demonstrates a practical application of AI and natural language processing in automating a business development task. It leverages the power of LLMs and vector databases to streamline the process of creating personalized cold emails, making outreach more targeted and efficient.
