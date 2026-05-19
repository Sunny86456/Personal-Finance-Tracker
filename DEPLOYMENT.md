# Deploying to Render

This app is configured for Render with `render.yaml`.

## Render settings

- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn app:app`
- Health check path: `/healthz`

## Required environment variables

Set these in Render before deploying:

- `MYSQL_HOST`
- `MYSQL_PORT` (usually `3306`)
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `MYSQL_DB`
- `MYSQL_SSL` (`true` if your MySQL provider requires SSL, otherwise `false`)

Many hosted MySQL providers also give a single connection string. You can set this instead of the separate MySQL fields:

- `DATABASE_URL=mysql://user:password@host:3306/database_name`

`SECRET_KEY` is generated automatically by the Render blueprint.

## Database note

The app uses MySQL. A local database host such as `localhost` will not work on Render. Use a MySQL database that is reachable from Render, then run `database.sql` on that database before opening the app.

Render's managed PostgreSQL database is not compatible with this app unless the SQL queries and schema are migrated from MySQL to PostgreSQL.
