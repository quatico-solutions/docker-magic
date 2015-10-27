# docker-magic
Docker command-line aliases. Copy these to your .zshrc or .bashrc.

# ------------------------------------
# Docker alias and function
# ------------------------------------
alias dm='docker-machine'
alias dc='docker-compose'

# Start a docker machine and connect shell
docker-machine-start() { docker-machine start $1 && eval "$(docker-machine env $1)"; }
alias dmstart=docker-machine-start

# Get latest container ID
alias dl="docker ps -l -q"

# Get container process
alias dps="docker ps"

# Get process included stop container
alias dpa="docker ps -a"

# Get images
alias di="docker images"

# Remove given image
alias drmi="docker rmi -f"

# Remove given container
alias drm="docker rm -v"

# Get container IP
alias dip="docker inspect --format '{{ .NetworkSettings.IPAddress }}'"

# Execute docker command
alias de="docker exec -it"

# Execute docker shell
docker-shell() { docker exec -it $1 /bin/bash; }
alias dshell=docker-shell

# Run deamonized container, e.g., $drund base /bin/echo hello
alias drund="docker run -d -P"

# Run interactive container, e.g., $druni base /bin/bash
alias druni="docker run -i -t -P"

# Stop and remove container
docker-stop() { docker stop $1 && docker rm -v $1; }
alias dstop=docker-stop

# Stop all containers
docker-stop-all() { docker stop $(docker ps -a -q); }
alias dstopall=docker-stop-all

# Stop and Remove all containers
alias drmall='docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)'

# Remove all images
docker-rmi-all() { docker rmi $(docker images -q); }
alias drmiall=docker-rmi-all

# Dockerfile build, e.g., $dbu tcnksm/test
docker-build() { docker build -t=$1 .; }
alias dbu=docker-build

# Show all alias related docker
dalias() { alias | grep 'docker' | sed "s/^\([^=]*\)=\(.*\)/\1 => \2/"| sed "s/['|\']//g" | sort; }
unset -f docker-machine-start docker-shell docker-stop docker-stop-all docker-rmi-all docker-build
