
# Setting up Git within a Docker Container

search for REPLACE-ME and enter the needed information

run this steps as root from a docker container, step by step

`docker run -it ubuntu:focal bash`

## install git

`apt update && apt install git`
`git --version`

## install gpg
`apt update && apt install gpg`

## clone repo from server
`git clone https://REPLACE-ME-WITH-A-GIT-REPO-URL`

## set up git

see https://docs.github.com/en/get-started/quickstart/set-up-git

`git config gpg.program gpg`
`git config gpg.program`

`git config commit.gpgsign true`
`git config commit.gpgsign`

`git config user.name "REPLACE-ME"`
`git config user.email "REPLACE-ME"`

## create gpg key

see https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key?platform=linux

`gpg --full-generate-key`

`gpg --list-secret-keys --keyid-format=long`

`gpg --armor --export REPLACE-ME`

## tell github about your key

see https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account

## attach VS Code to your container

Attaching VS Code to a running container is very convenient with the following extensions

- Docker

https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker

- Kubernetes

https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools

Just use RMD (Right Mouse Button) and go

![Attaching](https://code.visualstudio.com/assets/docs/devcontainers/attach-container/k8s-attach.png)

