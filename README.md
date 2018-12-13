```
A tool for deploying an application to a remote host in a Docker
container, according to a configuration provided in a `ddeployrc` file
(optionally prefixed with a dot `.`).

Options:

-f - Foreground mode: do not pass `--detach` to `docker run`.
-r - Ref to check out and deploy, `master` by default.
-q - Quit without attempting to log into the deploy host. This is a guard
     flag for internal use against looping indefinitely.
```
