Dynamic Portfolio Website
Database Architecture Document
Project Name : Dynamic Portfolio Website
Version      : 1.0.0
Document Type: Database Architecture Document
Framework    : Django
Database     : PostgreSQL
Author       : Mahammad Sinan
Status       : Planning Phase
1. Introduction
Overview

The Dynamic Portfolio Website relies on a relational database to manage structured information such as user profiles, projects, skills, education, work experience, certifications, blogs, contact messages, analytics, and site settings.

The database is designed using PostgreSQL and follows relational database principles to ensure data integrity, scalability, security, and efficient querying. It serves as the central data layer of the application and interacts with Django through the Django ORM.

This document describes the database architecture, design principles, entity relationships, indexing strategy, normalization rules, and future scalability plans.

2. Database Design Goals

The database has been designed with the following objectives:

Maintain data consistency and integrity.
Minimize data redundancy.
Support efficient CRUD operations.
Provide fast query performance.
Enable easy scalability for future modules.
Maintain referential integrity.
Support secure storage of sensitive information.
Integrate seamlessly with Django ORM.
Simplify maintenance and migrations.
Ensure compatibility with cloud deployment.
3. Database Architecture Overview

The project follows a layered database architecture.

Application Layer
        │
        ▼
Django ORM
        │
        ▼
PostgreSQL Database
        │
        ▼
Physical Storage
Responsibilities

Application Layer

Business logic
Validation
Data processing

Django ORM

SQL generation
Model mapping
Query optimization
Migrations

PostgreSQL

Data storage
Transactions
Constraints
Indexes
4. Database Selection (Why PostgreSQL?)

PostgreSQL has been selected because it provides enterprise-grade features and integrates seamlessly with Django.

Advantages
Open source and highly reliable.
ACID-compliant transactions.
Excellent Django ORM support.
Advanced indexing capabilities.
Foreign key enforcement.
JSON and JSONB support.
Full-text search capabilities.
Scalability for large datasets.
Strong security features.
Active community support.
Why Not SQLite?

SQLite is suitable for development but has limitations for concurrent access and production workloads.

Why Not MySQL?

While MySQL is a capable relational database, PostgreSQL offers richer SQL features, stronger standards compliance, advanced indexing, and better support for complex queries, making it well suited for scalable Django applications.

5. Database Normalization

The database follows normalization principles to reduce redundancy and improve maintainability.

First Normal Form (1NF)
Atomic values only.
No repeating groups.
Second Normal Form (2NF)
Every non-key attribute depends on the whole primary key.
Third Normal Form (3NF)
No transitive dependencies.
Benefits
Reduced redundancy.
Improved consistency.
Easier maintenance.
Better scalability.
6. Naming Conventions

To maintain consistency across the project:

Tables
Singular model names in Django (e.g., Project, Skill).
Snake_case for database table names where explicitly defined.
Columns
created_at
updated_at
is_active
slug
title
description
Primary Keys
id (BigAutoField)
Foreign Keys
<entity>_id
Index Names
idx_project_title
idx_blog_slug
7. Entity Overview

The application consists of the following core entities:

User Management
User
UserProfile
SocialLink
Resume
Portfolio
Skill
SkillCategory
Technology
Project
ProjectCategory
ProjectImage
Education
Experience
Certificate
Achievement
Publication
Gallery
Blog
Blog
BlogCategory
Tag
Communication
ContactMessage
Subscriber
Analytics
Visitor
VisitorPage
Administration
SiteSetting
Testimonial

Each entity is responsible for a single domain of the application, promoting a modular and maintainable data model.

8. Entity Relationships

The database uses a combination of one-to-one, one-to-many, and many-to-many relationships.

One-to-One
User → UserProfile
User → Resume
One-to-Many
User → Project
User → Certificate
User → Blog
ProjectCategory → Project
BlogCategory → Blog
Many-to-Many
Project ↔ Technology
Blog ↔ Tag

These relationships are enforced using foreign keys and Django ORM relationship fields.

9. Table Specifications

Each table will be documented with:

Purpose
Columns
Data Types
Primary Key
Foreign Keys
Constraints
Default Values
Indexes
Relationships

Example:

Table	Purpose
UserProfile	Stores personal profile information
Project	Stores portfolio projects
Skill	Stores technical skills
Blog	Stores blog articles
ContactMessage	Stores contact form submissions

Detailed table specifications will be documented separately as the data model is finalized.

10. Primary Keys Strategy

The project uses:

BigAutoField

Advantages:

Globally unique within the database.
Efficient indexing.
Better support for future scalability.

Each table will have a single primary key.

11. Foreign Keys Strategy

Foreign keys enforce referential integrity between related tables.

Examples:

project.category_id
blog.category_id
project.user_id

Benefits:

Prevent orphan records.
Maintain consistent relationships.
Simplify joins and ORM queries.
12. Constraints & Validation

The database will enforce:

NOT NULL

Required fields cannot be empty.

UNIQUE

Fields such as email, username, and slug must be unique where applicable.

CHECK Constraints

Used for validating numeric ranges or predefined values when appropriate.

Default Values

Applied for status flags, timestamps, and other common fields.

Validation will also be performed at the Django model and form/serializer layers.

13. Indexing Strategy

Indexes improve query performance.

Planned indexes include:

Primary Key indexes.
Foreign Key indexes.
Slug indexes.
Email indexes.
Title indexes.
Created date indexes.
Composite indexes for frequently filtered fields where justified.

Index usage will be reviewed after profiling to avoid unnecessary overhead.

14. Transactions & Data Integrity

The application will use PostgreSQL transactions to ensure data consistency.

Strategies:

Atomic operations.
Rollback on failures.
Referential integrity.
Cascading updates/deletes only where appropriate.

Django's transaction management will be used for multi-step operations.

15. Backup & Recovery Strategy

Backup strategy:

Scheduled automated database backups.
Secure off-site storage where applicable.
Periodic restore testing.

Recovery plan:

Restore from the latest verified backup.
Validate data integrity after restoration.
16. Database Security

Security measures include:

Strong authentication.
Restricted database privileges.
Encrypted connections (SSL/TLS) in production.
Environment variables for credentials.
Regular updates and security patches.
Principle of least privilege for database users.
17. Performance Optimization

Performance strategies include:

Proper indexing.
Query optimization using Django ORM.
select_related() and prefetch_related() where appropriate.
Pagination for large datasets.
Lazy loading of related content.
Caching frequently accessed data.
Monitoring slow queries.
18. Future Database Expansion

The database is designed to accommodate future enhancements such as:

Multi-user portfolio support.
Team and organization profiles.
Comments and discussions.
Notifications.
Job application tracking.
AI-assisted content generation.
Portfolio themes.
Audit logs.
Additional analytics.
Multi-language content.

These features can be integrated with minimal changes to the existing schema.

19. Database Diagram Reference

The Entity Relationship (ER) Diagram will be documented in:

docs/05_ER_Diagram.md

Additional diagrams:

docs/diagrams/
├── er_diagram.png
├── er_diagram.svg
└── er_diagram.mmd

The ER diagram will visually represent:

Entities
Attributes
Relationships
Cardinality
Primary Keys
Foreign Keys
20. Conclusion

The Database Architecture establishes a robust, scalable, and maintainable foundation for the Dynamic Portfolio Website. By leveraging PostgreSQL, normalization principles, well-defined relationships, indexing strategies, and security best practices, the design supports both current application requirements and future growth. This document serves as the blueprint for implementing Django models, migrations, APIs, and administrative functionality while ensuring long-term maintainability and performance.