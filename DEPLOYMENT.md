# Deploying to Render

This app is configured for Render with `render.yaml`.

## Render settings

- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn app:app`
- Health check path: `/healthz`

## PostgreSQL setup

Set this environment variable in Render:

- `DATABASE_URL`

Use the PostgreSQL internal connection URL from your Render database. Do not commit the URL to GitHub because it contains the database password.

## Initialize the database

The app creates the required tables automatically on first database use. `database.sql` is also included if you prefer to initialize the schema manually from Render's database shell or another PostgreSQL client.

## Troubleshooting

After deployment, open `/healthz/db` on your Render app URL. It returns the configured database host, port, user, database name, and the PostgreSQL connection error without exposing the password.

Common fixes:

- Make sure `DATABASE_URL` starts with `postgresql://` or `postgres://`.
- Use the Render PostgreSQL internal URL when the web service and database are in the same Render region.
- Open `/healthz/db` after deployment to confirm the app can connect and initialize the schema.
- If tables already exist from an older failed setup, drop/recreate them or run the schema manually.
