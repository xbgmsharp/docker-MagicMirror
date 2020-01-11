[![Docker Pulls](https://img.shields.io/docker/pulls/xbgmsharp/docker-magicmirror.svg)](https://hub.docker.com/r/xbgmsharp/docker-magicmirror/)[![Build Status](https://travis-ci.com/xbgmsharp/docker-MagicMirror.svg?branch=master)](https://travis-ci.com/xbgmsharp/docker-MagicMirror)

# Docker MagicMirror²

This multi architecture Alpine Linux based Docker image allows you to run [MagicMirror²: The open source modular smart mirror platform.](https://github.com/MichMich/MagicMirror)

**MagicMirror²** is an open source modular smart mirror platform. With a growing list of installable modules, the **MagicMirror²** allows you to convert your hallway or bathroom mirror into your personal assistant.

# Why Docker?
In some cases, you want to start the application without an actual app window. In this case, you can start MagicMirror² in server only mode by manually running `node serveronly` or using Docker. This will start the server, after which you can open the application in your browser of choice.

# Supported tags:

- `latest` - Latest MagicMirror² server ([Dockerfile](https://github.com/xbgmsharp/docker-MagicMirror/blob/master/Dockerfile))

> The docker images are updated daily by a cron job from ([Travis CI](https://travis-ci.com/xbgmsharp/docker-MagicMirror)).

> This docker image is based on the popular Alpine Linux project, available in the alpine official image. Alpine Linux is much smaller than most distribution base images (~5MB), and thus leads to much slimmer images in general (less than 400MB).

# Supported architectures: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))
`amd64`, `arm32v6`, `arm32v7`, `arm64v8`, `i386`

| **Docker** | **uname -m architecture** | **Annotate flage** | **Boards** |
| --- | --- | --- | --- |
| amd64 | x86_64 | (none) |
| arm32v6 | armhf | Raspberry Pis | --os linux --arch arm |
| arm64v8 | aarch64 | A53, H3, H5 ARMs |--os linux --arch arm64 --variant armv8 |

If you compiled for other architectures and know other combinations, let me know!

> The docker image tag `latest` is available for all supported architectures.

# Run MagicMirror² in server only mode
After a successful [Docker installation](https://docs.docker.com/engine/installation/) you just need to execute the following command in the shell:

```bash
docker pull xbgmsharp/docker-magicmirror
docker run  -d \
	--publish 80:8080 \
	--restart always \
	--volume ~/magic_mirror/config:/opt/magic_mirror/config \
	--volume ~/magic_mirror/modules:/opt/magic_mirror/modules \
	--name magic_mirror \
	xbgmsharp/docker-magicmirror
```

# Volumes
| **Volume** | **Description** |
| --- | --- |
| `/opt/magic_mirror/config` | Mount this folder to insert your own config into the docker container. |
| `/opt/magic_mirror/modules` | Mount this folder to add your own custom modules into the docker container. |
| `/opt/magic_mirror/css` | Mount this directory to add your own custom css into the docker container. <br><br> **Important:** You need to create the file before you run the container. Otherwise Docker will create a `custom.css` folder. |

# Config
You need to configure your MagicMirror² config to listen on any interface and allow every ip address.

```javascript
var config = {
    address: "0.0.0.0",
    port: 8080,
    ipWhitelist: []
}

if (typeof module !== "undefined") { module.exports = config; }
```

# Contribution
I'm happy to accept Pull Requests! Please note that this project is released with a [Contributor Code of Conduct](https://github.com/xbgmsharp/docker-MagicMirror/blob/master/CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

# License
[MIT](https://github.com/xbgmsharp/docker-MagicMirror/blob/master/LICENSE) ❤️
