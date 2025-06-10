# mk-jupyter docker
It's a jupyter docker repo based on `datascience-jupyter` image, this docker has mutiple kernels of different Python version from 3.8 to 3.10 with **R** and **Julia**, and also removes the default kernel of ipykernel to keep clean from jupyter environment.

## Docker Deploy
[![Deploy with Docker](https://img.shields.io/badge/Deploy%20with-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/r/xhh1128/mk-jupyter)

It is easy to deploy by Docker and the following code

```shell
docker run --rm -p 8888:8888 \
	-e DOCKER_STACKS_JUPYTER_CMD=notebook \
	xhh1128/mk-jupyter:latest
```

and also by `docker-compose.yml` file, you can download the file from this repo and then run

```shell
docker compose up -d
```
then it will run at backend.
