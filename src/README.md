# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Project Structure

```
.
├── src/
│   ├── app.py                 # Main FastAPI application with API endpoints
│   └── static/
│       ├── index.html         # Frontend HTML UI
│       ├── app.js             # Frontend JavaScript for activities and sign-ups
│       └── styles.css         # CSS styling for the web interface
├── pyproject.toml             # Project metadata and dependency configuration
├── uv.lock                    # Locked dependency versions (auto-generated)
├── .python-version            # Python version specification
├── pytest.ini                 # Pytest configuration
├── requirements.txt           # Legacy pip requirements (see pyproject.toml)
└── README.md                  # This file
```

### File Descriptions

- **app.py** - FastAPI application with:
  - In-memory database of activities
  - API endpoints for fetching activities and signing up
  - Static file serving for the web interface

- **index.html** - Interactive web interface with:
  - Activity listing with current availability
  - Student sign-up form

- **app.js** - Frontend logic for:
  - Fetching activities from the API
  - Handling form submissions
  - Displaying success/error messages

- **styles.css** - Responsive styling for desktop and mobile

## Getting Started

1. Install `uv` (if not already installed):

   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh  # macOS/Linux
   # or for Windows: powershell -ExecutionPolicy BypassUser -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

2. Install dependencies and set up the virtual environment:

   ```bash
   uv sync
   ```

3. Run the application:

   ```bash
   uv run python app.py
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## Running the Application

### Start the Server

From the project root directory:

```bash
uv run python src/app.py
```

Or with auto-reload enabled for development:

```bash
uv run uvicorn src.app:app --reload
```

### Access the Web Interface

Open your browser and navigate to:

**http://localhost:8000**

This will take you to the interactive UI where you can:
- View all available extracurricular activities
- See remaining spots for each activity
- Sign up for activities using your student email
- View confirmation or error messages

### API Documentation

Explore and test the API directly using interactive documentation:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Test the API with curl

```bash
# Get all activities
curl http://localhost:8000/activities

# Sign up for an activity
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=student@mergington.edu"
```

### Stop the Server

Press `Ctrl+C` in the terminal to stop the application.

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.

## Project Setup

This project uses **uv** for fast and reliable Python package management. Key files:

- `pyproject.toml` - Project metadata and dependencies
- `uv.lock` - Locked dependency versions for reproducible builds
- `.python-version` - Python version specification (3.11)

### Useful `uv` Commands

```bash
uv sync              # Install/sync all dependencies
uv add <package>     # Add a new dependency
uv add --dev <pkg>   # Add a dev dependency
uv run <command>     # Run a command in the virtual environment
uv pip <command>     # Use pip-compatible commands if needed
```

## Available Activities

The API comes pre-loaded with sample activities:

1. **Chess Club**
   - Schedule: Fridays, 3:30 PM - 5:00 PM
   - Max Participants: 12

2. **Programming Class**
   - Schedule: Tuesdays and Thursdays, 3:30 PM - 4:30 PM
   - Max Participants: 20

3. **Gym Class**
   - Schedule: Mondays, Wednesdays, Fridays, 2:00 PM - 3:00 PM
   - Max Participants: 30

## Development

### Dependencies

**Core:**
- fastapi - Modern web framework
- uvicorn - ASGI server
- httpx - HTTP client library

**Development (optional):**
- pytest - Testing framework
- pytest-asyncio - Async test support

### Testing

```bash
uv run pytest
```

### Troubleshooting

- **Port 8000 already in use?** Specify a different port: `uv run uvicorn src.app:app --port 8001`
- **Data not persisting?** The API uses in-memory storage, so data resets on server restart
