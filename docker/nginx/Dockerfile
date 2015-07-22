#
# Nginx Dockerfile
#

# Pull base image.
FROM debian:wheezy
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>

COPY nginx_signing.key nginx_signing.key 

# Install Nginx.
RUN \
  echo "deb http://nginx.org/packages/debian/ wheezy nginx" >> /etc/apt/sources.list && \
  echo "deb-src http://nginx.org/packages/debian/ wheezy nginx" >> /etc/apt/sources.list && \
  cat /nginx_signing.key | apt-key add - && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
EXPOSE 443


# Registrator environment variables for service discovery
ENV SERVICE_80_CHECK_HTTP /health/endpoint/path
ENV SERVICE_80_CHECK_INTERVAL 15s
# Optional, Consul default value is used when not specified
ENV SERVICE_80_CHECK_TIMEOUT 5s

ENV SERVICE_443_NAME https
ENV SERVICE_80_NAME http
ENV SERVICE_TAGS www
