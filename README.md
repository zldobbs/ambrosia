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

### Migrations

Apply any new migrations to the server using the [apply_migrations.sh script](./ambrosia-server/db/apply_migrations.sh).

```sh
docker compose run backend /ambrosia-server/db/apply_migrations.sh
```

> NOTE: Command may not work if ran from Git Bash. Try CMD/PowerShell if errors occur.

### Seeding Database

Apply initial data to the database:

```sh
docker compose run backend psql -U postgres -p postgres -f /ambrosia-server/db/sql/seed.sql
```

Adjust as necessary based on user credentials.

> NOTE: Command may not work if ran from Git Bash. Try CMD/PowerShell if errors occur.
