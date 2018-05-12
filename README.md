<!-- markdownlint-disable MD041 -->
> I would greatly appreciate it if you kindly give me some feedback if you found an error
> [Send feedback to me](mailto:feedback@mathias-stadler.de)
<!-- markdownlint-enable MD041 -->

# docker-machine-roundup-apple

- thought and things about docker-machine on apple MacOS High Sierra

## [details](https://docs.docker.com/machine/get-started/#start-local-machines-on-startup)

## [prerequisite](doc/prerequisite.md)

## create docker-machine with default value on virtualbox

```bash
> docker-machine create <name of machine>
> docker-machine create vbox-test
```

- should use standard installed virtualbox
- used [standard setting]((https://docs.docker.com/machine/drivers/virtualbox/#options)) of docker-machine

## create docker-machine force on virtualbox

```bash
> docker-machine create --driver=virtualbox virtualbox-test
```

- [details for docker-machine virtualbox driver](https://docs.docker.com/machine/drivers/virtualbox/)
- [defaults for docker-machine of virtualbox](https://docs.docker.com/machine/drivers/virtualbox/#options)

## create a stronger docker-machine

```bash
docker-machine create --driver  virtualbox --virtualbox-cpu-count=4 --virtualbox-memory=4096 --virtualbox-disk-size=10000  box-strong
```

## list all docker machine

```bash
> docker-machine ls
```

## show/set/unset env for (local) docker-cli

- show env variable for docker-machine

```bash
> docker-machine env <name of machine>
> docker-machine env vbox-test
```

- set env variable for docker-machine

```bash
> eval $(docker-machine env <name of machine>)
> eval $(docker-machine env vbox-test)
```

- unset env variable for docker-machine

```bash
> eval $(docker-machine env -u)
```

- after this command should you reach your local docker daemon

- for another docker machine load this present env setting

```bash
> eval $(docker-machine env another-docker-machine)
```

## display which machine is active under control from your local docker cli

```bash
> docker-machine active
```

- very useful for script
- e.g. see the ssh kez login script

## login in docker-machine

```bash
> docker-machine ssh <name of machine>
> docker-machine ssh vbox-test
```

or

- login via ssh direct

```bash
> ssh docker@$(docker-machine ip <name of machine>)
> ssh docker@$(docker-machine ip vbox-test)
```

- the default password is **tcuser**

or

- login via ssh with the kez

- all credits goes to [robert](https://stackoverflow.com/questions/30330442/how-to-ssh-into-docker-machine-virtualbox-instance)

```bash
script_name="docker-machine-kez-virtualbox-login.sh"
cat > ./${script_name} << 'EOL'
#!/bin/bash
if !  docker-machine active; then
 echo "No active machine";
 echo "Set first with docker-machine env <name of machine>" ;
exit 1
fi
docker_machine_name=$(docker-machine active)
docker_ssh_user=$(docker-machine inspect $docker_machine_name --format={{.Driver.SSHUser}})
docker_ssh_key=$(docker-machine inspect $docker_machine_name --format={{.Driver.SSHKeyPath}})
docker_ssh_port=$(docker-machine inspect $docker_machine_name --format={{.Driver.SSHPort}})
ssh -i $docker_ssh_key -p $docker_ssh_port $docker_ssh_user@localhost
EOL
chmod +x ./${script_name}
```

@TODO Add accept kez without extra confirm

## stop docker-machine

```bash
> docker-machine stop <name of vm>
> docker-machine start vbox-test
```

## start docker-machine

```bash
> docker-machine start <name of vm>
> docker-machine start vbox-test
```

## kill docker-machine

- kill only if the machine are not response of docker-machine stop or you can not login via docker-machine ssh
- for debug seethe output of the virtualbox GUI to

```bash
> docker-machine kill <name of vm>
> docker-machine kill vbox-test
```

## ip of current docker-machine

```bash
> docker-machine ip <name of machine>
> docker-machine ip default vbox-test
```

## deploy container inside docker-machine

```bash
> docker run --detach --publish <port local:port remote> <name of images>
> docker run -d -p 8000:80 nginx
```

- check local status of docker-machine from local prompt via ssh login

## connect service from container e.g. nginx

```bash
> curl $(docker-machine ip <name of machine>):<published port>
> curl $(docker-machine ip vbox-test):8000
```

## remove docker-machine

```bash
> docker-machine rm <name of machine>
> docker-machine rm vbox-test
```