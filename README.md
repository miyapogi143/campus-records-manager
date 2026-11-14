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

The included `render.yaml` creates an independent free web service with auto-deploy enabled. Since a Render workspace can have only one active free PostgreSQL database, this free setup uses SQLite on the service filesystem. SQLite data on Render is not durable and can be lost when the service restarts or redeploys. Use PostgreSQL for persistent records.

Connect this repository as a new Render Blueprint; do not attach it to the existing student-record service. To provision a staff account on the free SQLite deployment, set `BOOTSTRAP_ADMIN_USERNAME` and `BOOTSTRAP_ADMIN_PASSWORD` in the Render environment before deploying. The build command creates the account only if it does not already exist. Because the database is rebuilt from scratch on redeploy, keep those values in Render (never in Git) if you need the staff account recreated after a redeploy. For persistent records and safer one-time credential handling, use PostgreSQL.
