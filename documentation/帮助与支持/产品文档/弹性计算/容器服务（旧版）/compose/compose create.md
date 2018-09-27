# **compose create**

Usage:jcloud compose create [OPTIONS] [SERVICE...]
Creates containers for a service.
-f, --file=docker-compose.yml Specify an alternate compose file
--force-recreate Recreate containers even if their configuration
and image haven't changed.
Incompatible with --no-recreate.
--help Print usage
--no-recreate If containers already exist, don't recreate them.
Incompatible with --force-recreate.
-p, --project-name Specify an alternate project name

注意：默认情况下，项目名称是当前目录的名称。项目名称应为

^[a-zA-Z_][a-zA-Z0-9_]/*$
。