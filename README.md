# ddeploy

A tool for deploying an application from a Git repository to a remote host using
[Docker Compose](https://docs.docker.com/compose/), according to a configuration
provided in a `docker-compose.yml` file.  Run `ddeploy` in a directory
containing the configuration file to make the magic happen.

## Configuration

`ddeploy` configuration mostly happens via `docker-compose.yml` containing a
special [extension
field](https://docs.docker.com/compose/compose-file/#extension-fields)
`x-ddeploy-conf` (in addition to standard sections such as `services`).
Configuration subkeys:

* `deploy_host` - *String* Deploy target host name.
* `deploy_workdir` - *String* A directory for deployment infrastructure files,
  will be created if nonexistent. This may be a transient directory.
* `services` - *Mapping* Service IDs linked to a mapping, containing the
  following keys:
  * `deploy_dir` - *String* Service directory on the deploy host. This is
    expected to be present and be a Git working directory. On deploy, the
    configured ref will be fetched and checked out. Generally this directory is
    also expected to be mounted onto the container, but this is up to standard
    Docker Compose configuration.
  * `ref` - *String* The Git ref to be fetched and checked out on deploy. Making
    this configurable on the command line is TODO.

  The values in `services` will also be made available for later use via the
  [env file](https://docs.docker.com/compose/env-file/). Variable names are
  constructed by prefixing the configuration key with the service ID. E.g. the
  key

  ```
  services:
    webapp:
      deploy_dir: "/opt/docker/webapp"
  ```

  will become available as `${webapp_deploy_dir}`.

See `docker-compose.example.yml` for an example.

## Command-line options:

* `-f` - Foreground mode: do not pass `--detach` to `docker compose up`.

