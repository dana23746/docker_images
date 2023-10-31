# syntax=docker/dockerfile:1

FROM ubuntu:latest 

#Set Username : 
ARG USERNAME=dana

#exceute next command as root : 
USER root

RUN apt update
RUN apt upgrade -y
RUN apt install -y apt-file apt-transport-https
RUN apt-file update
RUN apt install -y curl net-tools dnsutils iputils-ping ssh telnet wget sudo gpg git apt-transport-https zsh vim

#Set user non root 
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

## Azure Cli 
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

## Install Terraform 
RUN wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
RUN apt update && sudo apt install -y terraform

## INstall Kubectl 
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/bin

## Clean Up 
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Switch to user name to set up user context.
USER $USERNAME

# Set up zsh
COPY sources/.zshrc /home/$USERNAME/.zshrc 

WORKDIR /home/$USERNAME/
