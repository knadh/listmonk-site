# Upgrade

Some versions may require changes to the database. These changes or database "migrations" are applied automatically and safely, but, it is recommended to take a backup of the Postgres database before running the `--upgrade` option, especially if you have made customizations to the database tables.

## Binary
- Download the [latest release](https://github.com/knadh/listmonk/releases) and extract the listmonk binary.
- `./listmonk --upgrade` to upgrade an existing DB. Upgrades are idempotent and running them multiple times have no side effects.
- Run `./listmonk` and visit `http://localhost:9000`.

## Docker

- `docker-compose pull` to pull the latest version from DockerHub.
- `docker-compose run --rm app ./listmonk --upgrade` to upgrade an existing DB.
- Run `docker-compose up app db` and visit `http://localhost:9000`.
