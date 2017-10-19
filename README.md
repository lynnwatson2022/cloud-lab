
# Cloud Lab

[Cloud Lab](http://tinylab.org/cloud-lab) is a Docker based online lab center, it integrates many popular computer
science courses and provides a Docker based experiment environment as-is.

## Quickstart

### Install docker

Cload Lab is docker based, please make sure docker environment is installed with [Docker CE](https://store.docker.com/search?type=edition&offering=community), Docker CE support Mac, Windows, Ubuntu, Debian, Fedora, CentOS, Azure and AWS, we have tested Cloud Lab with Docker CE in Ubuntu and Mac.

The old install method for Windows and Mac OSX is [Docker Toolbox](https://www.docker.com/docker-toolbox).

### Configure docker

In order to run docker without password, please make sure your user is added in the docker group:

    $ sudo usermod -aG docker $USER

In order to speedup docker images downloading, please configure a local docker mirror in `/etc/default/docker`, for example:

    $ grep registry-mirror /etc/default/docker
    DOCKER_OPTS="$DOCKER_OPTS --registry-mirror=https://docker.mirrors.ustc.edu.cn"
    $ service docker restart

In order to avoid network ip address conflict, please try following changes and restart docker:

    $ grep bip /etc/default/docker
    DOCKER_OPTS="$DOCKER_OPTS --bip=10.66.0.10/16"
    $ service docker restart

If the above changes not work, try something as following:

    $ grep dockerd /lib/systemd/system/docker.service
    ExecStart=/usr/bin/dockerd -H fd:// --bip=10.66.0.10/16 --registry-mirror=https://docker.mirrors.ustc.edu.cn
    $ service docker restart

### Choose a Lab

    $ tools/docker/choose

    Current Lab is: linux-lab

    Available Labs:

         1	cs630-qemu-lab
         2	linux-0.11-lab
         3	linux-lab
         4	markdown-lab
         5	qing-lab
         6	tinylab.org

    Choose the lab number: 2
         2	linux-0.11-lab


    Download the lab...

### Run the Lab

    $ tools/docker/run

### Remove the Lab

    $ tools/docker/rm

### Stop the Lab

    $ tools/docker/stop

### Start the Lab

    $ tools/docker/start

### Update everything

    $ tools/docker/update

### Run as root without password

If get syntax error under `/etc/sudoers*`, please use `pkexec visudo` to fix up it.

    $ sudo -s
    $ echo "$SUDO_USER ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$SUDO_USER
