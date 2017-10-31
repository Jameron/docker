FROM amazonlinux
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install mysql56-server -y

RUN chown -R mysql:root /var/lib/mysql/

EXPOSE 3306
