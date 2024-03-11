# Bash based task runner for all your projects

## What does it do?
This little script file ```devenv``` provides a cli task runner only written with bash for all your projects. 
It does not serve any functions, you have to define each useful function for your project on your own. 
Use it to handle docker compose commands or to interact with your toolchain in a normalized way for example.

## Requirements
You just need git installed on your machine, nothing else.

## Install
Copy the script file ```devenv``` to ```/usr/local/bin/devenv``` and make it executable ```chmod +x devenv```.

```bash
sudo cp devenv /usr/local/bin/
sudo chmod +x /usr/local/bin/devenv
```

## Usage
Create a directory for your project and create the directory ```.build``` within for your project specific stuff e.g. docker compose files. In this directory you need the script file ```devenv-functions.sh``` which holds all your custom tasks.
In your devenv-functions.sh file you have to define bash functions for your propose which can called with ```devenv nameOfYourFunction argument1 argument2```

## Customisation
You can name this devenv file whatever you want to define the cli command before you copy it to ```/usr/local/bin/devenv```.

```bash
sudo cp devenv /usr/local/bin/runmytask
sudo chmod +x /usr/local/bin/runmytask
```

## Example

<sub style="color:grey;"><project-root>/.build/devenv-functions.sh</sub>
```bash
include ./Tasks/001-default.sh
include ./Tasks/002-install.sh
include ./Tasks/003-linting.sh

build:css() {
  gulp --dev build
}

start() {
  docker compose up "$@"
}

halt() {
  docker compose down "$@"
}

docker:shell() {
  docker exec -it "$@" bash
}

composer() {
  docker exec -it "$1" composer "$@"
}
```