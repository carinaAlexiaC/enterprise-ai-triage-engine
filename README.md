# Enterprise AI Support & PII Triage Engine

![Python](https://img.shields.io/badge/Backend-Python_Flask-3776AB?style=flat&logo=python&logoColor=white)
![Frontend](https://img.shields.io/badge/Frontend-ES6_JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Database](https://img.shields.io/badge/Database-Indexed_SQLite-003B57?style=flat&logo=sqlite&logoColor=white)
![AI Engine](https://img.shields.io/badge/AI_Engine-OpenAI_SDK_%26_Ollama-10A37F?style=flat&logo=openai&logoColor=white)

An enterprise IT support triage pipeline that ingests unstructured support tickets, automatically redacts Personally Identifiable Information (PII), classifies issue categories and urgency sentiment using a Local LLM (Ollama) via the OpenAI Python SDK, and logs audited records into an indexed SQLite database.

**[Launch Live Interactive Web Demo](https://carinaAlexiaC.github.io/enterprise-ai-triage-engine/)**

## Application Interface Preview

![Enterprise AI Triage Dashboard Preview](assets/dashboard-preview.png)

## System Architecture

```mermaid
flowchart TD
    A[Client Browser: ES6 Async/Await UI] -->|POST /api/triage JSON| B(Flask REST API Controller)
    B --> C[PII Sanitization Layer: Regex Masking]
    C -->|Sanitized String| D{Local Ollama LLM Active?}
    D -->|Yes: OpenAI SDK HTTP| E[Local Llama / Qwen JSON Triage]
    D -->|No: Automatic Failover| F[Deterministic Keyword NLP Engine]
    E --> G[Parameterized SQL Insert ?]
    F --> G
    G --> H[(SQLite DB: Non-Clustered Index on Category & Sentiment)]