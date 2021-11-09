# Meltano ALTA

## Install meltano

You can either install meltano using python or run it directly using docker. You can find how to install [here](https://meltano.com/docs/installation.html#local-installation).

When installed manually, you can directly run the command like this:

```bash
meltano COMMAND
```

When using docker, you must specify the directory that meltano project used inside docker and optionally change the container noetwork to run as host, so it can access any other resource that run on the host machine. The command for docker will be like this:

```bash
docker run -v $(pwd):/projects -w /projects --network host meltano/meltano COMMAND
```

## How to run EL (Extractor and Loader) process

### Install plugin

```bash
meltano install
```

### Update github configuration

You can get github access token by following [this](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

This configuration already applied to `alterraacademy/skcbd`, `alterraacademy/axiapp`, `alterraacademy/rfitness-backend`, and `alterraacademy/rfitness-mobile` repositories. You can modify manually by editing `meltano.yml`.

```bash
meltano config tap-github set access_token YOUR_ACCESS_TOKEN
```

### Update postgresql configuration

Run postgresql and create new database and user in postgresql. For other configuration, you can visit [here](https://meltano.com/plugins/loaders/postgres.html#next-steps).

```bash
meltano config target-postgres set postgres_host YOUR_POSTGRESQL_HOST
meltano config target-postgres set postgres_port YOUR_POSTGRESQL_PORT
meltano config target-postgres set postgres_database YOUR_POSTGRESQL_DB_NAME
meltano config target-postgres set postgres_username YOUR_POSTGRESQL_USERNAME
meltano config target-postgres set postgres_password YOUR_POSTGRESQL_PASSWORD
```

### Run EL (Extractor and Loader) process

```bash
meltano elt tap-github target-postgres --job_id=github-to-postgres
```

## Verify the process

If you got `Extract & load complete!` in terminal then the process is complete and you can check the data directly to the database.