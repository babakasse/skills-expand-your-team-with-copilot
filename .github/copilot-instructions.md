### Copilot Instructions

This repository contains a FastAPI-based high school management system for Mergington High School, serving 400-600 students across grades 9-12. The system allows students to view and sign up for extracurricular activities.

## Project Overview

**Languages & Frameworks**: Python 3.13, FastAPI, Uvicorn, MongoDB (optional)
**Type**: Web application with REST API and static frontend
**Architecture**: Simple backend API with HTML/CSS/JavaScript frontend

## Development Environment Setup

**Required**: GitHub Codespaces (recommended) or local Python 3.13+ environment

1. Install dependencies:
   ```bash
   pip install -r src/requirements.txt
   ```

2. Run the application:
   ```bash
   python -m uvicorn src.app:app --host 0.0.0.0 --port 8000 --reload
   ```
   
   Or use VS Code debugger: Select "Launch Mergington WebApp" configuration and press F5

3. Access the application:
   - Frontend: http://localhost:8000/
   - API docs: http://localhost:8000/docs
   - Alternative docs: http://localhost:8000/redoc

**Important**: Data is stored in memory. Server restarts reset all data.

## Build, Test, and Validation

**No formal build step required** - Python application runs directly
**No test suite currently exists** - Manual testing via browser and API docs
**No linting configuration** - Code should follow PEP 8 conventions

To validate changes:
1. Start the server with the command above
2. Test endpoints via http://localhost:8000/docs
3. Test frontend via http://localhost:8000/
4. Verify server logs show no errors

## Project Structure

```
src/
├── app.py                      # Main FastAPI application entry point
├── requirements.txt            # Python dependencies (FastAPI, Uvicorn, etc.)
├── backend/
│   ├── database.py            # In-memory database and initialization
│   └── routers/
│       ├── activities.py      # Activities endpoints (GET /activities, POST /activities/{name}/signup)
│       └── auth.py            # Authentication endpoints
└── static/                     # Frontend HTML/CSS/JavaScript files

.github/
├── copilot-instructions.md     # This file - repository-wide instructions
├── copilot-instructions-ext.md # Extended instructions with school context
└── workflows/                  # GitHub Actions for course automation

docs/
└── how-to-develop.md          # Detailed development guide

.vscode/
└── launch.json                # VS Code debugger configuration

.devcontainer/
└── devcontainer.json          # Codespaces configuration
```

## Key Architectural Facts

1. **Entry Point**: `src/app.py` - Creates FastAPI app, mounts static files, includes routers
2. **Routing**: API routes in `src/backend/routers/` - activities and auth modules
3. **Data Storage**: In-memory database in `src/backend/database.py` - no persistence
4. **Static Files**: Served from `src/static/` via FastAPI's StaticFiles at `/static` path
5. **Root Route**: Redirects to `/static/index.html`

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/activities` | Get all activities with participant counts |
| POST | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity |

## Dependencies

Core dependencies from `src/requirements.txt`:
- `fastapi==0.115.12` - Web framework
- `uvicorn==0.34.2` - ASGI server
- `pymongo==4.12.1` - MongoDB driver (optional, for future persistence)
- `argon2==0.1.10` and `argon2-cffi==23.1.0` - Password hashing

Always install dependencies before running: `pip install -r src/requirements.txt`

## User Interaction Guidelines

**Target Users**: Non-technical school staff (students and teachers)
- Use simple terms, avoid jargon
- Code must be easy to maintain without significant coding experience
- User experience should be simple and intuitive

## Code Conventions

1. **Languages Only**: HTML, CSS, JavaScript, Python - No other languages
2. **No CLI tools** - Web interface only
3. **No microservices** - Single application architecture
4. **File Organization**: Use clear directory structure, avoid long single files
5. **Documentation**: Always update README.md; move to `docs/` when too long
6. **Testing**: Create unit tests for grade/score calculations and numerical data
7. **Security**: 
   - Never hardcode secrets or passwords
   - Implement proper login/logout flows
   - Privacy and security are critical (personal student information)

## School Context

For additional context about Mergington High School (name, motto, schedules, roles), see `.github/copilot-instructions-ext.md`.

## Important Notes

- This is a training/exercise repository with GitHub Actions workflows for course automation
- Focus changes in `src/` directory for application code
- The application uses FastAPI's auto-reload during development
- No GitHub Actions CI/CD for application testing - workflows are for course management
