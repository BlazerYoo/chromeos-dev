# setting up chrome os for development

crouton: http://goo.gl/fd3zc

old_crouton: https://github.com/runeandre/crouton_for_the_oldbooks/raw/refs/heads/master/installer/crouton

## crouton setup

1. enable developer mode
    1. reboot into recovery mode: turn off device -> holding down `ESC`+`Refresh`+`Power` (Chrome OS is missing or damaged)
    2. press `Ctrl`+`D` (To turn OS verification OFF, press ENTER)
    3. press `Enter` (will reboot)
  
2. reboot (OS verification is OFF)
3. press `Ctrl`+`D` (will transition to developer mode)
4. log in or open guest mode
5. open new tab and press `Ctrl`+`Alt`+`T`
6. run `shell`
7. run `cd ~/Downloads`
8. download crouton:
    * default: `curl -LO http://goo.gl/fd3zc`
    * older devices: `curl -LO https://github.com/runeandre/crouton_for_the_oldbooks/raw/refs/heads/master/installer/crouton
`
9. run `sudo install -Dt /usr/local/bin -m 755 ./crouton`
10. run `sudo crouton -r list`
11. select and setup distro + desktop env:
    * `sudo crouton -r precise -t xfce -m http://old-releases.ubuntu.com/ubuntu/`
    * `sudo crouton -r precise -t unity -m http://old-releases.ubuntu.com/ubuntu/`
    * `sudo crouton -r xenial -t xfce`
    * `sudo crouton -r focal -t xfce`
12. assign username + password
13. start chroot desktop: `sudo startxfce4` or `sudo startunity`
14. switch between chrome os and chroot desktop: `Ctrl`+`Alt`+`Shift`+`Back` and `Ctrl`+`Alt`+`Shift`+`Forward`
15. exit: log out or shutdown on chroot desktop or switch to chrome os and press `Ctrl`+`C`

## crouton usage

1. reboot (OS verification is OFF)
2. press `Ctrl`+`D`
3. log in or open guest mode
4. open new tab and press `Ctrl`+`Alt`+`T`
5. run `shell`
6. start chroot desktop: `sudo startxfce4` or `sudo startunity`
7. switch between chrome os and chroot desktop: `Ctrl`+`Alt`+`Shift`+`Back` and `Ctrl`+`Alt`+`Shift`+`Forward`
8. exit: log out or shutdown on chroot desktop or switch to chrome os and press `Ctrl`+`C`

## dev setup

1. refresh list: `sudo apt update`
2. firefox: `sudo apt install firefox`
3. curl: `sudo apt install curl`
4. nano: `sudo apt install nano`
5. git: `sudo apt-get install git`
6. `cd ~/Desktop && mkdir dev && cd ./dev`
7. vscode:
    1. `curl -L -o code.deb "https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64"`
    2. `sudo apt install ./code.deb`
8. docker: see [docker.md](https://github.com/BlazerYoo/chromeos-dev/blob/main/docker.md)
