# **compose up**

****
Usage: hyper compose up [OPTIONS] [SERVICE...]
Builds, (re)creates, starts, and attaches to containers for a service.
Unless they are already running, this command also starts any linked services.
The `jcloud compose up` command aggregates the output of each container. When
the command exits, all containers are stopped. Running `jcloud compose up -d`
starts the containers in the background and leaves them running.
If there are existing containers for a service, and the service's configuration
or image was changed after the container's creation, `jcloud compose up` picks
up the changes by stopping and recreating the containers (preserving mounted
volumes). To prevent Compose from picking up changes, use the `--no-recreate`
flag.
If you want to force Compose to stop and recreate all containers, use the
`--force-recreate` flag.
-d, --detach Detached mode: Run containers in the background,
print new container names.
Incompatible with --abort-on-container-exit.
-f, --file=hyper-compose.yml Specify an alternate compose file
--force-recreate Recreate containers even if their configuration
and image haven't changed.
Incompatible with --no-recreate.
--help Print usage
--no-recreate If containers already exist, don't recreate them.
Incompatible with --force-recreate.
-p, --project-name Specify an alternate project name

注意：默认情况下，项目名称是当前目录的名称，项目名称应符合正则表达式 ^[a-zA-Z_][a-zA-Z0-9_]/*$ （首字母必须是 a-zA-Z_，剩余其他字母必须是 a-zA-Z0-9_）

。