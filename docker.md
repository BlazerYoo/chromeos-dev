# setting up docker

https://medium.com/@abiosoft/docker-on-chromebook-b9679e491c06

1. install qemu:
    1. `sudo apt update`
    2. `sudo apt install qemu-system`
2. prepare virtual machine:
    1. `mkdir termux-docker && cd termux-docker`
    2. `git clone https://github.com/pwdonald/chromeos-qemu-docker`
    3. `qemu-img create -f qcow2 virtual_drive 4G`
    4. curl -L http://dl-cdn.alpinelinux.org/alpine/v3.7/releases/x86_64/alpine-virt-3.7.0-x86_64.iso -o alpine_x86_64.iso
3. install alpine on virtual machine
