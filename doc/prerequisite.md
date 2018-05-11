# prerequisite

## install Virtualbox

- [Download](https://www.virtualbox.org/wiki/Downloads)
- follow instruction of page

## install Virtualbox extension pack

- [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- follow instruction of page

## install docker

- [download CE version](https://store.docker.com/editions/community/docker-ce-desktop-mac)
- follow instruction of page

## install docker-machine

- [instruction](https://docs.docker.com/machine/install-machine/)
- follow instruction of page

- run on bash

```bash
base=https://github.com/docker/machine/releases/download/v0.14.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/usr/local/bin/docker-machine &&
  chmod +x /usr/local/bin/docker-machine
```

## check all works correctly


### VirtualBox check (weak check)

- try to start VirtualBox GUI
- and check VBoxMange on cli

```bash
> VBoxManage --version
```

### docker check

```bash
> docker run hello-world
```

- you should see output
- container and images should listed

```bash
> docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
48edea0da7aa        hello-world         "/hello"            13 hours ago        Exited (0) 13 hours ago
```

```bash
> docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              e38bc07ac18e        4 weeks ago         1.85kB
```

- [detail instruction see here](https://hub.docker.com/_/hello-world/)


## docker-machine check

- check the list of machine <- should empty on start

```bash
> docker-machine ls
NAME        ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
```