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


- to see list fo docker volumes
> docker volume ls

- to create volume using docker command use below command

> docker volume create <volume_name>

- to create named volume use below command

> docker run -d -p 3000:80 --rm --name <container_name> p -v <any_name_to_your_voume>:<folder_path> <name_of_your_image>:tag

For Ex. 
> docker run -d -p 3000:80 --rm --name feedback-app -v  feedback:/app/feedback feedback-node:volume

To remove unused anonymous volumes
> docker volume rm VOL_NAME 
or 
> docker volume prune


- Bind Mounts - Shortcuts
Just a quick note: If you don't always want to copy and use the full path, you can use these shortcuts:

macOS / Linux: -v $(pwd):/app

Windows: -v "%cd%":/app

I don't use them in the lectures, since I want to show an approach that works for everyone (and I don't want to switch between both all the time), but you can use these shortcuts depending on which OS you are working on to save some typing.

- To Inspect Volume 
> docker volume inspect <volume_name>

- To pass Environement variable value
> docker run -p 3000:80 --env <environment_variable>=<value> <container_name>
or 
> docker run -p 3000:80 -e <environment_variable>=<value> <container_name>

Note : to use multiple environment_variable, use 
> docker run -p 3000:80 -e <environment_variable>=<value> -e <environment_variable>=<value> <container_name>


============================================
Docker Deployment Commands
============================================
Step 1 : build image
> docker build .
> docker build -t <image_name> .
> docker build -t node_example .
 -t : tag name to the image

Step 2 : To Run Image on Container
> docker run -d --rm --name <container_name> -p <host_port>:<image_port> <image_name>
> docker run -d --rm --name node_app -p 80:80 node_example
 -d : detach mode
 --rm : remove container once it is stopped
 -p : port
 --name : name of the container
 
-Volume
-- bind mount (container have their own data/files and detached from host machine file system)
-v /local/path:/container/path

-- persistant data
-- name container (store data in container internally, will lost the data if container is removed)
-v NAME:/container/path  (named volume)
-v /container/path  (annonymous volume)

 
============================================
 To Push Image on Docker Hub and AWS EC2
============================================

To see list of images locally
> docker images

To tag Image (renaming by tag)
> docker tag <existing_image_name> <new_image_name>
> docker tag node_example docker_id/reponame

To Push image on docker hub
> docker push <image_name>
> docker push docker_id/reponame

To Run Image on EC2 (Remote machine)
> sudo docker run -d --rm --name node_app -p 80:80 <image_name>
> sudo docker run -d --rm --name node_app -p 80:80 docker_id/reponame

To See Runing container on Remote EC2 Machine
> sudo docker ps

To Pull image from the docker hub
> sudo docker pull <image_name>
> sudo docker pull docker_id/reponame

==================Kubernates=======================
Install minikube
> minikube dashboard (to see runing pods on browser)

==================================================
Deployment - Using the Imperative Approach (Use Commands to Deployment)
==================================================
To create new Deployment Object
> kubectl create deployment <name_of_your_deployment(any_name)> --image=<docker_hub_image_name>

to get list of deployments
> kubectl get deployments

To get list of pods
> kubectl get pods

To delete deployment
> kubectl delete deployment <name_of_your_deployment>

to Expose Shared IP (Public IP) to communicate between the pods or to access the application in browser use below command to create service and expose the IP address using LoadBalance
> kubectl expose deployment <name_of_your_deployment> --type=LoadBalancer --port=<exposed_port_by_your_application>

To see list of service created
> kubectl get services

To get the working url/ip using minukube for local system (developer system) use below command (This will work only local system if you have installed Minikube)
> minikube service <name_of_your_deployment>

To Scale your application/container 
> kubectl scale deployment/<name_of_your_deployment> replicas=<no_of_container_you_want_to_run>
Note : it will create <no_of_container_you_want_to_run> in same pod

To update an image after you change something in source code and redeploy it on pods
> kubectl set image deployment/<name_of_your_deployment> <container_name>=<docker_hub_image_name>

To check the status of your Image deployment
> kubectl rollout status deployment/<name_of_your_deployment>

To Rollback deployment
> kubectl rollout undo deployment/<name_of_your_deployment>

To check the deployment history
> kubectl rollout history deployment/<name_of_your_deployment>

To see the details of the deployment from the history
> kubectl rollout history deployment/<name_of_your_deployment> --revision=3

To deploy specific version from the deployment from the history
> kubectl rollout undo deployment/<name_of_your_deployment> --to-revision=1

==================================================
Deployment - Using the Declarative Approach (Use File for deployment)
==================================================
Refer URL : https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

Create two yaml file with any name of your choice for ex. deployment.yaml, service.yaml

To deploy using declarative approach, use below command
>kubectl apply -f deployment.yaml

To Delete the pods/deployment
>kubectl delete -f=deployment.yaml,<multiple_file_name>
>kubectl delete -f=deployment.yaml  -f=service.yaml

delete deployment by selector/label
>kubectl delete -l <label_name>:<label_value>

delete deployment by selector/label by kind 
>kubectl delete <kind_name> -l <label_name>:<label_value>
For ex. >kubectl delete deployment,service -l group:example

set imagePullPolicy: Always to pull image every time 

To get Storage Classes
> kubectl get sc

To get list of Persistence Volume 
>kubectl get pv

To get list of Persistence Volume Claims
>kubectl get pvc

To get list of configmap
> kubectl get configmap

MVIP : Kubernate create automatically Environment variable to get the IP address of the service, the name of the environment variable is service name in capital latters and - will be replaced with _. 
For ex. if your service name is like auth-service will be AUTH_SERVICE_SERVICE_HOST

To Get List of namespaces	
> kubectl get namespaces

To See Logs 
> kubectl logs -f pod_name


kubectl get pods 

To Get List Of Files on Linux
============================
> ls

Open File in Linux
===================
> sudo nano filename
Ex. sudo nano ocelot.json
Ex. sudo nano appsettings.json
---- cd /volume/configuration

kubectl get pods
kubectl delete pods <pod_name>
