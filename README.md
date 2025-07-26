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

## MySQL Sample

```shell
$ task compose:build

$ task compose:up

$ task mysql:up

$ task mysql:connect

mysql> SHOW TABLES;
+-------------------+
| Tables_in_test    |
+-------------------+
| schema_migrations |
| test              |
+-------------------+
```

## PostgreSQL Sample

TODO: Add PostgreSQL sample
