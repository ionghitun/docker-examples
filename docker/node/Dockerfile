FROM node:22-bullseye-slim

USER root

ARG USER_ID
ARG GROUP_ID

RUN if [ `id -u node` -eq ${USER_ID} ] ; then groupmod -g 1099 node && usermod -u 1099 -g 1099 node; fi

RUN mkdir /var/www

RUN userdel -f www-data
RUN if getent group www-data ; then groupdel www-data; fi
RUN groupadd -g ${GROUP_ID} www-data
RUN useradd -l -u ${USER_ID} -g www-data www-data
RUN chown -R www-data:www-data /var/www

RUN install -d -m 0755 -o www-data -g www-data /home/www-data
RUN chown -R www-data:www-data /home/www-data

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y xdg-utils

RUN export EDITOR="/usr/bin/nano"

RUN npm update -g

USER www-data

WORKDIR /var/www

ENTRYPOINT ["tail", "-f", "/dev/null"]
