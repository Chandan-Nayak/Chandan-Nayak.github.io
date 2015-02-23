---
layout: post_page
title: Playing around with docker containers &#187
---

<p>
This was the second match between India vs SA live from the beautiful Melbourne Cricket Ground and i was again finding some thing to read while i enjoy the match. Knowing that docker is becoming so popular, I tried to search for some solid hands on content but i could not find many at same place. I will be posting a series of hands on docker stuff here.
</p>
<BR>
<h4>What is docker and why it is so famous</h4>
- <a href="https://www.docker.com/whatisdocker/#copy1">https://docs.docker.com</a>
- <a href="http://opensource.com/resources/what-docker">http://opensource.com/resources/what-docker</a>
- <a href="http://www.centurylinklabs.com/what-is-docker-and-when-to-use-it/">http://www.centurylinklabs.com/what-is-docker-and-when-to-use-it/</a>
<BR>
<h4>Why docker is good</h4>
1. Easy to make changes
2. Light weight and Fast
3. Segregation of duties
4. Reduced cycle time between code written and code deployed (portable, easy to build and easy to colaborate)
5. Docker encourages service oriented and microservices architectures
6. Flexible application model - It can be distributed where each application/service is connected by a series of containers - easy to scale debug, introspect and apps or it can also run the application inside one system and have many containers running inside it
<BR>
<h4>VM vs Docker</h4>
Virtual machines try to emulate virtual hardware, that means they are fat in terms of system requirement. however containers use shared operating systems. Instead of virtualizing they stay on top of a single linux instance. So they can exclude the most of the resources what was needed for VM and still operate. A perfectly tunes container system can hold 4-6 times of applications as a VM can. The key difference between containers and VMs is that while the hypervisor abstracts an entire device, containers just abstract the operating system kernel.This efficiency can turn out to be a huge difference when it comes to the large scale usage of VM on cloud. Cloud heavy infrastructure companies can save a lot using docker.
<BR>
<BR>
<h4>Docker componenets</h4>
1. Docker comes with docker command line client and a daemon. You can run both on the same machine or connect to a remote daemon on a remote machine
2. Docker images are layred format which uses union file system - It is built step by step following a series of instructions. Containers can be launched form the docker image. Images are like source code for for containers
3. Registries are two types - private and public, <a href="https://hub.docker.com/">dockerhub</a> is the place where you can store your source code, you can also host your own private registry if that is the requirement
4. Containers are launched form images and can contain one or more processes
<BR>
<h4>Install Docker on Ubuntu</h4>
{% highlight ruby%}
#This will install old docker version ~1.0
$ sudo apt-get install docker.io
#Installs the latest docker version 1.5
$ curl -sSL https://get.docker.com/ubuntu/ | sudo sh
{% endhighlight %}

To confirm docker is installed
{% highlight ruby%}
$ docker -v
Docker version 1.5.0, build a8a31ef
{% endhighlight %}
<BR>
<h4>Dockerhub login</h4>
Docker has a lot of useful docker images on dockerhub, to make use of it we need to signin to dockerhub. This is very simillar to github login where we get public repositories for free.
{% highlight ruby%}
$ docker login
#Provide username,email and password which you used on dockerhub to signin
{% endhighlight %}
<BR>
<h4>Hosting a static page on nginx using docker container</h4>
We will host a plain static index.html using nginx, we will see how to create an image which downloads nginx and does the configurations needed for us to deploy our index.html. This will also show how to use docker volumes where we will keep our index.html for deployment into the container. Lets check how to do this using docker container on the ubuntu host.
<BR><BR>
There are two ways we can build an image on docker

1. Using a base image from dockerhub > starting the container from the image > manually doing all our needed changes on > Docker commit
2. Create a Dockerfile with all the instructions and build an image from it
We will follow the option two here as this is the suggested way to do it and this can become a flexible way to do it when the complexity increases. 

Lets get started, create our Dockerfile at /opt/static/
{% highlight ruby%}
$ mkdir -p /opt/static
$ touch /opt/static/Dockerfile
{% endhighlight %}

Dockerfile content
{% highlight ruby linenos %}
FROM ubuntu:14.04
MAINTAINER chandan nayak "chandan.nayak@synerzip.com"
RUN apt-get update
RUN apt-get -yq install nginx
RUN mkdir -p /opt/page/
ADD global.conf /etc/nginx/conf.d/
ADD nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
{% endhighlight %}

Here is an explanation for what is written in the above Dockerfile

1. Line one checks if docker has ubuntu:14.04 image on the local machine, If not it goes on to pull this form dockerhub, this is a trimmed down ubuntu image maintained by docker.
2. Line two just adds the author info to the image
3. Third line RUN command will run any command provided by the user on the new layer and commit the changes, so here it will run apt-get update
4. Fourth line installs nginx in background. -y for noninteractive mode installation
5. Fifth line creates a directory called page under opt - where we will be placing our index.html later using the volume command
6. sixth and seventh adds nginx config files from current Dockerfile directory to targeted directories
7. Last line - EXPOSE informs Docker that the container will listen on the 80 port at runtime
<BR>

So, lets get the files in place
{% highlight ruby %}
$ apt-get install wget
$ cd /opt/static/
$ wget https://github.com/Chandan-Nayak/chandan-nayak.github.io/tree/master/resources/global.conf
$ wget https://github.com/Chandan-Nayak/chandan-nayak.github.io/tree/master/resources/nginx.conf
{% endhighlight %}

<BR>
From this Dockerfile we can build our new image using the docker build command. Lets build the image from this Dockerfile -> note the "." at the end
{% highlight ruby %}
$ sudo docker build -t chandan83/nginx .
{% endhighlight %}

Run the below command to check current available images
{% highlight ruby %}
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
chandan83/nginx     latest              c7cd7a031f59        19 hours ago        227 MB
chandan83/nginx1    latest              c7cd7a031f59        19 hours ago        227 MB
<none>              <none>              71ff56c41526        19 hours ago        227 MB
ubuntu              14.04               2d24f826cb16        2 days ago          188.3 MB
ubuntu              14.04.2             2d24f826cb16        2 days ago          188.3 MB
ubuntu              latest              2d24f826cb16        2 days ago          188.3 MB
ubuntu              trusty              2d24f826cb16        2 days ago          188.3 MB
ubuntu              trusty-20150218.1   2d24f826cb16        2 days ago          188.3 MB
{% endhighlight %}

Use the docker history command to check what actually happened when the image was built
{% highlight ruby %}
$ sudo docker history chandan83/nginx
{% endhighlight %}

Our Image is ready and we can go on to create our container, before doing that we need to get out index.html file which we want to land on the container's /opt/page directory at run time

{% highlight ruby %}
$ mkdir -p /opt/static/website
$ cd /opt/static/website
$ wget https://github.com/Chandan-Nayak/chandan-nayak.github.io/tree/master/resources/nginx.conf/index.html
{% endhighlight %}

Time to start the container from the image chandan83/nginx, Run the below command to start it
{% highlight ruby %}
$ sudo docker run -d -p 80 --name static_website -v $PWD/website:/opt/page chandan83/nginx nginx
{% endhighlight %}

Run this command to see all the containers
{% highlight ruby %}
$ docker ps -a
CONTAINER ID     IMAGE                     COMMAND    PORTS                   NAME
2335dc83135d     chandan83/nginx1:latest   "nginx"    0.0.0.0:49166->80/tcp   static_website
{% endhighlight %}

Our page is up and running, as you can see port 80 in the container is mapped to 49166 on the host, If we access
{% highlight ruby %}
localhost:49166
{% endhighlight %}
We will be able to access the hosted index.html page

   

