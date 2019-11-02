# Unturned-Docker
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjulien040%2Funturned-docker.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjulien040%2Funturned-docker?ref=badge_shield)

This repository contains scripts for installing 64bit Unturned Linux with .NET 4.6.1 (optionally using Docker). It also uses Unturned .NET 4.6.1 versions.

# Getting Started
Images are hosted at `imperialplugins/unturned`. You can visit the [Docker Hub Repository](https://hub.docker.com/r/imperialplugins/unturned) for more information.

Example command to host a simple RocketMod 4 Unturned server:

`docker run -it -e STEAM_USERNAME=myusername -e STEAM_PASSWORD=mypassword -p 27015:27015 -p 27016:27016 -e SERVER_TYPE=rm4 --restart unless-stopped --name myserverinstance imperialplugins/unturned`

This will create a docker container that will listen on 27015 for Unturned and 27016 for Steam queries with RocketMod 4. It will automatically restart should the server shut down or crash.

Also, on each container restart the server will automatically update.

You will not be able to input anything to the console (because Unity handles stdin/stdout in a weird way).

## Server Type
The following are supported for the SERVER_TYPE environment variable:
* rm4 (installs RocketMod 4 module)
* rm5 (installs RocketMod 5 module)
* anything else or empty (does not install any modules)

## Building
To build, use `docker build . -t unturned`.

After building, you can start your server like the command in "Getting Started", but you will have to replace "imperialplugins/unturned" with just "unturned".

## Non-Docker Usage
First install required dependencies:
```sh
$ sudo apt-get install -y unzip tar curl coreutils lib32gcc1 libgdiplus git
```

Then install .NET Core SDK following [this guide](https://dotnet.microsoft.com/download/linux-package-manager/ubuntu18-04/sdk-current).

After installing the .NET Core SDK, set GAME_INSTALL_DIR, GAME_ID (304930 for Unturned), STEAM_USERNAME and STEAM_PASSWORD, SERVER_TYPE environment variables:

```sh
$ export GAME_INSTALL_DIR=/path/to/Unturned
$ export GAME_ID=304930
$ export SERVER_TYPE=rm4
$ export STEAM_USERNAME=myUsername
$ export STEAM_PASSWORD=myPassword
```

You do not have to install steacmd, this script will do it for you.

Finally, run `init.sh` to install / update your server. It will automatically start the server afterwards:
```sh
$ ./init.sh
```


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjulien040%2Funturned-docker.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjulien040%2Funturned-docker?ref=badge_large)