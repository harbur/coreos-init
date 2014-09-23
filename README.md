CoreOS Initialization
=====================

This is a script for preparing CoreOS systems automatically. It features the following:

* It installs btrfs-swapon script (https://github.com/sebastian-philipp/btrfs-swapon)
* It installs docker-enter script (https://github.com/jpetazzo/nsenter/blob/master/docker-enter)
* It installs fig (http://www.fig.sh/install.html)
* It creates 2Gb swapfile

To use it, directly on new CoreOS instances:

<pre>
git@github.com:harbur/coreos-init.git
cd coreos-init
sudo ./install
</pre>

You'll then be able to see the following:

h2. Swap

<pre>
core@demo ~ $ swapon -s
Filename				Type		Size	Used	Priority
/dev/loop2                             	partition	2097148	69420	-1
</pre>

<pre>
core@demo ~ $ free -m 
             total       used       free     shared    buffers     cached
Mem:           494        487          6          0          0         51
-/+ buffers/cache:        436         58
Swap:         2047         67       1980
</pre>

h2. Fig

<pre>
core@demo ~ $ fig 
Punctual, lightweight development environments using Docker.

Usage:
  fig [options] [COMMAND] [ARGS...]
  fig -h|--help

Options:
  --verbose                 Show more output
  --version                 Print version and exit
  -f, --file FILE           Specify an alternate fig file (default: fig.yml)
  -p, --project-name NAME   Specify an alternate project name (default: directory name)

Commands:
  build     Build or rebuild services
  help      Get help on a command
  kill      Kill containers
  logs      View output from containers
  ps        List containers
  rm        Remove stopped containers
  run       Run a one-off command
  scale     Set number of containers for a service
  start     Start services
  stop      Stop services
  up        Create and start containers
</pre>

h2. docker-enter

Docker-enter is a wrapper script that helps to nsenter inside containers. It uses as parameter the container id or name to identify the namespace.

Note: Remember prefix `sudo` on docker-enter commands as it needs to run as root to get the necessary privileges.

<pre>
core@demo ~ $ docker run --name jenkins -d -P quay.io/harbur/jenkins
fdf7ff06b4f1d44e1558506c70b9a325d4c0595f68637c883b22968968f9c87f
</pre>

<pre>
core@demo ~ $ sudo docker-enter jenkins
root@fdf7ff06b4f1:~# 
</pre>
