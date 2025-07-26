# Template of [golang-migrate](https://github.com/golang-migrate/migrate)

The following command sample:

- database url for golang-migrate
  ```shell
  $  migrate -database "mysql://root:root@tcp(127.0.0.1:3306)/test" up 
  ```
- create migration file command
  ```shell
  $ migrate create -ext sql -dir migrations -tz Asia/Tokyo create_test
  ```

## Usage of golang-migrate

```shell
$ migrate --help
Usage: migrate OPTIONS COMMAND [arg...]
       migrate [ -version | -help ]

Options:
  -source          Location of the migrations (driver://url)
  -path            Shorthand for -source=file://path
  -database        Run migrations against this database (driver://url)
  -prefetch N      Number of migrations to load in advance before executing (default 10)
  -lock-timeout N  Allow N seconds to acquire database lock (default 15)
  -verbose         Print verbose logging
  -version         Print version
  -help            Print usage

Commands:
  create [-ext E] [-dir D] [-seq] [-digits N] [-format] [-tz] NAME
           Create a set of timestamped up/down migrations titled NAME, in directory D with extension E.
           Use -seq option to generate sequential up/down migrations with N digits.
           Use -format option to specify a Go time format string. Note: migrations with the same time cause "duplicate migration version" error.
           Use -tz option to specify the timezone that will be used when generating non-sequential migrations (defaults: UTC).

  goto V       Migrate to version V
  up [N]       Apply all or N up migrations
  down [N] [-all]    Apply all or N down migrations
        Use -all to apply all down migrations
  drop [-f]    Drop everything inside database
        Use -f to bypass confirmation
  force V      Set version V but don't run migration (ignores dirty state)
  version      Print current migration version

Source drivers: file, github, github-ee
Database drivers: stub, mysql
```

## Usage of this repository

### Requirements

- Install [Docker](https://docs.docker.com/engine/install/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)
- Install [Task](https://taskfile.dev/installation/)

### Available Commands

```shell
$ task               
task: [default] task -l --sort none
task: Available tasks for this project:
* default:              List all available tasks
* mysql:version:        Run migrate version to mysql
* mysql:create:         Run migrate create to mysql
* mysql:up:             Run migrate up to mysql
* mysql:down:           Run migrate down N to mysql
* mysql:down:all:       Run migrate down to mysql
* mysql:connect:        Connect to mysql
* compose:build:        Docker compose build
* compose:up:           Docker compose up
* compose:down:         Docker compose down
```

### MySQL Sample

```shell
$ task compose:build
task: [compose:build] docker compose build migrate
...

$ task compose:up
task: [compose:up] docker compose up -d mysql
...

$ task mysql:up
task: [mysql:run] docker compose run --rm migrate -path migrations -database "mysql://root:root@tcp(mysql:3306)/test" up
20250726085241/u create_test (16.055083ms)
20250726122605/u insert_test (23.12025ms)

$ task mysql:connect

mysql> SHOW TABLES;
+-------------------+
| Tables_in_test    |
+-------------------+
| schema_migrations |
| test              |
+-------------------+
```

### PostgreSQL Sample

TODO: Add PostgreSQL sample
