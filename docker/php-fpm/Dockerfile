# The container includes:
#
# - Git
# - PHP Version 5.5.9 (With FPM)
#

FROM debian:wheezy
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>

# Install php-fpm
RUN apt-get update \
  && apt-get install -y -qq \
      libxml2 \
      libcurl4-openssl-dev \
      php5-dev \
      php5-cli \
      php5-sqlite \
      php5-mysql \
      php5-mcrypt \
      php5-curl \
      php5-json \
      php5-gd \
      php5-fpm \
      php-pear \
      php-apc \
  && apt-get clean -qq \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Enable php modules
RUN php5enmod mcrypt

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh

# Configure nginx root with sample app
ADD web-root/ /var/www/public

EXPOSE 9000
CMD ["/run.sh"]