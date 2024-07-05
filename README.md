# Retrieval Augmented Generation with Azure OpenAI and Azure AI Search  
   
This repository contains a series of Python notebooks that demonstrate how to process raw text data, generate embeddings using Azure OpenAI, create and populate an Azure AI Search index, perform various search techniques, and implement a Retrieval-Augmented Generation (RAG) system.  
   
## Table of Contents  
1. [Setup](#setup)  
2. [Notebooks Overview](#notebooks-overview)  
3. [Environment Variables](#environment-variables)  
4. [Folder Structure](#folder-structure)  
5. [Sample Data](#sample-data)  
6. [Usage](#usage)  
7. [Evaluation](#evaluation)  
8. [Contributing](#contributing)  
   
## Setup  
   
### Prerequisites  
1. **Azure Resources:**  
   - Azure AI Search (at least the Basic SKU)  
   - Azure OpenAI Service with Embedding and Chat models  
   
2. **Local Machine:**  
   - Python installed  
   - Git installed  
   
### Steps  
1. **Clone the Repository:**  
   ```bash  
   git clone https://github.com/tayganr/rag.git
   cd rag
   ```  
   
2. **Create and Activate a Virtual Environment:**  
   ```bash  
   python -m venv venv  
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`  
   ```  
   
3. **Install Required Libraries:**  
   ```bash  
   pip install -r requirements.txt  
   ```  
   
4. **Prepare the `documents` Folder:**  
   - The `documents` folder contains sample text files from the UK Parliament Hansard, specifically debates from [Commons Hansard for 24 May 2024 (Volume 750)](https://hansard.parliament.uk/commons/2024-05-24). These files are available in the public domain and are used to demonstrate the capabilities of this project.  
   - To use your own data, replace the text files in the `documents` folder with your own text documents.  
   
5. **Create the `.env` File:**  
   - Create a `.env` file in the root directory of the project and populate it with your Azure service details.  
  
   Example:  
   ```plaintext  
   # Azure AI Search  
   AZURE_AI_SEARCH_SERVICE_NAME=your-search-service-name  
   AZURE_AI_SEARCH_ADMIN_KEY=your-search-admin-key  
  
   # Azure OpenAI  
   AZURE_OPENAI_ENDPOINT=https://your-openai-endpoint.openai.azure.com/  
   AZURE_OPENAI_KEY=your-openai-key  
   AZURE_OPENAI_EMBEDDING_DEPLOYMENT=your-embedding-deployment  
   AZURE_OPENAI_EMBEDDING_MODEL_NAME=your-embedding-model  
   AZURE_OPENAI_API_VERSION=2024-05-01-preview  
   AZURE_OPENAI_CHAT_DEPLOYMENT=your-chat-deployment  
   AZURE_OPENAI_CHAT_MODEL_NAME=your-chat-model  
   ```  
   
6. **Prepare the Evaluation Dataset:**  
   - The `evaluation_data.json` file contains sample evaluation data corresponding to the Hansard debates.  
   - To use your own evaluation data, replace the contents of `evaluation_data.json` with your own questions, contexts, and ground_truth data.  
   
## Notebooks Overview  
   
1. **01_text_chunking_and_embedding.ipynb:**  
   - Processes raw text data, chunks it into manageable pieces, generates embeddings for each chunk using Azure OpenAI, and saves the chunked and embedded text into JSON files.  
   
2. **02_indexing.ipynb:**  
   - Creates and populates an Azure AI Search index using the chunked and embedded text generated in the previous notebook.  
   
3. **03_search.ipynb:**  
   - Demonstrates various search techniques including keyword search, vector search, hybrid search, hybrid search with a semantic ranker, and filtered search.  
   
4. **04_rag.ipynb:**  
   - Implements a Retrieval-Augmented Generation (RAG) system to retrieve relevant context from indexed documents and generate answers using a language model.  
   
5. **05_evaluation.ipynb:**  
   - Evaluates and compares different RAG setups using predefined metrics and visualizes the results.  
   
## Environment Variables  
   
The `.env` file should contain the following variables:  
   
```plaintext  
# Azure AI Search  
AZURE_AI_SEARCH_SERVICE_NAME=your-search-service-name  
AZURE_AI_SEARCH_ADMIN_KEY=your-search-admin-key  
   
# Azure OpenAI  
AZURE_OPENAI_ENDPOINT=https://your-openai-endpoint.openai.azure.com/  
AZURE_OPENAI_KEY=your-openai-key  
AZURE_OPENAI_EMBEDDING_DEPLOYMENT=your-embedding-deployment  
AZURE_OPENAI_EMBEDDING_MODEL_NAME=your-embedding-model  
AZURE_OPENAI_API_VERSION=2024-05-01-preview  
AZURE_OPENAI_CHAT_DEPLOYMENT=your-chat-deployment  
AZURE_OPENAI_CHAT_MODEL_NAME=your-chat-model  
```  
   
## Folder Structure  
   
```plaintext  
.  
├── documents/                # Folder containing text files to be processed  
├── embeddings/               # Folder where the chunked and embedded JSON files will be saved  
├── .env                      # Environment variables file  
├── requirements.txt          # List of required Python libraries  
├── 01_text_chunking_and_embedding.ipynb  
├── 02_indexing.ipynb  
├── 03_search.ipynb  
├── 04_rag.ipynb  
├── 05_evaluation.ipynb  
├── evaluation_data.json      # Evaluation dataset containing question, contexts, and ground_truth  
└── sample_data/              # Folder containing sample data used for demonstration  
```  
   
## Sample Data  
   
- The `documents` folder contains sample text files from the UK Parliament Hansard, specifically debates from [Commons Hansard for 24 May 2024 (Volume 750)](https://hansard.parliament.uk/commons/2024-05-24). These files are in the public domain and are used to demonstrate the capabilities of this project.  
- The `evaluation_data.json` file contains sample evaluation data corresponding to the Hansard debates. The evaluation data includes synthetic question/answer pairs generated using large language models (LLMs). This synthetic data may contain mistakes and has not been validated by a Subject Matter Expert (SME). It is purely used for demonstration purposes.  
   
### JSON Structure  
The structure of the `evaluation_data.json` adheres to the expected structure for the RAGAS framework:  
```json  
{  
  "question": ["Example question 1", "Example question 2"],  
  "contexts": [["Context 1 for Q1", "Context 2 for Q1"], ["Context 1 for Q2", "Context 2 for Q2"]],  
  "ground_truth": ["Expected answer for Q1", "Expected answer for Q2"]  
}  
```  
   
### Replacing with Your Own Data  
- **Text Documents:**  
  - Replace the text files in the `documents` folder with your own text documents in plain text format.  
    
- **Evaluation Dataset:**  
  - Replace the contents of `evaluation_data.json` with your own questions, contexts, and ground_truth data following the same structure.  
   
## Usage  
   
1. **Run the Notebooks in Sequence:**  
   - Start with `01_text_chunking_and_embedding.ipynb` and proceed to `05_evaluation.ipynb`.  
   
2. **Monitoring Progress:**  
   - Each notebook is designed to be run step-by-step. Follow the instructions and markdown comments within each notebook.  
   
## Evaluation  
   
- The `05_evaluation.ipynb` notebook provides a framework to evaluate and compare different RAG setups.  
- Metrics such as Answer Relevancy, Answer Similarity, and Context Precision are calculated and visualized.  
   
## Contributing  
   
Contributions are welcome! Please submit a pull request or open an issue for any improvements or bug fixes.  
