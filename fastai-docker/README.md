# Fastai docker
Con este Dockerfile es posible crear un contenedor con todas las configuraciones necesarias para correr los notebooks de los cursos
- [Lesson 1](http://course.fast.ai/lessons/lessons.html "Fastai Lesson 1")
- [Lesson 2](http://course.fast.ai/lessons/lessons2.html "Fastai Lesson 2")

### Prerequisitos
Para poder correr este contenedor es necesario tener instalado previamene lo siguientes:
- [Docker CE](https://docs.docker.com/install/linux/docker-ce/ubuntu/ "Docker Community Edition")
- [NVIDIA-docker](https://github.com/NVIDIA/nvidia-docker)
- [nvidia-docker-compose](https://github.com/eywalker/nvidia-docker-compose "Allow docker-compose to work with GPU")
- Nvidia Drivers

### Build and Run
Para poder construir la imagen correr el siguiente comando dentro de la carpeta
```
sudo docker build fastai . 
```
Para levantar el contenedor correr el siguiente comando
```
sudo docker run --name fastai --runtime=nvidia -d -p 8888:8888 fastai
```
Una vez creado el contenedor, es posible volver a correr el contenedor previamente levantado ejecutando el siguiente comando
```
docker restart fastai
```

### Montar usando ```docker-compose```