# Regulatory Tracker - Technical Architecture Documentation

**Source**: repository/technical-specifications/regulatory-tracker-technical-architecture.md
**Type**: Technical Specification
**Upload Date**: 2026-02-09
**Source SHA**: Not provided

## Key Points

- Three-tier cloud-ready architecture with Next.js 14 frontend, FastAPI backend, and SQLite database, using asynchronous background processing for AI-powered regulatory analysis
- ScanOrchestrator service manages a 7-stage pipeline (Initializing → Retrieving Sources → Detecting Changes → Analyzing → Scoring → Generating Artifacts → Finalizing) coordinating regulatory document analysis via Claude API
- LLMService integrates with Claude Sonnet 4 model to provide structured regulatory analysis with JSON schema output including impact assessment, affected areas, and confidence scoring
- ChangeDetectionService uses SHA-256 content hashing, regex-based keyword detection, and demo mode to identify material regulatory changes
- Full data flow from scan submission through background task execution, result storage in SQLite, workflow status transitions (draft → in_review → verified), and artifact generation in Markdown and Word formats
- Deployment via Docker Compose with containerized frontend (Node.js 20), backend (Python 3.11), and shared volumes for data persistence
- Security considerations include CORS configuration, input validation via Pydantic, JWT authentication for production, encryption at rest/transit, and comprehensive audit logging
- Scalability roadmap includes migration from SQLite to PostgreSQL, Redis caching, distributed task queues via Celery, horizontal scaling with load balancers, and database indexing optimization

## Entities and Topics

- **Next.js 14**: Frontend React framework with App Router and TypeScript for UI component rendering
- **FastAPI**: Modern Python web framework serving RESTful API endpoints for scans, results, workflows, and knowledge management
- **Claude API (Sonnet 4)**: Anthropic's AI model for regulatory document analysis with configurable prompts and JSON output schema
- **ScanOrchestrator**: Core service managing the 7-stage regulatory analysis pipeline with state management and error handling
- **ChangeDetectionService**: Identifies material changes using SHA-256 hashing, keyword detection, and demo mode
- **ArtifactGenerator**: Creates professional Markdown and Word (.docx) documentation from analysis results
- **SQLite Database**: File-based relational database storing scans, results, and sources with schema including workflow status tracking
- **Docker Compose**: Container orchestration enabling multi-container deployment with networking and volume management
- **Asyncio Task Queue**: Asynchronous background processing for long-running scan operations
- **Knowledge Store**: Verified regulatory knowledge accessible via API with export functionality

## Relevance to Project

This technical specification document provides the foundational architectural blueprint for the Regulatory Tracker application, detailing all system layers, services, data flows, and deployment configurations. It is essential for development teams implementing the platform, as it defines component interactions, API contracts, database schema, and technology stack decisions required to build a scalable, production-ready regulatory compliance analysis system.