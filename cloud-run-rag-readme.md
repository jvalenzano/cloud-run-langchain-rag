# Cloud Run LangChain RAG Application

A Retrieval Augmented Generation (RAG) application using LangChain and Google Cloud Run to answer questions about Cloud Run release notes. The application uses Gemini AI with a PostgreSQL vector database to provide accurate, context-aware responses.

## Overview

This application allows users to:
- Ask questions about Cloud Run features and capabilities
- Get responses grounded in actual Cloud Run release notes
- Access information through a REST API or web interface

![RAG Workflow](/images/rag-workflow.svg)
![Cloud SQL Setup](/images/cloud-sql-setup.png)
![LangChain Architecture](/images/langchain-architecture.png)

## 🚀 Project Structure

```
cloud-run-rag-tutorial/
│
├── images/                  # Project diagrams and screenshots
│   ├── rag-workflow.svg
│   ├── cloud-sql-setup.png
│   ├── langchain-architecture.png
│
├── README.md                # Main project documentation
├── code/                    # Source code
│   ├── indexer.py           # Data indexing script
│   ├── server.py            # LangChain application server
│
├── docs/                    # Detailed documentation
│   ├── SETUP.md             # Installation and setup guide
│   ├── DEPLOYMENT.md        # Deployment instructions
```

## 📋 Prerequisites

- Google Cloud account
- Python 3.11+
- Google Cloud SDK
- LangChain CLI
- Poetry

## 🔧 Key Components

### 1. Vector Database
- PostgreSQL on Cloud SQL
- Uses pgvector for semantic search
- Stores Cloud Run release notes

### 2. Retrieval Process
- Converts release notes to embeddings
- Semantic search of relevant notes
- Context-aware query resolution

### 3. AI-Powered Response Generation
- Uses Google's Gemini AI
- Generates natural language answers
- Provides grounded, context-specific responses

## 🧪 Demo Scenarios

### Example Queries

1. "Can I mount a Cloud Storage bucket in Cloud Run?"
2. "What are the latest runtime updates?"
3. "How have job timeouts changed recently?"

## 🚢 Deployment Steps

1. Set up Google Cloud project
2. Create Cloud SQL instance
3. Index release notes
4. Deploy LangChain application
5. Explore the LangServe playground

## 📊 Performance Metrics

- Total Release Notes: 231
- Date Range: Aug 15, 2018 - Dec 13, 2024
- Average Query Response Time: < 500ms

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

[Specify your license - MIT/Apache/etc]

## 🌟 Acknowledgments

- Google Cloud
- LangChain
- Gemini AI Team

## 📞 Support

For issues or questions, please open a GitHub issue or contact [your contact information]
