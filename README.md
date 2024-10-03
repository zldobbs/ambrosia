# ambrosia

Monorepo collection of all ambrosia services

- [Application](./ambrosia-app/)
- [Web Server](./ambrosia-server/)

## Launching

`docker compose up --build` will (re)build the backend and launch the database.

To additionally build and launch the frontend, use `docker compose --profile frontend up --build`.

> NOTE: The frontend container is configured to run via the "web" bundler by default.
> This bundler is also not configured for fast-refresh (at least on Windows).
> Development and other emulators should be manually targetted separately for the frontend (e.g. `yarn ios`).

The frontend container uses an anonymous volume to store the node_modules directory.
If the npm dependencies change, the volume will need to either be rebuilt or a manual installation within a running container will be required.

This is all that is necessary to get the entire application up and running.

> NOTE: The first launch of this server will require manually running SQL scripts to initialize the database.
> Refer to the [database](#database) section for more information.

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

## Issues

- See all TODOs

### Android

- Back button doesn't work
- Header logo doesn't display
- VirtualizedLists should never be nested inside plain ScrollViews with the same orientation because it can break windowing and other functionality - use another Virtualized-backed container instead.
