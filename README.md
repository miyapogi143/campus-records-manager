# Campus Ledger

A standalone student records system for campus staff, built with Django. It provides a dashboard, searchable student and course directories, enrollment and grade tracking, and CSV export.

## Features

- Staff-only authentication and record management
- Student profiles, statuses, and academic year/section
- Course catalog with active/inactive state
- Enrollment records for school year and semester
- Prelim, midterm, and final grades with a computed average
- Search across students, courses, and enrollments
- Student CSV export
- Responsive dashboard and interface

## Run locally

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open `http://127.0.0.1:8000/`. Sign in with the staff account created above. SQLite is used by default; setting `DATABASE_URL` enables a managed PostgreSQL database.

## Deploy to Render

The included `render.yaml` creates an independent web service and PostgreSQL database with auto-deploy enabled. Connect this repository as a new Render Blueprint; do not attach it to the existing student-record service.

To provision the first staff account, temporarily add `BOOTSTRAP_ADMIN_USERNAME` and `BOOTSTRAP_ADMIN_PASSWORD` in the new Render service's environment, then deploy. The build command creates the account only if it does not already exist. Remove both variables after the successful deployment and redeploy to avoid retaining the one-time password in service configuration.
