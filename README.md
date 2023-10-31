# docker_images

Docker Images, feel free to use

## To upload a new one

docker build --tag dana23747/azure-devops-linux-agent:latest . && docker push dana23747/azure-devops-linux-agent:latest


docker build --platform linux/amd64 -t dana23747/ubuntu-admintools:1.0.0 .
docker tag dana23747/ubuntu-admintools:1.0.0 dana23747/ubuntu-admintools:latest
docker push dana23747/ubuntu-admintools:1.0.0
docker push dana23747/ubuntu-admintools:latest

docker run --name nettools --rm -i -t dana23747/ubuntu-admintools:latest zsh
