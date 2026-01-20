# Formula_1_Regulations_RAG_Systems

## An end-to-end Retrieval-Augmented Generation (RAG) platform designed to demystify complex F1 regulations and provide data-driven race insights.

``` mermaid
graph TD
    User([User or Official]) --> UI[Streamlit Frontend]
    
    subgraph Data_Pipeline [Data Engineering - Airflow]
        Docs[FIA Regulation PDFs] --> Adobe[Adobe Extractor]
        Adobe --> Airflow[Airflow Orchestrator]
        Live_Data[OpenF1 API] --> Airflow
    end

    subgraph Storage_Layer [Data Storage]
        Airflow --> Snowflake[(Snowflake Data Warehouse)]
        Airflow --> Pinecone[(Pinecone Vector DB)]
        Airflow --> S3[(Amazon S3)]
    end

    subgraph Intelligence_Layer [AI and ML Logic]
        UI --> FastAPI[FastAPI Backend]
        FastAPI --> Snowflake
        FastAPI --> Pinecone
        FastAPI --> GPT4[OpenAI GPT-4]
        FastAPI --> SKLearn[Scikit-Learn Model]
    end

    style UI fill:#e10600,color:#fff
    style Snowflake fill:#29b5e8,color:#fff
    style Pinecone fill:#000,color:#fff
    style GPT4 fill:#10a37f,color:#fff
```

## Key Features

    AI Rules Expert: RAG-powered chatbot using GPT-4 and Pinecone to provide grounded answers to regulatory questions based on official FIA documents.

    FIA Decision Support: Automated incident analysis tool that suggests penalties based on real-time regulation matching.

    Predictive Strategy Game: A machine learning module built with Scikit-Learn for predicting race outcomes and performance.

    Live Hub: Access to real-time driver profiles, track details, and race analytics via the OpenF1 API.

## Technical Stack

    Backend: FastAPI, Python.

    Data Engineering: Apache Airflow (Orchestration), Adobe Extractor (PDF Parsing).

    Storage: Snowflake (Structured Data), Pinecone (Vector Embeddings), Amazon S3 (Raw Files).

    AI/ML: OpenAI GPT-4, Scikit-Learn.

    Frontend: Streamlit.

    DevOps: Docker, Poetry.



## Setup Instructions
### Step 1: Clone the Repository
Clone the repository to your local machine:
```bash
git clone https://github.com/your-repo/formula1-regulation-rag.git
cd formula1-regulation-rag
```

### Step 2: Install Dependencies
Install all required dependencies using Poetry:
```bash
poetry install
```

### Step 3: Configure Environment Variables
Create a `.env` file in the root directory and add the following variables:
```env
OPENAI_API_KEY=your_openai_api_key
SNOWFLAKE_USER=your_snowflake_user
SNOWFLAKE_PASSWORD=your_snowflake_password
SNOWFLAKE_ACCOUNT=your_snowflake_account
S3_BUCKET_NAME=your_s3_bucket_name
OPENF1_API_KEY=your_openf1_api_key
```

### Step 4: Initialize Databases
Set up Snowflake for structured data:
1. Create tables for storing regulatory clauses, historical race information, and user data.
2. Populate initial data for testing.

Populate Pinecone with embeddings:
- Use the text embeddings from OpenAI to index regulatory content in Pinecone.

Configure Amazon S3:
- Store FIA PDFs in an S3 bucket for text extraction.

### Step 5: Run Airflow for Automation
Initialize Airflow and set up data scraping:
```bash
airflow db init
airflow webserver -p 8080
airflow scheduler
```

🚀 Getting Started
Prerequisites

    Python 3.10+

    Poetry (Dependency Manager)

    Docker & Docker Compose

    Accounts for: OpenAI, Snowflake, Pinecone, and AWS (S3).

### Execution Instructions
#### Step 1: Start the Backend Server
Run the FastAPI server to handle backend operations:
```bash
poetry run uvicorn fastapi_app:app --reload
```

#### Step 2: Start the Frontend Application
Run the Streamlit application for the user interface:
```bash
poetry run streamlit run app.py
```

#### Step 3: Access the Application
Open your browser and navigate to:
```arduino
http://localhost:8501
```

## Conclusion
The Formula 1 Regulation RAG System is designed to transform the way Formula 1 fans, professionals, and officials interact with the sport. By integrating advanced AI capabilities with real-time data access and an engaging user interface, the platform will enhance transparency, education, and entertainment. Whether you're a casual fan or a decision-maker in the FIA, the system offers tools to enrich your understanding and engagement with Formula 1.

## References
- Formula 1 Revenue Report
- FIA Official Website

