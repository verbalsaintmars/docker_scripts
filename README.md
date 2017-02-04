# createContainer

## Prerequisite

1. python 2.7+
2. python docker library: [python docker lib]

## Basic
createContinaer is 'project' based tool to create docker container for us.
Base on project type, script will prepare a docker container that mount needed volumes as well as modified passwd/group allowing us to debug in the host environment.
Those volumes are mounted:
- /var/log/deployer
- /home/shinto/deployer
- /home/shinto/host
- /etc/passwd
- /etc/group

## Usage
- --basesrc (required) git source root directory.
- --project (required) project type.
** deployer
** higgs_deployer
** racdb_deployer
** general
- --cmd Command to run in the created container. [default: tail -f /dev/null]
- --cname Created container name. [default: imageid_{timestamp}]
- --gid gid [default: current gid]
- --group group [default: deployer]
- --image image id [default: base on project, find image with tag: latest]
- --no_proxy_host host without proxy. [default: localhost,127.0.0.1]
- --privileged run with privileged enable [default: false]
- --root set C_FORCE_ROOT [default: true]
- --tag script will find the image base on provied tag [default: latest]
- --user user [default: deployer]
- --uid uid [default: current uid]
- --workdir working directory. Will create ./log ./src under working directory.
  [default: ./tmpxxxx]


## Example
```sh
$ ./createContainer --basesrc . --project deployer
```
Print out:
>Warning: source path: ./compute-konrad-deployer/deployer doesn't exist.
Access container: "docker exec -it 7dd96e77d6 /bin/sh"
Stop container: "docker stop 7dd96e77d6"
Remove container: "docker rm 7dd96e77d6"
List containers: "docker ps -a"
Stop all containers: "docker stop $(docker ps -a -q)"
Remove all containers: "docker rm $(docker ps -a -q)"
Log dir: /files/docker_image_factory/docker_scripts/container_helper/tmpSHafBX/log
Src dir: /files/docker_image_factory/docker_scripts/container_helper/tmpSHafBX/src


[python docker lib]: <https://github.com/docker/docker-py>
