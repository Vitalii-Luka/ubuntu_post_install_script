# Docker-based PHP development infrastructure. #

This is a part of the local infrastructure project which aims to create easy to install and use environment for PHP
development based on Ubuntu LTS.

1. `Ubuntu post-installation scripts` (this repository) - install software,
   clone repositories with `Docker infrastructure` and `Dockerizer for PHP` tool. Infrastructure is launched automatically
   during setup and you do not need start it manually. Read below information to get more info about what software is installed,
   where the files are located and why we think this software is needed.

2. [Docker infrastructure](https://github.com/Vitalii-Luka/docker_infrastructure) - run [Traefik](https://traefik.io/)
   reverse-proxy container with linked MySQL 5.6, 5.7, MariaDB 10.1, 10.3, phpMyAdmin and Mailhog containers.
   Infrastructure is cloned and run automatically by the `Ubuntu post-installation scripts`.
   Check this repository for more information on how the infrastructure works, how to use xDebug, LiveReload etc.

3. [Dockerizer for PHP](https://github.com/Vitalii-Luka/dockerizer_for_php) - install any Magento 2 version in 1
   command. Add Docker files to your existing PHP projects in one command. This repository is cloned automatically
   by the [Ubuntu post-installation scripts](https://github.com/Vitalii-Luka/ubuntu_post_install_script). Please, check
   [Dockerizer for PHP](https://github.com/Vitalii-Luka/dockerizer_for_php) repository to get more information on available
   commands and what the tool does.


## Environment ##

Automated environment installation script for Ubuntu 20.04 LTS x64 and above. Download it and run:

```bash
sh ubuntu_20.04.sh
```

**Important!**

Do not run it with `sudo` or when you switch to the root user. Never. Otherwise, a lot of things may have
insufficient permissions.

**PHP Upgrades**

In case of undesired PHP upgrades performed by Ubuntu run the following:

```bash
sudo update-alternatives --set php /usr/bin/php7.4
```



## Web-server application stack ##

See [Docker infrastructure](https://github.com/Vitalii-Luka/docker_infrastructure) and
[Dockerizer for PHP](https://github.com/Vitalii-Luka/dockerizer_for_php)


## Aliases ##

There are several useful alises added to the `~/.bash_aliases` file.

PHP (deprecated, 18.04 only):
- `PHP56` - switch to PHP 5.6
- `PHP70` - switch to PHP 7.0
- `PHP71` - switch to PHP 7.1
- `PHP72` - switch to PHP 7.2
- `PHP73` - switch to PHP 7.3

Connect to the database:
- `MY56` - connect to MySQL 5.6 server in the `mysql56` docker container (on port `3356`, the same as `mysql -uroot -proot -h127.0.0.1 --port=3356 --show-warnings`)
- `MY57` - connect to MySQL 5.7 server in the `mysql57` docker container (on port `3357`, the same as `mysql -uroot -proot -h127.0.0.1 --port=3357 --show-warnings`)
- `MY80` - connect to MySQL 5.7 server in the `mysql57` docker container (on port `3380`, the same as `mysql -uroot -proot -h127.0.0.1 --port=3380 --show-warnings`)
- `MY101` - connect to MariaBD 10.1 server in the `mariadb101` docker container (on port `33101`, the same as `mysql -uroot -proot -h127.0.0.1 --port=33101 --show-warnings`)
- `MY102` - connect to MariaBD 10.1 server in the `mariadb101` docker container (on port `33102`, the same as `mysql -uroot -proot -h127.0.0.1 --port=33102 --show-warnings`)
- `MY103` - connect to MariaBD 10.3 server in the `mariadb103` docker container (on port `33103`, the same as `mysql -uroot -proot -h127.0.0.1 --port=33103 --show-warnings`)
- `MY104` - connect to MariaBD 10.3 server in the `mariadb103` docker container (on port `33104`, the same as `mysql -uroot -proot -h127.0.0.1 --port=33104 --show-warnings`)

Misc (see [Dockerizer for PHP](https://github.com/Vitalii-Luka/dockerizer_for_php) for more details);:
- `DOCKERIZE` - run `/usr/bin/php7.x ${PROJECTS_ROOT_DIR}dockerizer_for_php/bin/console dockerize `
- `ENVADD` - run `/usr/bin/php7.4 ${PROJECTS_ROOT_DIR}dockerizer_for_php/bin/console env:add `

## Applications for development ##
- cUrl
- Git &amp; Git Gui
- Node Package Manager (NPM) &amp; Grunt - needed
- HomeBrew and mkcert

## Other software ##
- `Clipit` (18.04) / `Diodon` (20.04) - clipboard manager for easy copy/paste
- `htop` - process manager, better than `top`
- `Tweaks` - tuning you Ubuntu
- `KeePassXC` - encrypted password storage
- `Midnight Commander`
- `Shutter` - a tool for making and editing screenshots
- `Sublime Text` - text editor
- `Vim` - console text editor

**PHP modules that are installed:**
- bcmath
- bz2
- curl
- gd
- imagick
- imap
- intl
- mbstring
- mcrypt
- memcache
- mysql
- pear
- recode
- soap
- ssh2
- xml
- xmlrpc
- xdebug
- zip

`xDebug` is configured automatically and does not require additional adjustments if you use PHPStorm. `php.ini` settings are updated for development environment.
You may also want to download the [free Microsoft IE/Edge virtual machines for VirtualBox](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)


## HTTPS is insecure ##

If the certificates generated by `mkcert` are insecure then run the following and restart the browser:

```bash
mkcert -install
```

This may happen because browsers are not started during the software installation and local CA is not trusted yet.


## Tips for developers ##

1) Create bookmark for at least `~/misc` folder in Nautilus (file manager) - just move the folder to the left sidebar of Nautilus to add it to bookmarks.

2) Use Ubuntu `Startup Applications` to automate launching apps on system startup.

3) Use `Guake` dropdown terminal as an alternative to Terminal application. Set it to, for example, F1 key. Set switching tabs to ALT+1, ALT+2 and so on because this is a default shortkut for many other apps.

4) Enable workspaces in Ubuntu and learn how to use them (if not yet) and how to move windows between workspaces. You may like using static number of workspaces instead of dynamically adding/removing them.

If you prefer to loop through the current workspace apps only rather than all apps on all workspaces:

```bash
gsettings set org.gnome.shell.app-switcher current-workspace-only true
```

5) Use `Tweaks` to fine-tune your system.

6) It is possible to customize terminal output to show current time and Git branch when you-re inside the repository. Use $PS1 like this in your `~/.bashrc`:

```bash
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;35m\][\d \t] \[\033[01;33m\]\w\[\033[01;31m\]\[\033[01;34m\]$(__git_ps1)\[\033[01;31m\] > \[\033[01;32m\]'
```

Or take this one as an example and modify it for your needs (but be sure to backup the file before that).




