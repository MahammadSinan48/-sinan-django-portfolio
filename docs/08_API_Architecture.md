Dynamic Portfolio Website
API Architecture Document
Project Name : Dynamic Portfolio Website
Version      : 1.0.0
Document Type: API Architecture
Framework    : Django REST Framework (DRF)
Database     : PostgreSQL
Author       : Mahammad Sinan
Status       : Planning Phase
Table of Contents
1. Introduction

2. Purpose

3. API Overview

4. REST API Principles

5. API Architecture

6. API Modules

7. Endpoint Structure

8. Authentication & Authorization

9. Request Lifecycle

10. Request & Response Format

11. HTTP Methods

12. Status Codes

13. API Versioning

14. Serializer Architecture

15. View Architecture

16. URL Routing

17. Pagination

18. Filtering & Searching

19. Validation Strategy

20. Error Handling

21. Rate Limiting

22. API Security

23. API Documentation

24. Future API Expansion

25. Conclusion
1. Introduction
Overview

The Dynamic Portfolio Website provides a RESTful API built with Django REST Framework (DRF). The API enables frontend applications, mobile apps, and external services to securely access and manage portfolio data.

The API follows REST principles, uses JSON for data exchange, and is designed to be scalable, maintainable, and secure.

2. Purpose

This document defines the API architecture used by the application.

It describes:

API structure
Endpoints
Authentication
Request flow
Validation
Error handling
Security
Versioning

The API is designed to support both the web application and future mobile clients.

3. API Overview

The API exposes the following resources:

Portfolio
Projects
Skills
Technologies
Education
Experience
Certificates
Achievements
Publications
Blogs
Contact Messages
Subscribers
Analytics
Site Settings

Data is exchanged using JSON over HTTPS.

4. REST API Principles

The API follows these principles:

Resource-based URLs
Stateless communication
JSON request/response format
Proper HTTP methods
Standard HTTP status codes
Secure authentication
Predictable endpoints
5. API Architecture
Client
   │
   ▼
REST API
   │
   ▼
URL Router
   │
   ▼
APIView / ViewSet
   │
   ▼
Serializer
   │
   ▼
Model
   │
   ▼
PostgreSQL
6. API Modules
Module	Purpose
Portfolio API	Portfolio information
Projects API	Project management
Skills API	Technical skills
Blog API	Blog articles
Contact API	Contact messages
Analytics API	Visitor statistics
Settings API	Site configuration
7. Endpoint Structure
/api/v1/

│

├── projects/

├── skills/

├── technologies/

├── education/

├── experience/

├── certificates/

├── achievements/

├── publications/

├── blogs/

├── categories/

├── tags/

├── contact/

├── subscribers/

├── analytics/

└── settings/

Example:

GET    /api/v1/projects/
GET    /api/v1/projects/5/
POST   /api/v1/contact/
8. Authentication & Authorization

The API supports:

Public Endpoints
Portfolio
Projects
Blogs
Skills
Education
Experience
Protected Endpoints
Dashboard
Analytics
Site Settings
Content Management

Authentication options:

Django Session Authentication
Token Authentication (future)
JWT Authentication (future)

Permissions are managed using Django REST Framework permission classes.

9. Request Lifecycle
Client

↓

HTTP Request

↓

URL Router

↓

APIView/ViewSet

↓

Serializer Validation

↓

Business Logic

↓

Model

↓

Database

↓

Serializer

↓

JSON Response

↓

Client
10. Request & Response Format
Request Example
{
    "name": "John Doe",
    "email": "john@example.com",
    "message": "Hello!"
}
Success Response
{
    "success": true,
    "message": "Contact message submitted successfully."
}
Error Response
{
    "success": false,
    "errors": {
        "email": [
            "This field is required."
        ]
    }
}
11. HTTP Methods
Method	Purpose
GET	Retrieve data
POST	Create new record
PUT	Replace record
PATCH	Partial update
DELETE	Delete record
12. Status Codes
Code	Meaning
200	OK
201	Created
204	No Content
400	Bad Request
401	Unauthorized
403	Forbidden
404	Not Found
500	Internal Server Error
13. API Versioning

The API uses URL versioning.

Example:

/api/v1/projects/
/api/v2/projects/

Benefits:

Backward compatibility
Easier upgrades
Stable client integrations
14. Serializer Architecture

Serializers handle:

Input validation
Data conversion
JSON serialization
Deserialization

Example serializers:

ProjectSerializer
BlogSerializer
SkillSerializer
ContactSerializer
15. View Architecture

The project primarily uses DRF ModelViewSet and ReadOnlyModelViewSet where appropriate.

Example:

ProjectViewSet
BlogViewSet
SkillViewSet
ContactAPIView

Responsibilities:

Handle requests
Apply permissions
Return serialized data
16. URL Routing
config/urls.py

│

└── api/

        │

        ├── portfolio/

        ├── blog/

        ├── contact/

        ├── analytics/

        └── settings/

Each module maintains its own urls.py for modularity.

17. Pagination

Large datasets will use pagination.

Default strategy:

Page Number Pagination

Example:

GET /api/v1/blogs/?page=2

Benefits:

Faster responses
Reduced bandwidth
Better scalability
18. Filtering & Searching

Supported features:

Search by keyword
Category filtering
Tag filtering
Featured projects
Date filtering
Ordering

Example:

/api/v1/projects/?featured=true
/api/v1/blogs/?category=django
/api/v1/blogs/?search=python
19. Validation Strategy

Validation occurs at multiple layers:

Serializer validation
Model validation
Database constraints

Examples:

Required fields
Email validation
URL validation
Unique slug validation
File type validation
20. Error Handling

The API returns consistent JSON error responses.

Example:

{
    "success": false,
    "message": "Validation failed.",
    "errors": {
        "title": [
            "This field is required."
        ]
    }
}

Custom exception handling will provide a uniform response format.

21. Rate Limiting

To protect the API from abuse:

Anonymous user throttling
Authenticated user throttling
Contact endpoint rate limiting

This can be configured using Django REST Framework throttling classes.

22. API Security

Security measures include:

HTTPS in production
Authentication and permissions
CSRF protection (session-based endpoints)
Input validation
SQL injection prevention
XSS protection
CORS configuration
Secure environment variables
23. API Documentation

The API will be documented using:

OpenAPI Specification
Swagger UI
ReDoc

Documentation will include:

Endpoint descriptions
Parameters
Request bodies
Response schemas
Authentication requirements
Example requests and responses
24. Future API Expansion

Future enhancements include:

JWT Authentication
OAuth2 integration
GraphQL API
Webhooks
Real-time notifications (WebSockets)
Mobile application APIs
AI assistant endpoints
Public developer API
25. Conclusion

The API Architecture establishes a scalable and secure communication layer for the Dynamic Portfolio Website. By following REST principles and leveraging Django REST Framework, the application provides well-structured, maintainable, and extensible APIs. This design supports current web functionality while preparing the project for future mobile applications, third-party integrations, and advanced services.

