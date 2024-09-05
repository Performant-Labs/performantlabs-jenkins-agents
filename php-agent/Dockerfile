FROM jenkins/ssh-agent:latest

LABEL maintainer="Ilia Liaukin <ilia.liaukin@performantlabs.com>"

RUN apt update
RUN apt install -y php8.2 php8.2-curl php8.2-xml php8.2-mbstring php8.2-gd unzip curl

RUN cd ~
RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
RUN php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
