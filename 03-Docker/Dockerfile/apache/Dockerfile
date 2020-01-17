# Base Image
FROM ubuntu:16.04

# Maintiner
MAINTAINER Amit Vashist <amitvashist7@gmail.com>

# UPDATE APT REPO
RUN apt-get update

# Install Apache Packages
RUN apt-get install apache2 -y 

EXPOSE 80
EXPOSE 9091

# New Web Page
COPY amit.html /var/www/html/myapp.html


# Excute the Service
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
