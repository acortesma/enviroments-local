FROM jenkins/ssh-agent:jdk17
USER root
RUN apt-get update && \
    apt-get -qy full-upgrade && \
    apt-get install -qy curl && \
    apt-get install -qy curl && \
    curl -sSL https://get.docker.com/ | sh

# Agregamos el usuario jenkins al grupo docker
RUN usermod -aG docker jenkins

EXPOSE 22
