# Developer setup
The app has two distinct components, the Go backend and the VueJS frontend. In the dev environment, both are run independently.

### First time setup
`git clone https://github.com/knadh/listmonk.git`. The project uses go.mod, so it's best to clone it outside the Go src path.

1. Copy `config.toml.sample` as `config.toml` and add your config.
2. `make deps` (to install Go dependencies for the backend and the JS dependencies for the frontend).
3. `make build` to build the listmonk binary. Once the binary is built, run `./listmonk --install` to run the DB setup.

> [mailhog](https://github.com/mailhog/MailHog) is an excellent standalone mock SMTP server (with a UI) for testing and dev.

### Running the dev environment
1. Run `make run` to start the listmonk Go server.
2. Run `make run-frontend` to start the Vue frontend in dev mode using yarn. Refer to the [frontend README](https://github.com/knadh/listmonk/blob/master/frontend/README.md) for an overview on how the frontend is structured.
3. Setup the Nginx dev proxy as described below and visit `http://localhost:9001`.


# Dev proxy

### Setup an Nginx proxy endpoint
In the dev mode, although the frontend and backend are running as two independent servers, the requests should go via the same endpoint for the app to work. In production, this is not the case as the frontend is bundled into the server.

Here's a sample Nginx config that achieves this. Once this is up and running, visit `http://localhost:9001` to access the frontend running in development mode where Javascript updates are pushed live.

```
# listmonk
server {
    listen 9001;

    # Proxy all /api/* requests to the Go backend.
    location /api {
        proxy_pass http://localhost:9000;
    }

    # Proxy everything else to the Vue frontend running on the Yarn server.
    location / {
        proxy_pass http://localhost:8080;
    }
}

```

# Production build

Run `make dist` to build the Go binary, build the Javascript frontend, and embed the static assets producing a single self-contained binary, `listmonk`
