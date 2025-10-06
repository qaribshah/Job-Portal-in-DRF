# Job Portal REST API

A comprehensive RESTful API for a modern job portal platform built with Django REST Framework. This application serves as a complete backend solution for connecting companies with talent, providing robust job posting, application tracking, and candidate management capabilities.

## 🚀 Features

- **Advanced Authentication System**: JWT-based authentication with refresh tokens and Google OAuth integration
- **Complete Job Ecosystem**: Sophisticated job posting and management with full CRUD operations
- **Company Profiles**: Detailed company profiles with hiring metrics and team management
- **Applicant Tracking System**: Professional-grade tracking system for applicants through the hiring pipeline
- **Intelligent Application Processing**: Smart ranking and filtering of applications based on qualifications
- **Advanced Filtering & Search**: Powerful search with multiple parameters, including skill-based filtering
- **Google OAuth Integration**: Secure sign-in with Google accounts for seamless user authentication
- **Responsive Pagination**: Customizable pagination for optimal performance with large datasets
- **Hierarchical Resources**: Sophisticated nested resources for complex data relationships
- **Extensive API Documentation**: Detailed documentation for all endpoints

## 🛠️ Tech Stack

- **Backend**: Python 3.12, Django 5.2.6
- **API Framework**: Django REST Framework 3.16.1
- **Authentication**: Django REST Framework SimpleJWT, Django AllAuth with Google OAuth
- **Database**: SQLite (development)
- **Filtering**: Django Filter, Custom filters
- **Routing**: Django Nested Routers
- **External APIs**: Google OAuth API for social authentication
- **Security**: JWT with refresh tokens
- **Testing**: Django's built-in testing framework

## 🏗️ Project Architecture

This project follows a modular, microservices-inspired architecture with clear separation of concerns:

- `api`: Core API gateway, routing, and central configuration
- `jobs`: Comprehensive job posting and management system
- `applicants`: Advanced applicant profiles with skill matching
- `applications`: Full-featured application processing pipeline
- `employees`: Employee management for corporate users
- `accounts`: Enterprise-grade authentication system
- `resumes`: Secure document storage with parsing capabilities

Each module is designed to scale independently and communicate through well-defined interfaces, ensuring maintainability and allowing for future expansion.

## Setup Instructions

### Prerequisites

- Python 3.12+
- pip
- virtualenv (recommended)

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd job-portal-rest
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv env
   source env/bin/activate  # On Windows, use: env\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the project root with the following variables:
   ```
   # Core Django settings
   SECRET_KEY=your_secret_key_here
   DEBUG=True
   DATABASE_URL=sqlite:///db.sqlite3
   ALLOWED_HOSTS=localhost,127.0.0.1
   
   # Email configuration
   EMAIL_HOST=smtp.example.com
   EMAIL_PORT=587
   EMAIL_HOST_USER=your_email@example.com
   EMAIL_HOST_PASSWORD=your_email_password
   EMAIL_USE_TLS=True
   
   # JWT Configuration
   JWT_SECRET_KEY=your_jwt_secret_key
   JWT_ALGORITHM=HS256
   JWT_ACCESS_TOKEN_LIFETIME=60 # in minutes
   JWT_REFRESH_TOKEN_LIFETIME=7 # in days
   
   # Google OAuth
   GOOGLE_OAUTH_CLIENT_ID=your_google_client_id
   GOOGLE_OAUTH_CLIENT_SECRET=your_google_client_secret
   ```

5. Apply migrations:
   ```bash
   cd job_portal_main
   python manage.py migrate
   ```

6. Create a superuser:
   ```bash
   python manage.py createsuperuser
   ```

7. Run the development server:
   ```bash
   python manage.py runserver
   ```

## 🔄 API Endpoints

This API follows RESTful conventions with a comprehensive suite of endpoints:

### Authentication

- `POST /api/token/`: Obtain JWT tokens
- `POST /api/token/refresh/`: Refresh JWT tokens
- `POST /api/token/verify/`: Verify token validity
- `GET /accounts/google/login/`: Initiate Google OAuth login
- `GET /accounts/google/callback/`: Google OAuth callback URL

### Jobs

- `GET /jobs/`: List all jobs with filtering
- `POST /jobs/`: Create a new job posting
- `GET /jobs/{id}/`: Get detailed job information
- `PUT /jobs/{id}/`: Update job details
- `PATCH /jobs/{id}/`: Partially update job
- `DELETE /jobs/{id}/`: Remove job posting
- `GET /jobs/{id}/applications/`: List all applications for a specific job

### Companies

- `GET /companies/`: List all companies
- `POST /companies/`: Create a new company
- `GET /companies/{id}/`: Get company details
- `PUT /companies/{id}/`: Update company information
- `GET /companies/{id}/jobs/`: List all jobs posted by a company

### Applicants

- `GET /applicants/`: List all applicants with filtering
- `POST /applicants/`: Create a new applicant profile
- `GET /applicants/{id}/`: Get applicant details
- `PUT /applicants/{id}/`: Update applicant information
- `GET /applicants/{id}/applications/`: List applications by an applicant

### Applications

- `GET /jobs/{job_id}/applications/`: List applications for a job
- `POST /jobs/{job_id}/applications/`: Submit application for a job
- `GET /jobs/{job_id}/applications/{id}/`: Get specific application details
- `PUT /jobs/{job_id}/applications/{id}/status/`: Update application status
- `GET /applicants/{applicant_id}/applications/`: List all applications by an applicant

## 🔍 Advanced Filtering

The API supports sophisticated filtering mechanisms:

### Job Filtering
```
/jobs/?job_title=Software Engineer&location=New York&min_salary=80000&skills=python,django
```

### Applicant Filtering
```
/applicants/?name=John&email=john@example.com&contact=123456789
```

## 📄 Pagination

API responses are paginated for better performance:

```
/jobs/?page=2&jobs_per_page=20
```

Results include comprehensive metadata:
```json
{
  "count": 135,
  "next": "https://api.example.com/jobs/?page=3",
  "previous": "https://api.example.com/jobs/?page=1",
  "results": [...]
}
```

## 🔐 Authentication

The system implements a secure authentication approach:

### JWT Authentication
API endpoints require authentication with JWT tokens.

Include the JWT token in the header of your requests:
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Google OAuth Authentication

Users can authenticate using their Google accounts, providing a seamless and secure login experience:

1. Users are redirected to Google for authentication
2. Upon successful authentication, they are redirected back to the application
3. A JWT token is issued for subsequent API calls

### Token Lifecycle

- Access tokens expire after the configured lifetime (default: 60 minutes)
- Refresh tokens allow obtaining new access tokens

### Permission Levels

- Anonymous: Limited to public job listings
- Applicants: Access to own profile and applications
- Employers: Access to own company, jobs, and received applications
- Admins: Full access to all resources

## 🧪 Development

### Running Tests

```bash
# Run all tests
python manage.py test

# Run specific test modules
python manage.py test jobs.tests applications.tests
```

### Local Development

```bash
# Run development server
python manage.py runserver

# Create new app module
python manage.py startapp new_feature

# Generate database migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate
```

##  Performance

This API is designed for good performance:
- Query optimization with select_related/prefetch_related
- Optimized ORM queries
- Pagination to handle large datasets

## 📜 License

[MIT License](LICENSE)

## 👨‍💻 Contributors

- Your Name - Lead Developer

---

**Note**: Before running the application, ensure you have created a `.env` file with all required credentials as shown in the setup instructions, especially your Google OAuth credentials for social authentication. The `.env` file contains sensitive information and should never be committed to version control.