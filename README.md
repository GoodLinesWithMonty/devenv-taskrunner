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
Create a directory named ```.build``` in your project root path for your project setup e.g. docker compose files. In this directory you need a script file ```devenv-functions.sh``` which holds all your custom tasks.
You have to define bash functions in your script file for your custom needs, which can be executed then with ```devenv <function> <arg1> <arg2> ...```

## Customisation
You can name this devenv file whatever you want to define the cli command before you copy it to ```/usr/local/bin/devenv```.

```bash
sudo cp devenv /usr/local/bin/runmytask
sudo chmod +x /usr/local/bin/runmytask
```

## Best practice 
A dotenv file in the project build directory will be automatically loaded to export variables to your devenv functions.

<sub style="color:grey;"><project-root>/.build/.env</sub>
```
PROJECT_KEY="example"
```

## Examples

<sub style="color:grey;">Project folder tree</sub>
```text
project-root
├── .build                      <- required
│   ├── .env                    <- optional
│   ├── compose.yaml
│   ├── deploy.php
│   ├── devenv-functions.sh     <- required
│   └── Docker
│       └── php
│           └── Dockerfile
├── .composer
│   └── ...
├── web
│   ├── public
│   ├── vendor
│   └── ...
├── .gitignore
└── README.md
```

<sub style="color:grey;"><project-root>/.build/devenv-functions.sh</sub>
```bash
source ./Tasks/001-default.sh
source ./Tasks/002-install.sh
source ./Tasks/003-linting.sh

build:css() {
  gulp --dev build
}

start() {
  docker compose up "$@"
}

halt() {
  docker compose down "$@"
}

shell() {
  docker exec -it "$@" bash
}

composer() {
  docker exec -it "$1" composer "$@"
}
```