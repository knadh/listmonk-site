# Configuration

### TOML Configuration file
One or more TOML files can be read by passing `--config config.toml` multiple times. Apart from a few low level configuration variables and the database configuration, all other settings can be managed from the `Settings` dashboard on the admin UI.

To generate a new sample configuration file, run `--listmonk --new-config`

### Environment variables
Variables in config.toml can also be provided as environment variables prefixed by `LISTMONK_` with periods replaced by `__` (double underscore). Example:

| **Environment variable**       | Example value  |
|--------------------------------|----------------|
| `LISTMONK_app__address`        | "0.0.0.0:9000" |
| `LISTMONK_app__admin_username` | listmonk       |
| `LISTMONK_app__admin_password` | listmonk       |
| `LISTMONK_db__db`              | db             |
| `LISTMONK_db__user`            | listmonk       |
| `LISTMONK_db__password`        | listmonk       |
| `LISTMONK_db__database`        | listmonk       |
| `LISTMONK_db__ssl_mode`        | disable        |


### Customizing system templates
[Read this](../templating/#system-templates)


### HTTP routes
When configuring auth proxies in front of listmonk, these end user facing URIs should be open to the internet. All other paths can be secured behind the proxy.

| Methods	        | Route              |
| ------------------|--------------------|
| `GET, POST`       | `/subscription/*`  |
| `GET, `           | `/link/*`          |
| `GET`             | `/campaign/*`      |
| `GET`             | `/public/*`        |
