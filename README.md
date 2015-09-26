# Node 4 on Docker

## Install [Docker]()

### OSX:

#### Prerequisites
Make sure you have installed [Homebrew](http://brew.sh/) and [Homebrew-Cask](http://caskroom.io/).
```sh
# Install Homebrew
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Install Homebrew-cask
$ brew install caskroom/cask/brew-cask

```

#### Install Docker
```sh
$ brew cask install virtualbox
$ brew install docker docker-machine
```

## Create Virtual Machine (VM)
#### Create `dockernodevm` VM
```sh
$ docker-machine create --driver virtualbox dockernodevm

# See current vm's
$ docker-machine ls

# NAME           ACTIVE   DRIVER       STATE     URL
# dockernodevm   *        virtualbox   Running   tcp://192.168.99.102:2376
```
#### Get environment settings of `dockernodevm`
```sh
$ docker-machine env dockernodevm

# Setup on our computer
eval "$(docker-machine env dockernodevm)"

# Check if everything is ok
$ docker run hello-world
```

## Run this project

#### Create image and run app
```sh
# Let's name the container: `myimage`
$ docker build -t myimage .

# Sending build context to Docker daemon 1.171 MB
# Step 0 : FROM node:4.1.1-onbuild
# ...
# Successfully built f98b01458d39

$ docker run -d -P --name myapp myimage

# Display current containers
$ docker ps --all
```

#### Access to app
```sh
# Get app port
$ docker port myapp
# 3000/tcp -> 0.0.0.0:32771

# Get VM ip
$ docker-machine ip dockernodevm
# 192.168.99.102
```

Now on your browser, go to `192.168.99.104:32771`
