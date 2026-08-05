# Research Profile Management Module

## Milestone 1

### Module Assigned
**Research Profile Management**

### Objective
Develop the backend module for managing researcher profiles in the Funding & Innovation Platform. The module enables authenticated users to create, view, update, delete, and search research profiles.

### Milestone 1 Deliverables

- Designed and understood the Research Profile database schema.
- Worked with the `users` and `research_profiles` tables.
- Implemented the Research Profile CRUD APIs.
- Added profile listing API.
- Added search by research domain API.
- Added search by keywords API.
- Configured and ran the FastAPI backend.
- Connected the backend with PostgreSQL using SQLAlchemy.
- Verified the Registration API using Swagger UI.
- Successfully pushed the implementation to the `kesiya-dev` branch.

---

## Overview

The Research Profile Management module is a part of the Funding & Innovation Platform. It allows researchers to create, manage, search, and delete their research profiles. The module is developed using FastAPI, SQLAlchemy, and PostgreSQL.

---

## Features

- User Registration
- User Authentication (JWT)
- Create or Update Research Profile
- View Research Profile
- Delete Research Profile
- List All Research Profiles
- Search Research Profiles by Research Domain
- Search Research Profiles by Keywords

---

## Database Design

### Users Table

| Column | Description |
|---------|-------------|
| id | Primary Key |
| full_name | User's Full Name |
| email | Unique Email Address |
| password_hash | Encrypted Password |
| role | User Role |
| organization | Organization Name |
| created_at | Account Creation Time |

### Research Profiles Table

| Column | Description |
|---------|-------------|
| id | Primary Key |
| user_id | Foreign Key (Users Table) |
| research_domains | Research Domains |
| keywords | Research Keywords |
| publications | Publications |
| patents | Patents |
| technology_areas | Technology Areas |
| created_at | Profile Creation Time |

The `research_profiles` table is linked to the `users` table using the `user_id` foreign key.

---

## APIs

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /register | Register a new user |
| POST | /login | User Login |
| POST | /profile | Create or Update Research Profile |
| GET | /profile | View Logged-in User Profile |
| DELETE | /profile | Delete Research Profile |
| GET | /profiles | List All Research Profiles |
| GET | /profiles/domain/{domain} | Search Profiles by Research Domain |
| GET | /profiles/keyword/{keyword} | Search Profiles by Keywords |

---

## Technologies Used

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL
- MongoDB
- Docker
- Swagger UI
- JWT Authentication

---


## Work Completed

- Set up the backend development environment.
- Configured Docker containers for PostgreSQL and MongoDB.
- Understood the database schema and relationships.
- Studied the Research Profile Management workflow.
- Implemented and verified the Research Profile CRUD APIs.
- Added profile listing API.
- Added search by research domain API.
- Added search by keywords API.
- Successfully tested the Registration API using Swagger.
- Backend server and Swagger documentation are running successfully.
- Pushed the completed implementation to the `kesiya-dev` GitHub branch.

---



## Author

**Kesiya Sunny**

**Module:** Research Profile Management

**Milestone:** Milestone 1

**Project:** Funding & Innovation Platform
