# create-bridge-network-docker

## Description

Consider 2 conatiners in one EC2 instance, which are not allocated to any network. So if we try to ping both containers using IP, it will work, but if we use container name, it will not work and result error. This is because both conatiners are in different network. So here, we will discuss how to create containers in same network and ping both using containers using name and IP.

![image](https://user-images.githubusercontent.com/100773863/162556228-6ef9b7c2-5aee-4f44-9a0d-7f24fd9fe1a0.png)


## Installation

If you need to download docker to the EC2 instance, then follow this:

~~~sh
sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo systemctl status docker.service
sudo usermod -a -G docker ec2-user
~~~

Please exit from the instance and login back to reflect the above changes

## Steps involved

## 1. Create network

~~~sh
docker network create mynet
~~~

> To see the IP of the network:
~~~sh
docker network inspect mynet
~~~
> Result

![image](https://user-images.githubusercontent.com/100773863/162556398-ae9d207b-451e-40f7-9704-6ba6ebf3a926.png)


## 2. Create container along with network

~~~sh
docker container run --name red --network mynet -d -it alpine:latest
docker container run --name blue --network mynet -d -it alpine:latest
~~~

> ![image](https://user-images.githubusercontent.com/100773863/162556488-06cb8825-b4df-462c-ae13-fe2e54730b23.png)


## 3. Let try to ping from local system

~~~sh
docker container exec blue ping -c 3 red
docker container exec red ping -c 3 blue
~~~

> ![image](https://user-images.githubusercontent.com/100773863/162556572-7227770e-f9a2-454d-a687-0066705c2050.png)


## Conclusion

This is how we can create bridge network for 2 containers. Please contact me when you encounter any difficulty error while using this terrform code. Thank you and have a great day!


### ⚙️ Connect with Me
<p align="center">
<a href="https://www.instagram.com/dev_anand__/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/dev-anand-477898201/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a>

