![Metabase](assets/logo.png)

# Deploy N8N on Scalingo

## One-click deployment

Run your own Metabase instance with one click.

[![Deploy](https://cdn.scalingo.com/deploy/button.svg)](https://my.scalingo.com/deploy?source=https://github.com/Scalingo/n8n-scalingo#master)

## Steps to deploy N8N manually

1. Create an application on Scalingo

```
scalingo create my-n8n
```

2. Add a PostgreSQL for the internal usage of n8n

```
scalingo -a my-n8n addons-add postgresql postgresql-starter-512
```

3. Configure n8n to perform store its internal data in PostgreSQL

```
scalingo -a my-n8n env-set 'DB_POSTGRESDB_DATABASE=xxx'
scalingo -a my-n8n env-set 'DB_POSTGRESDB_HOST=xxx.postgresql.dbs.scalingo.com'
scalingo -a my-n8n env-set 'DB_POSTGRESDB_PASSWORD=xxx'
scalingo -a my-n8n env-set 'DB_POSTGRESDB_PORT=xxx'
scalingo -a my-n8n env-set 'DB_POSTGRESDB_USER=xxx'
scalingo -a my-n8n env-set 'DB_TYPE=postgresdb'
```

4. Add some needed configuration for N8N

Tell N8N to listen on the port provided by Scalingo.
```
scalingo -a my-n8n env-set 'N8N_PORT=$PORT'
```

Define an encryption key used to encrypt credentials before storing them in the database.
```
scalingo -a my-n8n env-set 'N8N_ENCRYPTION_KEY=<A RANDOM STRING>'
```

4. Clone this repository

```
git clone https://github.com/Scalingo/n8n-scalingo
```

5. Configure GIT

```
cd n8n-scalingo
scalingo -a my-n8n git-setup
```

6. Deploy the application

```
git push scalingo master
```

