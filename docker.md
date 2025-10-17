# setting up docker

instructions adapted from: https://medium.com/@abiosoft/docker-on-chromebook-b9679e491c06

1. install qemu in crouton env:
    1. `sudo apt update`
    2. `sudo apt install qemu-system`
2. prepare virtual machine:
    1. create directory: `mkdir termux-docker && cd termux-docker`
    2. clone required repo: `git clone https://github.com/pwdonald/chromeos-qemu-docker`
    3. create 4GB virtual hard drive (adjust size based on available space): `qemu-img create -f qcow2 virtual_drive 4G`
    4. [download](https://www.alpinelinux.org/downloads/) alpine linux iso: `curl -L -o alpine_x86_64.iso https://dl-cdn.alpinelinux.org/alpine/v3.22/releases/x86_64/alpine-virt-3.22.2-x86_64.iso`
3. modify scripts:
    1.  `nano ./chromeos-qemu-docker/scripts/start_persist.sh`
        *  replace `qemu` with `qemu-system-x86_64`
        *  replace `-localtime` with `-rtc base=localtime`  
    2.  `nano ./chromeos-qemu-docker/scripts/setup_alpine.sh`
        *  replace `qemu` with `qemu-system-x86_64`
        *  replace `-localtime` with `-rtc base=localtime`  
4. install alpine on vm
    1. start vm for setup: `bash ./chromeos-qemu-docker/scripts/setup_alpine.sh`
    2. enter `root` for `localhost login:`
    3. after boot, run alpine setup: `setup-alpine` (can use defaults except selecting disk drive and keyboard layout)
    4. <details><summary>Click to see setup specs</summary>
        
        ```
        [] - means default
        1. system hostname (Enter system hostname): [localhost]
        2. network interface (Which one do you want to initialize): [eth0]
        3. ip address (Ip address for eth0): [dhcp]
        4. manual network config (Do you want to do any manual network configuration): [n]
        5. root password (New password)
        6. timezone (Which timezone are you in): [UTC]
        7. proxy (HTTP/FTP proxy URL): [none]
        8. NTP client (Which NTP client to run): [busybox]
        9. mirror (Enter mirror number of URL): [1] (find and use fastest mirror)
        10. user (Setup a user): [no]
        11. SSH server (Which ssh server): [openssh]
        12. (Allow root ssh login): default is [prohibit-password] but yes
        13. (Enter ssh key or URL for root): [none]
        14. disk (Which disk(s) would you like to use?): default is [none] but sda
        15. use disk (How would you like to use it): default is [?] but sys
        16. erase disk (WARNING: Erase the above disk(s) and continue): default [n] but y
        ```
        </details>
    5. exit vm: `Ctrl`+`A` `X`
5. install docker in vm
    1. start vm: `bash ./chromeos-qemu-docker/scripts/start_persist.sh`
    2. install nano: `apk add --update nano`
    3. `nano /etc/apk/repositories`
        * uncomment community repo (ie. remove `#` for `#http://dl-cdn.alpinelinux.org/alpine/v3.22/community`)
    4. install docker: `apk add --update docker`
    5. start docker: `service docker start`
    6. check status: `service docker status`
    7. stop docker: `service docker stop`
6. set up docker client on host (crouton env) to use docker commands from crouton env instead of inside vm
    1. modify start script to forward port `2375`:
        1. `nano ./chromeos-qemu-docker/scripts/start_persist.sh`
        2. add `,hostfwd=tcp::2375-:2375` to `-net` flag
        3. shutdown vm: `Ctrl`+`A` `X`
    2. restart vm: `bash ./chromeos-qemu-docker/scripts/start_persist.sh`
    3. modify docker daemon settings to let it listen on `:2375`:
        1. `nano /etc/init.d/docker`
        2. add `DOCKER_OPTS='-H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375'` before `command`
        3. restart docker: `service docker restart`
    4. in crouton env, [download](https://download.docker.com/linux/static/stable/x86_64/) and install docker client
        1. `curl -L -o docker-ce.tgz "https://download.docker.com/linux/static/stable/x86_64/docker-28.5.1.tgz"`
        2. `tar xvfz docker-ce.tgz`
        3. `sudo mv docker/docker /usr/local/bin`
        4. `sudo chmod +x /usr/local/bin/docker`
        5. test it: `docker -H tcp://127.0.0.1:2375 ps`
        6. make it permanent:
            1. `echo 'export DOCKER_HOST=tcp://127.0.0.1:2375' >> ~/.bashrc`
            2. `source ~/.bashrc`
