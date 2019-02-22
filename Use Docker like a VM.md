# Use Docker like a VM

Docker has many usages. It can also be used like a simple virtual machine.

Recently I was doing a hw and trying to install a virtual machine. But I recalled that I used docker in my web application class. So why shouldn't keep using it?

Using docker has many benefit, you can just google it. But in this case, it is just faster and smaller.

## 1. Installation

Go to https://docs.docker.com/get-started/. Simple :)

For this tutorial, go through the part 1 is enough.

## 2. Some terms:

**Image**: something like ubuntu.iso. But in docker, it can also be a Python flask/sql environment . Go to https://hub.docker.com/ check what people have posted. You can also make your own image.

**container**: Instance of **Image**. Just like Win7/ubuntu/Mac os what you currently are using. 

## 3. Build a Ubuntu Container in Docker

**just one command**: docker run -it -v[the folder in your machine]:[the fold in container] -p [port # in your machine]:[port # in container] --name [name] [Image Name]

In this case: ***docker run -it -v ~/docker:/root -p 80:8080 --name Shen ubuntu***

I will explain what this command does in detail

1. docker run ubuntu

   This will downlooad **ubuntu** image (if you don't have the image)and make a running container for you. 

2. -it 

   this option will create a interactive terminal for you to use. Otherwise it is just inconvenient.

3. -v  [the folder in your machine]:[the fold in container]

   Map the folder in your machine to the fold in Ubuntu container. Super useful for file transfer.

4. -p [port # in your machine]:[port # in container]

   Map the port # in your machine to the port # in Ubuntu container. Super useful for web development.

5. --name 

   give a name to your container. optional

After running $docker run -it -v ~/docker:/root -p 80:8080 --name Shen ubuntu

you will probably have something like

root@d4323f6e55ec:/#  in terminal. Then do what ever you want to do with the system.

## 4. After 3

You can quit the container terminal by Ctrl-d.

If you want to enter the container again, use 

***docker start -i Shen* **		//don't use ***docker run***, it will create another container(not a big issue)

Also the ubuntu container you have is minial for running. 

Run *apt-get update* for getting the lastes package list.

Then you can run ***apt-get install make/g++/vim...*** to get whatever you usually use.

## 5. More on docker command 

several useful docker commands

***docker image --help*** check list of image related command

e.g. ***docker image ls***  

***docker rmi -f ubuntu* **

***docker stop shen***

***docker container --help*** check list of container related command

e.g. ***docker container stop [container id]***

***docker container rm [container id]***

***docker container rm $(docker container -aq)***  removes all containers

...

***docker ps: display currently-running containers***

***docker start -i shen***

***docker rename shen shen1*** 

***docker exec -it shen bash*** open another terminal

Also you can try to push your container to docker repo, and keep commiting and pushing your own docker image. Then you can quickly have your working environment everywhere :) Google it, not hard.



## 6. Upload to Dockerhub

***docker login*** first to gain access

***docker tag <existing-image> <hub-user>/<repo-name>[:<tag>]*** //tag existing image

***docker build -t <hub-user>/<repo-name>[:<tag>]*** //build with tag

***docker push <hub-user>/<repo-name>:<tag>***

***docker commit <existing-container> <hub-user>/<repo-name>[:<tag>]*** //tag existing container

 e.g:

***docker commit d4323f6e55ec  redhairdragon/shen:first*** //tag shen as first

***docker push redhairdragon/shen:first*** //push to repo as tag  *first*

***docker pull redhairdragon/shen:first***

