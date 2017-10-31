# Setting up a local Docker environment

# AWS AMI Linux

Mac Users, Docker wants to run web apps from the /Users/ directory. You will want to put your source code there.

Before getting started you will want to make sure you have done the following: 

1) Install the latest Docker on your machine if you haven't already. If you have VirtualBox installed make sure it is updated to the latest version.

2) Setup docker-machine, it is installed by default with Docker. Docker Machine is used to run docker containers.

3) Create a local virtual box. Open terminal, run `docker-machine create --driver virtualbox default`

If you are running MySQL you may need to allocate extra memory

    docker-machine create --driver virtualbox --virtualbox-memory 4096 default

or

    docker-machine create --driver virtualbox --virtualbox-memory 8192 default


4) Once that is finished you can check that it worked by listing your virtual boxes using this command: `docker-machine ls`

5) You can list commands for your new VM with this: `docker-machine env default`

6) Next you can connect your shell to your VM `eval "$(docker-machine env default)"`

To stop your machine run `docker-machine stop default`
To restart your machine run `docker-machine start default`

You can create an alias in your .bash_profile or .bashrc file to start up your machine and connect your shell like this:

    alias dockup="docker-machine start default && eval \"\$(docker-machine env default)\""

For more legit info visit this hyperlink: [Docker Machine Documentation](https://docs.docker.com/machine/get-started/)

7) Get the Amazon Linux Docker Image on your local machine by running this:

    docker pull amazonlinux

8) To get the composer docker package run: 

    docker pull composer/composer

9) Create your own apache image in a new folder on your machine where you want to store images. It can be anywhere, I put mine in my project webroot in a folder called docker and then images.

    ~/Users/project-folder/docker/images

10) From shell, navigate into your images folder and create a folder called apachephp. Then create a folder in the apachephp folder called ami(you might later want an Ubuntu apache image). Create a new file in the ami folder called Dockerfile and paste in the following:

    ~/Users/project-folder/docker/images/apachephp

```
FROM amazonlinux
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install httpd24 vim php71 php71-pdo php71-mbstring php71-pecl-imagick php71-opcache -y

EXPOSE 80

# Start the service
CMD ["-D", "FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]
```

10) Run this command from the folder to package up your docker image:

      docker build -t killacam/apachephp docker/images/apachephp/ami/.

If you need to rebuild your image after making changes run the command with --no-cache option.

      docker build --no-cache -t killacam/apachephp docker/images/apachephp/ami/.

11) Build your mysql container images/mysql/ami/Dockerfile

`
FROM amazonlinux
MAINTAINER Cameron Macfarlane <cammac1984@gmail.com>

RUN yum update -y
RUN yum install mysql56-server -y

RUN chown -R mysql:root /var/lib/mysql/

EXPOSE 3306
`

    docker build -t killacam/mysql docker/images/mysql/ami/.


    docker build --no-cache -t killacam/php docker/images/php/ami/.


Or you can run docker using pfp-fpm module with NGinx

`service:

`

    docker build --no-cache -t killacam/php-fpm docker/images/php-fpm/ami/.


11) Navigate to your web application and run your docker apache container with this command:

`docker run -it -p 8080:80 -v $(pwd)/docker/vhost.conf:/etc/httpd/conf.d/vhost.conf -v $(pwd):/var/www/html killacam/apachephp;` 

`docker run -it amazonlinux:latest /bin/bash`

To Stop your virtual machine run

 `docker-machine stop default`


To start your container as daemon (background) run

    docker-compose up -d

Then to see what images are running and get their ids run

    docker ps

To enter into a running instance's bash run this with the instance id

    docker exec -it e1b0b3f4d372 bash
