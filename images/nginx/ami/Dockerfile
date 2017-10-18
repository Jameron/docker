FROM amazonlinux
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install -y nginx

#RUN echo "daemon off;" >> /etc/nginx/nginx.conf
#RUN ln -sf /dev/stdout /var/log/nginx/access.log
#RUN ln -sf /dev/stderr /var/log/nginx/error.log


#RUN mkdir -p /etc/service/nginx
#ADD start.sh /etc/service/nginx/run
#RUN chmod +x /etc/service/nginx/run

EXPOSE 80

# Start the service
CMD ["nginx", "-g", "daemon off;"]
