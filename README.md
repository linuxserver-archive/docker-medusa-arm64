[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/pymedusa/Medusa
[hub]: https://hub.docker.com/r/lsioarmhf/medusa-aarch64/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/medusa-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/medusa-aarch64.svg)](https://microbadger.com/images/lsioarmhf/medusa-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/medusa-aarch64.svg)](http://microbadger.com/images/lsioarmhf/medusa-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/medusa-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/medusa-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-medusa)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-medusa/)

[Medusa][appurl], automatic Video Library Manager for TV Shows. It watches for new episodes of your favorite shows, and when they are posted it does its magic.

[![medusa](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/medusa-readme.png)][appurl]


## Usage

```
docker create \
  --name=medusa \
-v <path to config>:/config \
-v <path to downloads>:/downloads \
-v <path to tv-shows>:/tv \
-e PGID=<gid> -e PUID=<uid>  \
-e TZ=<timezone> \
-p 8081:8081 \
  lsioarmhf/medusa-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 8081` - the port(s)
* `-v /config` - where medusa should store config files.
* `-v /downloads` - your downloads folder
* `-v /tv` - your tv-shows folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London


It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it medusa /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARM64 VERSION`

Web interface is at `<your ip>:8081` , set paths for downloads, tv-shows to match docker mappings via the webui.


## Info

* Shell access whilst the container is running: `docker exec -it medusa /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f medusa`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' medusa`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/medusa-aarch64`

## Versions

+ **10.10.17:** Use repo version of mediainfo to shorten build time.
+ **05.08.17:** Internal git pull instead of at runtime.
+ **20.05.17:** Rebase to alpine 3.6.
+ **01.01.17:** Initial Release.
