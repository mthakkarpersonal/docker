Step 1 : To Create an Image
> docker build <docker path> (. means working directory if docker file in working directory)
ex . docker build . 

Step 2 : To run created docker image use below command. in windows image id will be generated like 
"writing image sha256:9a9598444c36818cf8933459b64e366b0a22c0ddce40ae984d409b6de0a76fcc" 
so here your image id will be "9a9598444c36818cf8933459b64e366b0a22c0ddce40ae984d409b6de0a76fcc"

> docker run <image_id> 
Ex. docker run 9a9598444c36818cf8933459b64e366b0a22c0ddce40ae984d409b6de0a76fcc

Note : run command will create new container and will run your image in it. 
so if there is no any code change and you want to run your image again then use "start" command instead of "run" command as below
using run command, container is runing in foreground, and using start command, container is runing in background.
start runing docker container is detach mode, while run runing docker container in attach mode.

> docker start <container_name>
> docker start -a <container_name> (to start container with attach mode. -a means attach)

if you want to run container with detach mode using run command then use below command (-d means detach mode)
> docker run -p 3000:80 -d 9a9598444c36818cf8933459b64e366b0a22c0ddce40ae984d409b6de0a76fcc

to attach again use below command
> docker attach <container_name>

note : in detach mode you can not see the logs, to see logs in detach mode use below command
> docker logs <container_name>

if you want to see logs now onwards in detach mode then use below command, (-f means follow logs output)
> docker logs -f <container_name> 

step 3: to see running container 
> docker ps 
- to see list of images
> docker images

step 4: to stop runing docker image
> docker stop <image_name>
Ex. docker stop agitated_boyd

step 5 : to see all (running/not running) container after stop docker image, -a means all
> docker ps -a

step 6 : to run your docker image use below command
> docker run -p any_port:exposed_port_in_docker_file image_id
    -p means publish
> docker run -p 3000:80 9a9598444c36818cf8933459b64e366b0a22c0ddce40ae984d409b6de0a76fcc 


- To Run docker container in interactive terminal you can use below command
> docker run -it <image_name>

- To remove docker container, 
first make sure the container is not running
> docker stop <container_name>
> docker rm <container_name> <container_name>

- to remove images
> docker rmi <image_id>

- To automatically remove the image once the container is stop use below command (--rm means remove automatically once container is stopped)
> docker run -p 3000:80 -d --rm <image_id>

- to remove all not running image
> docker purne -a


- copy any files or folder inside running container, use below command

> docker cp file_or_folder_path <container_name>:<destination_folder_path>

for Ex. docker cp dummy/. <container_name>:/test

- copy any files or folder from running container to local system, use below command

> docker cp <container_name>:<destination_folder_path> file_or_folder_path 

for Ex. docker cp <container_name>:/test dummy

- to give name to your container use below command

> docker run -p 3000:80 --name <name_of_your_choice> <container_name>

- to push docker image on hub

> docker push <image_name>

- to use image from docker hub

> docker pull <image_name>

- to tag to already created image in local, (Note : it will create clone of the existing image)

docker tag node-demo:latest <new_name>

- docker login/logout from docker hub
> docker login or docker logout
