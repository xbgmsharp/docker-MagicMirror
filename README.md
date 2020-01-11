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

# Parameters
Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 8080` | require for magicmirror to function |
| `-e PUID=1000` | for UserID (optional) |
| `-e PGID=1000` | for GroupID (optional) |
| `-e TZ=Europe/Paris` | TimeZone (optional) |
| `-v /opt/magic_mirror/config` | Mount this folder to insert your own config into the docker container. |
| `-v /opt/magic_mirror/modules` | Mount this folder to add your own custom modules into the docker container. |
| `-v /opt/magic_mirror/css` | Mount this directory to add your own custom css into the docker container. <br><br> **Important:** You need to create the file before you run the container. Otherwise Docker will create a `custom.css` folder. |

# Config
You need to configure your MagicMirror² config to listen on all interface and allow every ip address.

```javascript
var config = {
    address: "0.0.0.0",
    port: 8080,
    ipWhitelist: []
}

if (typeof module !== "undefined") { module.exports = config; }
```

# Updating Info

Most of our images are static, versioned, and require an image update and container recreation to update the app inside. 

Below are the instructions for updating containers:

## Via Docker Run/Create
* Update the image: `docker pull xbgmsharp/docker-magicmirror`
* Stop the running container: `docker stop magicmirror`
* Delete the container: `docker rm magicmirror`
* Recreate a new container with the same docker create parameters as instructed above (if mapped correctly to a host folder, your `config` and `modules` folder with settings will be preserved)
* Start the new container: `docker start magicmirror`
* You can also remove the old dangling images: `docker image prune`

```bash
docker pull xbgmsharp/docker-magicmirror
docker stop magic_mirror
docker rm magic_mirror
docker create \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  --restart unless-stopped \
  --publish 8181:8080 \
  --volume ~/magic_mirror/config:/opt/magic_mirror/config \
  --volume ~/magic_mirror/modules:/opt/magic_mirror/modules \
  --volume ~/magic_mirror/css:/opt/magic_mirror/css \
  --name magic_mirror xbgmsharp/docker-magicmirror
docker start magic_mirror
```

# Contribution
I'm happy to accept Pull Requests! Please note that this project is released with a [Contributor Code of Conduct](https://github.com/xbgmsharp/docker-MagicMirror/blob/master/CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

# License
[MIT](https://github.com/xbgmsharp/docker-MagicMirror/blob/master/LICENSE) ❤️
