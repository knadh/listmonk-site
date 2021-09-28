# Upgrade

## Binary
- Download the [latest release](https://github.com/knadh/listmonk/releases) and extract the listmonk binary.
- `./listmonk --upgrade` to upgrade an existing DB. Upgrades are idempotent and running them multiple times have no side effects.
- Run `./listmonk` and visit `http://localhost:9000`.

## Docker

- `docker-compose pull` to pull the latest version from DockerHub.
- `docker-compose run --rm app ./listmonk --upgrade` to upgrade an existing DB.
- Run `docker-compose up app db` and visit `http://localhost:9000`.

## Heroku Deployment

- Fork the [Listmonk-Heroku repository](https://github.com/knadh/listmonk-heroku) to your GitHub account
- In Heroku, go to your app and click on the "Deploy" tab.
- In the "Deployment method" section of this page, select GitHub.
- In the "Connect to GitHub" section, search for your forked Listmonk-Heroku repo. Connect to it.
![image](https://user-images.githubusercontent.com/55474996/135002032-0a7dce9c-548f-4edd-8db2-575708b490b4.png)

- In the "Automatic deploys" page, select "Enable Automatic Deploys"
![image](https://user-images.githubusercontent.com/55474996/135002226-bded2405-1bd4-40e4-834b-5f5def07215a.png)

- Head back to your forked Listmonk-Heroku repository on your GitHub account. Edit one of your files and make a simple modification (example, add some random characters to the readme.md) and commit the change directly to the main branch.
- This will trigger the Heroku deployment. Your app should now be updated to the latest release of Listmonk.
