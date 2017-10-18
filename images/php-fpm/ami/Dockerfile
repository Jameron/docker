FROM amazonlinux:latest
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install -y php71 php71 php71-mbstring php71-pecl-imagick php71-opcache php71-fpm

# Start the service
#CMD ["-D", "FOREGROUND"]
#CMD php-fpm -d
#ENTRYPOINT ["/usr/bin/php-fpm-7.1"]
