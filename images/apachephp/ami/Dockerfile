FROM amazonlinux
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install httpd24 vim php71 php71 php71-mbstring php71-pecl-imagick php71-opcache -y

EXPOSE 80

# Start the service
CMD ["-D", "FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]
