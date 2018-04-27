FROM php:5-apache

RUN apt-get update

# mysqli
RUN docker-php-ext-install mysqli

# ldap
RUN apt-get install -y \
        libldap2-dev && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap

# mcrypt
RUN apt-get install -y \
        libmcrypt-dev && \
    docker-php-ext-install -j$(nproc) mcrypt

# soap
RUN apt-get install -y \
        libxml2-dev && \
    docker-php-ext-install soap

# json
RUN docker-php-ext-install json

# gd
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-enable gd

# Graphviz
RUN apt-get install -y \
        graphviz

# cli

# zip 
RUN apt-get install -y \
        zlib1g-dev && \
    docker-php-ext-install zip 

# Other packages
RUN apt-get install -y \
        wget unzip

RUN rm -rf /var/lib/apt/lists/*

# Download latest iTop
RUN wget -O /itop.zip --trust-server-names https://sourceforge.net/projects/itop/files/latest/download
RUN unzip /itop.zip 'web/*' -d /var/www
RUN rm -rf /var/www/html; mv /var/www/web /var/www/html; chown www-data:www-data -R /var/www/html
WORKDIR /var/www/html

# Define session temp path
RUN echo "session.save_path = /tmp" > /usr/local/etc/php/conf.d/session.ini

# Download extension TeemIP Module
RUN wget -O /teemip.zip --trust-server-names https://sourceforge.net/projects/teemip/files/teemip%20-%20an%20iTop%20module/2.2.1/teemip-core-ip-mgmt-2.2.1.zip/download
RUN unzip /teemip.zip -d extensions/

#RUN /install-toolkit.sh

# Download extension TeemIP Discovery Module
#COPY teemip-discovery-module*.zip /app/extensions
#RUN unzip /app/extensions/teemip-discovery-module*.zip -d /app/extensions
#RUN rm -rf /app/extensions/teemip-discovery-module*.zip

EXPOSE 80
