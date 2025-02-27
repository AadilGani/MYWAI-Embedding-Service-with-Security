# MyWAI Embedding Service (With Security)

This repository contains a **FastAPI-based embedding service** for **MyWAI**, designed to process and store embeddings from various file types (PDF, DOCX, TXT, CSV, XLSX) using **OllamaEmbeddings**. The service reads files, splits the text into chunks, generates embeddings, and stores them in a **PostgreSQL database** with vector support. This version includes **security measures** such as **OAuth2 token authentication** and **CORS protection**.

---

## Features

- **Supports multiple file types:** PDF, DOCX, TXT, CSV, XLSX.
- **Uses OllamaEmbeddings** for generating text embeddings.
- **Stores embeddings** in a PostgreSQL database with vector support.
- **Automatically handles table alterations** for new columns.
- **Generates and stores metadata** for each processed file.
- **Secure authentication** using OAuth2 tokens with Auth0 integration.
- **CORS protection** with specific allowed origins and headers.

---

## Technologies Used

- **FastAPI**
- **SQLAlchemy**
- **PostgreSQL**
- **LangChain**
- **OllamaEmbeddings**
- **OAuth2 with Auth0**
- **JWT for token validation**

---

## Setup

### Prerequisites

- **Python 3.8+**
- **PostgreSQL** with **pgvector** extension.
- **Auth0 account** for OAuth2 token generation and validation.

---

### Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/AadilGani/MyWAI-Embedding-Service-with-security.git

### Create a virtual environment and activate it:
  ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use venv\Scripts\activate

### Install the required dependencies:

```bash
  pip install -r requirements.txt

### Set up the PostgreSQL database:

Create a new database and user:

```bash
  CREATE DATABASE experiment;
 CREATE USER mywai WITH ENCRYPTED PASSWORD 'Bth-12345';
 GRANT ALL PRIVILEGES ON DATABASE experiment TO mywai;

Update the CONNECTION_STRING in the code with your database credentials if necessary.

### Configure Auth0:

Update the AUTH0_CONFIG dictionary in the code with your Auth0 domain, audience, and issuer.

Ensure your Auth0 application is configured to issue tokens with the required claims.

### Start the FastAPI server:

```bash
  uvicorn app:app --host 0.0.0.0 --port 1213


# API Endpoints
### Generate Embeddings
- **URL: /generate_embeddings
- **Method: POST
- **Description: Upload a file to generate and store embeddings.
- **Authentication: OAuth2 token required.

- **Request:

    - **File: A file in one of the supported formats (PDF, DOCX, TXT, CSV, XLSX).
    - **Authorization Header: Bearer <token>

- **Response:
- **200 OK: {"message": "Embeddings created and stored successfully!"}
- **400 Bad Request: {"detail": "File is required"} or {"detail": "Unsupported file type"}
- **401 Unauthorized: {"detail": "Invalid token"}
- **500 Internal Server Error: {"detail": "Error processing file: <error_message>"}

# Security Features
## Auth2 Authentication
- **The service uses OAuth2 with Auth0 for token-based authentication.
- **Tokens are validated against Auth0's public keys.
- **Tokens must include the required audience (aud) and issuer (iss) claims.
- **Tokens are checked for expiration and validity.

## CORS Protection
- **The service includes CORS middleware with specific allowed origins, methods, and headers.
- **Only requests from the following origins are allowed:
  - **http://localhost:44360
  - **https://localhost:44360
  - **https://192.168.0.194:44360
  - **https://llm.platform.myw.ai
  - **https://rossana.platform.myw.ai

## Error Handling
- **Detailed error logging is implemented for debugging and monitoring.
- **Unauthorized requests are rejected with a 401 Unauthorized response.
- **Invalid or expired tokens are rejected with appropriate error messages.


# Contributing
Contributions are welcome! Please open an issue or submit a pull request.

# License
This project is licensed under the MIT License. See the LICENSE file for details.
