# steamcmd-wine-container-image

This base container image provides steamcmd and the latest wine as a secure container image

## How to use as a base image

```Dockerfile
FROM docker.io/rouhim/steamcmd-wine:latest

# Overwrite the following environment variables
# STEAM_APP_ID: The Steam App ID of the game server to install
ENV STEAM_APP_ID "xyz"
# STARTUP_COMMAND:  The command to run to start the server, 
#                   the current working directory is the server directory ($SERVER_DIR)
ENV STARTUP_COMMAND "wine server.exe -configpath "$SERVER_CONFIG_DIR""

# Optional pre.sh script to run before the server starts
# Ensure that the script is executable
COPY pre.sh /pre.sh
RUN chmod +x /pre.sh

# Optional post.sh script to run after the server starts
# Ensure that the script is executable
COPY post.sh /post.sh
RUN chmod +x /post.sh
```

## Environment Variables

The following environment variables are available:

* `USER` `"ubuntu"`
* `GROUP` `"ubuntu"`
* `USER_HOME` `"/home/$USER"`
* `STEAMCMD` `"$USER_HOME/steamcmd/steamcmd.sh"`
* `SERVER_DIR` `"/data"`
* `SERVER_CONFIG_DIR` `"/config"`