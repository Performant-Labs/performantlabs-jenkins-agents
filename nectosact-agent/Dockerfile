FROM jenkins/ssh-agent:latest

LABEL maintainer="Ilia Liaukin <ilia.liaukin@performantlabs.com>"

RUN apt update
RUN apt -y install curl
RUN curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/nektos/act/master/install.sh | bash
ENV PATH="$PATH:/home/jenkins/bin"

RUN curl -sSL https://get.docker.com/ | sh
