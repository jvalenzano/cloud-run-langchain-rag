# Cloud Run LangChain RAG Application

A Retrieval Augmented Generation (RAG) application using LangChain and Cloud Run to answer questions about Cloud Run release notes. The application uses Gemini AI with a PostgreSQL vector database to provide accurate, context-aware responses.

## Overview

This application allows users to:
- Ask questions about Cloud Run features and capabilities
- Get responses grounded in actual Cloud Run release notes
- Access information through a REST API or web interface

## Prerequisites

- Google Cloud Project with enabled APIs
- Python 3.11 or higher
- Google Cloud CLI (gcloud)
- PostgreSQL on Cloud SQL
- Poetry for dependency management
- LangChain CLI

## Setup

1. Clone the repository
```bash
git clone https://github.com/jvalenzano/cloud-run-langchain-rag.git
cd cloud-run-langchain-rag
```

2. Set up Google Cloud Project
```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

3. Enable required APIs
```bash
gcloud services enable \
    bigquery.googleapis.com \
    sqladmin.googleapis.com \
    aiplatform.googleapis.com \
    cloudresourcemanager.googleapis.com \
    artifactregistry.googleapis.com \
    cloudbuild.googleapis.com \
    run.googleapis.com \
    secretmanager.googleapis.com
```

4. Create Cloud SQL instance
```bash
export REGION=us-central1
gcloud sql instances create sql-instance \
    --database-version POSTGRES_14 \
    --tier db-f1-micro \
    --region $REGION
```

5. Install dependencies
```bash
poetry install
```

## Development

1. Set up local environment:
```bash
# Set environment variables
export DB_INSTANCE_NAME=$(gcloud sql instances describe sql-instance --format="value(connectionName)")
export DB_USER=app
export DB_NAME=release-notes
export DB_PASS=your_password
```

2. Run the indexing job to populate the database:
```bash
python app/indexer.py
```

3. Start the local development server:
```bash
langchain serve
```

## Deployment

1. Deploy the indexing job:
```bash
gcloud run jobs deploy indexer \
    --source . \
    --command python \
    --args app/indexer.py \
    --set-env-vars=DB_INSTANCE_NAME=$DB_INSTANCE_NAME \
    --set-env-vars=DB_USER=app \
    --set-env-vars=DB_NAME=release-notes \
    --set-env-vars=DB_PASS=your_password \
    --region=$REGION \
    --execute-now
```

2. Deploy the web application:
```bash
gcloud run deploy run-rag \
    --source . \
    --set-env-vars=DB_INSTANCE_NAME=$DB_INSTANCE_NAME \
    --set-env-vars=DB_USER=app \
    --set-env-vars=DB_NAME=release-notes \
    --set-env-vars=DB_PASS=your_password \
    --region=$REGION \
    --allow-unauthenticated
```

## Usage

1. Access the web interface at the deployed Cloud Run URL: `/playground`

2. Example questions you can ask:
   - "Can I mount a Cloud Storage bucket as a volume in Cloud Run?"
   - "What are the latest features in Cloud Run?"
   - "When did Cloud Run add support for Cloud Storage mounts?"

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request