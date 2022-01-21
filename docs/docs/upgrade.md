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

## Heroku

If you deployed listmonk on Heroku using the *Deploy to Heroku* button, then these steps are necessary to upgrade your installation as Heroku does not provide simpler means to upgrade. 

- Fork the [listmonk-heroku repository](https://github.com/knadh/listmonk-heroku-deploy) to your GitHub account.
- Login to Heroku, and go to the "Deploy" tab under the listmonk app.
- Select "GitHub" in the "Deployment method" section.
- In the "Connect to GitHub" section, search for your forked listmonk-Heroku repo. Connect to it.
[![image](https://user-images.githubusercontent.com/55474996/135002032-0a7dce9c-548f-4edd-8db2-575708b490b4.png)](https://user-images.githubusercontent.com/55474996/135002032-0a7dce9c-548f-4edd-8db2-575708b490b4.png)

- In the "Manual deploy" section, click on the "Deploy Branch" button. For all future upgrades, simply use this option once.
[![image](https://user-images.githubusercontent.com/547147/135745846-df37cd8f-a0b7-4dc8-bc15-5d350b1afe78.png)](https://user-images.githubusercontent.com/547147/135745846-df37cd8f-a0b7-4dc8-bc15-5d350b1afe78.png)
