# docker_images

Few docker images usefull for my daily work. 

## List 

- ubuntu net tools ( deprecated ) > debug-container:1.0.0

## Maual uplaod :

```bash
docker build --tag dana23747/azure-devops-linux-agent:latest . && docker push dana23747/azure-devops-linux-agent:latest

# If build from mac : 
docker build --platform linux/amd64 -t dana23747/ubuntu-admintools:latest .

docker tag dana23747/ubuntu-admintools:1.0.0 dana23747/ubuntu-admintools:latest
docker push dana23747/ubuntu-admintools:1.0.0
docker push dana23747/ubuntu-admintools:latest

docker run --name nettools --rm -i -t dana23747/ubuntu-admintools:latest zsh
```