# crouton

crouton: http://goo.gl/fd3zc

old_crouton: https://github.com/runeandre/crouton_for_the_oldbooks/raw/refs/heads/master/installer/crouton

## installation

1. enable developer mode
    1. reboot into recovery mode: turn off device -> holding down `ESC`+`Refresh`+`Power` (Chrome OS is missing or damaged)
    2. press `Ctrl`+`D` (To turn OS verification OFF, press ENTER)
    3. press `Enter` (will reboot)
  
2. reboot (OS verification is OFF)
3. press `Ctrl`+`D`
4. log in or open guest mode
5. open new tab and press `Ctrl`+`Alt`+`T`
6. run `shell`
7. download crouton: `curl -L -O https://github.com/runeandre/crouton_for_the_oldbooks/raw/refs/heads/master/installer/crouton
`
8. run `sudo install -Dt /usr/local/bin -m 755 ~/Downloads/crouton`
9. run `sudo crouton -r list`
10. select and setup distro + desktop env:
    * `sudo crouton -r precise -t xfce -m http://old-releases.ubuntu.com/ubuntu/`
    * `sudo crouton -r precise -t unity -m http://old-releases.ubuntu.com/ubuntu/`
    * `sudo crouton -r xenial -t xfce`
    * `sudo crouton -r focal -t xfce`
11. start chroot desktop: `sudo startxfce4` or `sudo startunity`
12. switch between chrome os and chroot desktop: `Ctrl`+`Alt`+`Shift`+`Back` and `Ctrl`+`Alt`+`Shift`+`Forward`
13. exit: log out or shutdown on chroot desktop or switch to chrome os and press `Ctrl`+`C`

## usage

1. reboot (OS verification is OFF)
2. press `Ctrl`+`D`
3. log in or open guest mode
4. open new tab and press `Ctrl`+`Alt`+`T`
5. run `shell`
6. start chroot desktop: `sudo startxfce4` or `sudo startunity`
7. switch between chrome os and chroot desktop: `Ctrl`+`Alt`+`Shift`+`Back` and `Ctrl`+`Alt`+`Shift`+`Forward`
8. exit: log out or shutdown on chroot desktop or switch to chrome os and press `Ctrl`+`C`

## setup

1. refresh list: `sudo apt update`
2. install firefox: `sudo apt install firefox`
3. install curl: `sudo apt install curl`
4. install nano: `sudo apt install nano`
5. install git: `sudo apt-get install git`
6. install vscode
