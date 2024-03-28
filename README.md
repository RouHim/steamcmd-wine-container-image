# steamcmd-wine-container-image

This base container image provides everything you need to run a windows based dedicated server which is to be installed
via SteamCMD. It's based on the latest packages provided by `ubuntu:devel` and is built weekly.

![Docker Image Version](https://img.shields.io/docker/v/_/ubuntu?label=ubuntu)

![Ubuntu Package Version (for series)](https://img.shields.io/ubuntu/v/wine/devel?label=wine&link=https%3A%2F%2Fpackages.ubuntu.com%2Fsearch%3Fkeywords%3Dwine%26searchon%3Dnames%26suite%3Dall%26section%3Dall)

## How to use

```Dockerfile
FROM docker.io/rouhim/steamcmd-wine:latest
USER $USER

# Set the following environment variables: STEAM_APP_ID, STARTUP_COMMAND

# STEAM_APP_ID: The Steam App ID of the game server to install
ENV STEAM_APP_ID "xyz"

# STARTUP_COMMAND:  The command to run to start the server, 
#                   the current working directory is the server directory ($SERVER_DIR)
ENV STARTUP_COMMAND "wine server.exe -configpath "$SERVER_CONFIG_DIR""

# Optional pre.sh script to run before the server starts
COPY pre.sh $USER_HOME/pre.sh

# Optional post.sh script to run after the server starts
COPY post.sh $USER_HOME/post.sh
```

If you want to install additional packages via apt,
make sure to become `USER root` before executing apt commands.
Obviously, you should also switch back to `USER $USER` after installing the packages.

## Environment Variables

The following environment variables are available in the base image:

| Variable            | Default Value                     | Description                                                   |
|---------------------|-----------------------------------|---------------------------------------------------------------|
| `USER`              | `ubuntu`                          | The user to run the server as                                 |
| `GROUP`             | `ubuntu`                          | The group to run the server as                                |
| `USER_HOME`         | `/home/$USER`                     | The home directory of the user                                |
| `STEAMCMD`          | `$USER_HOME/steamcmd/steamcmd.sh` | The path to the steamcmd executable                           |
| `SERVER_DIR`        | `/data`                           | The directory where the server files are stored               |
| `SERVER_CONFIG_DIR` | `/config`                         | The directory where the server configuration files are stored |
