# Backend

Django REST API for League Stat-Us.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python manage.py migrate
python manage.py loaddata fixtures/demo_data.json
python manage.py runserver
```

## Main apps

- `users` - custom user model and role workflows
- `scheduling` - teams and games
- `analytics` - attendance and match results
- `games` - game app scaffold
- `notifications` - notification scaffold
