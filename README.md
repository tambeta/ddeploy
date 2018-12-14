# ddeploy

A tool for deploying an application from a Git repository to a remote host in a
Docker container, according to a configuration provided in a `ddeployrc` file
(optionally prefixed with a dot `.`). Run `ddeploy` in a directory containing
the configuration file to make the magic happen.

In addition to the configuration file, `Dockerfile` and the runner script
defined by `CONTAINER_RUNNER` (if any) are required to be present in the same
directory.

## Configuration variables

* `DEPLOY_HOST` - Remote host name.
* `DEPLOY_DIR` - Directory wherein the project has been cloned on the remote
  host.
* `IMAGE_NAME` - Resulting Docker image name.
* `CONTAINER_NAME` - Docker container name.
* `CONTAINER_PORT_MAP` - _Optional_ Port mapping between the host and Docker
  container.  This is expanded to `-p 127.0.0.1:$CONTAINER_PORT_MAP` for
  Docker.
* `CONTAINER_DIR` - _Optional_ Installation directory within the container.
* `CONTAINER_RUNNER` - _Optional_ Name of a script copied to the container and
  used as the startup process.
* `CONTAINER_CMD` - _Optional_ Command used to launch the startup process. Do
  not use with `CONTAINER_RUNNER`.

## Command-line options:

* `-f` - Foreground mode: do not pass `--detach` to `docker run`.
* `-r` - Ref to check out and deploy.
* `-q` - Quit without attempting to log into the deploy host. This is a guard
  flag for internal use against looping indefinitely.
