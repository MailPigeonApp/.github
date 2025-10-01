# MailPigeon

**MailPigeon** is a form submission backend API service that provides a flexible, scalable solution for handling form data with validation, file uploads, and integration capabilities.

> **Now Open Source!** This project was previously private and is now available as open source. We welcome contributions, feedback, and community involvement.

## Overview

MailPigeon enables developers to create form backends without building custom validation and storage infrastructure. The system validates incoming form submissions against project-specific field configurations, supports file uploads to AWS S3, and integrates with external services like Telegram for notifications.

## Project Architecture

The MailPigeon system consists of three interconnected repositories:

### 1. [mailpigeon-prisma](https://github.com/MailPigeonApp/mailpigeon-prisma)

**Database Schema & ORM Layer**

The TypeScript/Prisma project that defines the core data model for the entire system.

- **Technology**: TypeScript, Prisma ORM, PostgreSQL
- **Core Entities**: Users, Nests (projects), Submissions, API Keys
- **Purpose**: Centralized database schema management and migrations

**Key Features**:

- User authentication and management
- Project organization via "Nests"
- JSON-based submission storage
- API key authentication at the user-nest level

### 2. [mailpigeon-api](https://github.com/MailPigeonApp/mailpigeon-api)

**Production API Service**

The production-ready PHP API backend deployed on Fly.io.

- **Technology**: Leaf PHP v3.0, PostgreSQL, AWS S3, Docker
- **Deployment**: Fly.io (London region)
- **Purpose**: Production API endpoints for form submission and file handling

**Key Features**:

- Bearer token authentication
- Dynamic field validation based on project configuration
- AWS S3 file upload support
- Telegram integration for notifications
- CORS-enabled for web clients
- Auto-scaling infrastructure

**API Endpoints**:

- `POST /api/v1/submit` - Main form submission
- `POST /api/v1/upload` - File uploads to S3

### 3. [mailpigeon-backend](https://github.com/MailPigeonApp/mailpigeon-backend)

**Local Development Backend**

A simplified local development version for testing and feature development.

- **Technology**: Leaf PHP v3.0, MySQL
- **Purpose**: Local development and testing environment
- **Status**: Development version with core validation logic

**Differences from Production**:

- Uses MySQL instead of PostgreSQL
- No AWS S3 integration
- No external integrations (Telegram, etc.)
- Simplified deployment (PHP built-in server)

## Getting Started

### For API Users

1. Set up your database using [mailpigeon-prisma](https://github.com/MailPigeonApp/mailpigeon-prisma)
2. Deploy [mailpigeon-api](https://github.com/MailPigeonApp/mailpigeon-api) to Fly.io or your preferred hosting
3. Configure environment variables for database and AWS S3
4. Generate API keys and start submitting forms

### For Local Development

1. Clone [mailpigeon-backend](https://github.com/MailPigeonApp/mailpigeon-backend)
2. Install dependencies: `composer install`
3. Configure `.env` with local MySQL credentials
4. Run: `php -S localhost:8000`

## Technology Stack

- **Backend**: Leaf PHP Framework (lightweight micro-framework)
- **Database**: PostgreSQL (production), MySQL (development)
- **ORM**: Prisma (schema management), Leaf DB (runtime queries)
- **File Storage**: AWS S3
- **Deployment**: Docker, Fly.io
- **Languages**: TypeScript (schema), PHP (API)

## System Flow

1. **Schema Definition**: Database structure defined in `mailpigeon-prisma`
2. **Project Configuration**: Projects define expected field types and validation rules
3. **API Authentication**: Clients authenticate using Bearer tokens (API keys)
4. **Form Submission**: Data validated against project field configuration
5. **File Handling**: Optional file uploads to S3 with public URLs
6. **Integrations**: Trigger external services (Telegram notifications)
7. **Storage**: Validated submissions stored as JSON in database

## Contributing

We welcome contributions to any of the three repositories! Each repository contains detailed documentation in its `CLAUDE.md` file to help you understand the codebase architecture and development workflow.

## License

Please check individual repositories for license information.

## Support

For issues, questions, or contributions, please open an issue in the relevant repository:

- [mailpigeon-prisma issues](https://github.com/MailPigeonApp/mailpigeon-prisma/issues)
- [mailpigeon-api issues](https://github.com/MailPigeonApp/mailpigeon-api/issues)
- [mailpigeon-backend issues](https://github.com/MailPigeonApp/mailpigeon-backend/issues)
