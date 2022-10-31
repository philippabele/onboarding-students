# Setting up Quarkus within a Docker Container

Set up Git. Please see other instructions on how to perform this.

run this steps as root from a docker container, step by step

`docker run -it ubuntu:focal bash`

# install quarkus cli

see https://quarkus.io/get-started/ for further information

``apt-get update; apt-get install -y curl``

``curl -Ls https://sh.jbang.dev | bash -s - trust add https://repo1.maven.org/maven2/io/quarkus/quarkus-cli/``

``curl -Ls https://sh.jbang.dev | bash -s - app install --fresh --force quarkus@quarkusio``

`quarkus create`

`cd code-with-quarkus`

set quarkus.http.host=0.0.0.0 in your application.properties (under src/main/resources)

`quarkus dev`

