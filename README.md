# ambrosia

Monorepo collection of all ambrosia services

- [Application](./ambrosia-app/)
- [Web Server](./ambrosia-server/)

## Launching

`docker compose up --build` will (re)build the backend and launch the database.

This is all that is necessary to get the backend completely up and running.

> NOTE: The first launch of this server will require manually running SQL scripts to initialize the database.
> Refer to the [database](#database) section for more information.

> TODO: Need to add the frontend to compose.yml as well.

## Database

Using [PostgreSQL](https://www.postgresql.org).

If launched via Docker Compose, follow these steps to finish first-time database setup:

- Connect to running container with a bash terminal: `docker exec -it ambrosia-database-1 bash`
- Run each of the sql scripts to initialize and seed the database:
  - `cd /var/lib/ambrosia/db/sql`
  - `psql -U postgres -f initialize.sql`
  - `psql -U postgres -f seed.sql`

> NOTE: The sql scripts should only need to be ran once.
> Should investigate automating these as part of docker compose.
