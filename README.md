**PPC RAG Chatbot: Pakistan Penal Code Query System**

A Retrieval-Augmented Generation (RAG) chatbot for querying the Pakistan Penal Code (PPC) in English and Urdu. The system scrapes PPC sections, generates bilingual summaries using OpenAI's API, stores embeddings in a FAISS vector database, and answers queries via a LangChain-powered RAG pipeline. A Gradio interface provides an interactive UI. This project demonstrates skills in web scraping, AI integration, multilingual processing, and RAG system design.
**Table of Contents**

Features
Architecture
Data Flow
Installation
Usage
Dependencies
Setup Instructions
Running the Project
Contributing
License
Contact

**Features**

Web Scraping: Extracts PPC sections from an online source using BeautifulSoup.
Bilingual Summarization: Generates concise English and Urdu summaries using OpenAI's gpt-4o-mini.
Vector Search: Indexes summaries with OpenAI embeddings in a FAISS vector store for fast retrieval.
RAG Pipeline: Combines retrieval and generation using LangChain for accurate query responses.
Interactive UI: Gradio-based chatbot interface supporting English and Urdu queries.
Error Handling: Robust handling of API, scraping, and runtime errors.
Kaggle Compatibility: Designed for Kaggle notebooks with secure API key management via Kaggle Secrets.

**Architecture**
The project follows a modular, layered architecture:

Data Ingestion Layer:

Scrapes PPC text from https://www.pakistani.org/pakistan/legislation/1860/actXLVof1860.html.
Parses and structures into a Pandas DataFrame (~534 sections).


Data Processing Layer:

Summarizes sections in English and Urdu using OpenAI's Chat Completions API.
Embeds summaries using OpenAI's text-embedding-3-small and stores in FAISS.


Query Processing Layer (RAG):

Retrieves top-5 relevant sections using FAISS.
Generates responses with OpenAI's gpt-4o-mini via LangChain.


Presentation Layer:

Gradio UI for interactive query input and response display.






Layer
Technologies
Purpose



Data Ingestion
BeautifulSoup, Requests, Pandas
Fetch and structure PPC text.


**Data Processing**
OpenAI API, FAISS
Summarize and vectorize data.


**Query Processing**
LangChain, OpenAI LLM
Retrieve and generate responses.


**Presentation**
Gradio
Interactive query interface.


**Data Flow**
Scraping: Fetch HTML → Parse with regex → Save as DataFrame (id, chapter, official_text).
Summarization: Batch process official_text → OpenAI API → Add summary_en and summary_ur to DataFrame → Save as ppc_bilingual.csv.
Vectorization: Combine summaries → Generate embeddings → Index in FAISS → Save as ppc_faiss_index.
Querying: User query → Embed → Retrieve from FAISS → Format context → OpenAI LLM → Response.
UI: Gradio accepts query → Displays RAG response.

**Installation**
Clone the repository and install dependencies in a Python 3.8+ environment.
git clone https://github.com/Aman017Javed/ppc-rag-chatbot.git
cd ppc-rag-chatbot
pip install -r requirements.txt

**Requirements File**
Create a requirements.txt with:
openai==1.30.0
langchain==0.2.0
langchain-openai==0.1.0
langchain-community==0.2.0
faiss-cpu==1.7.4
requests==2.31.0
beautifulsoup4==4.12.2
pandas==2.0.3
tqdm==4.66.1
gradio==4.0.2

**Dependencies**

Python Libraries: openai, langchain, langchain-openai, langchain-community, faiss-cpu, requests, beautifulsoup4, pandas, tqdm, gradio.
External Services: OpenAI API key (for summarization, embeddings, and generation).
Environment: Kaggle notebook (recommended) or local Jupyter with internet access.

**Setup Instructions**

Obtain OpenAI API Key:

Sign up at OpenAI Platform.
Generate and copy an API key.


Kaggle Setup:

Create a Kaggle notebook.
Go to "Add-ons" > "Secrets" and add OPENAI_API_KEY with your API key.
Enable "Internet" in "Notebook options".


Local Setup (Alternative):

Set the API key as an environment variable:export OPENAI_API_KEY="your-api-key"


Or modify os.environ["OPENAI_API_KEY"] in the code.


Enable T4 GPU (Optional):

In Kaggle, select "GPU T4 x2" under "Notebook options" > "Accelerator".
Note: OpenAI API is cloud-based and doesn't use the T4 GPU; consider hybrid models for GPU usage.



**Running the Project**

Open the Notebook:

Use Kaggle or a local Jupyter environment.
Copy the provided notebook.ipynb into your environment.


Execute Cells Sequentially:

Cell 1: Install dependencies.
Cell 2: Set up OpenAI API and validate key.
Cell 3: Scrape PPC (~534 sections).
Cell 4: Generate bilingual summaries, save as ppc_bilingual.csv.
Cell 5: Build and save FAISS index (ppc_faiss_index).
Cell 6: Test RAG pipeline with a sample query.
Cell 7: Launch Gradio UI for interactive querying.


**Expected Outputs:**

Cell 2: "✅ OpenAI API key validated successfully."
Cell 3: "Scraped 534 PPC sections" with DataFrame display.
Cell 4: Progress bar (67 batches), saves CSV.
Cell 5: "FAISS index built with 534 entries."
Cell 6: Sample answer (e.g., "Section PPC_379: Imprisonment up to 7 years, or fine, or both.").
Cell 7: Public Gradio URL.


**Troubleshooting:**
AuthenticationError: Verify OPENAI_API_KEY in Kaggle Secrets.
RateLimitError: Reduce batch_size in Cell 4 (e.g., to 4) or add time.sleep(1) between batches.
Gradio Failure: Retry or run locally if public URL fails.
Check OpenAI usage at OpenAI Usage.



**Contributing**
Contributions are welcome! To contribute:

Fork the repository.
Create a feature branch (git checkout -b feature/your-feature).
Commit changes (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a Pull Request with a detailed description.

Please follow the Contributor Covenant Code of Conduct.
License
This project is licensed under the MIT License. See the LICENSE file for details.
Contact
For questions or feedback:

GitHub: https://github.com/Aman17Javed
Email: amanjaved421@example.com

