# ====================================================================================
#   Thanks to Daniel Ribeiro for his work (https://github.com/drgomesp/symfony-docker)
#   And of course to Chema (https://github.com/jmsv23/docker-drupal)
# ====================================================================================

# This container is intended to be used like base common place for the different frameworks 
# and services developed in PHP like: Drupal, Magento, Symfony, etc.

# This Dockerfile was updated 17/07/2020 for reuse the Docker build images more efficiently
# so, please don't be use directly. For more details see the comments at the end of this file. 


# Use an official PHP runtime as a parent image
FROM php:7.2.32-fpm

LABEL maintainer "Alejandro G. Lagunas <alagunas@coati.com.mx>"

# Get the last available packages
RUN apt-get update

# Install any needed packages
RUN apt-get install -y libpng16-16
RUN apt-get install -y libpng-dev
RUN apt-get install -y git
RUN apt-get install -y mariadb-client
RUN apt-get install -y libicu-dev
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libjpeg62-turbo-dev
RUN apt-get install -y libxml2-dev
RUN apt-get install -y libxslt1-dev
RUN apt-get install -y libmcrypt-dev


# Run docker-php-ext-install for available extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
RUN docker-php-ext-install gd
RUN docker-php-ext-install intl
RUN docker-php-ext-install soap
RUN docker-php-ext-install xsl
RUN docker-php-ext-install zip
RUN docker-php-ext-install opcache
RUN docker-php-ext-install sockets

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set your timezone here...
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/America/Mexico_City /etc/localtime
RUN "date"

# The usage of this extension depends of database driver connection needed.

# -> Uncomment this line for CodeIgniter, Revivie AdServer
# RUN docker-php-ext-install mysqli

# -> Uncomment this line for Symfony 3 and 4, Laravel 5, 6 and 7;
RUN docker-php-ext-install pdo_mysql 

# tag: agomezguru/base7php:v7.2.32
# Example: docker build . --tag agomezguru/base7php:v7.2.32

# If you desire use this Docker Image directly, uncomment the next line. 
# CMD php-fpm -F

# End of file
