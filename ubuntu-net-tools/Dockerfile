# syntax=docker/dockerfile:1

FROM ubuntu:latest

# Set Username
ARG USERNAME=dana

# Execute commands as root
USER root

# Update and install dependencies
RUN apt update && apt upgrade -y && \
    apt install -y \
        apt-file \
        apt-transport-https \
        ca-certificates \
        curl \
        dnsutils \
        gpg \
        git \
        gnupg \
        iputils-ping \
        net-tools \
        software-properties-common \
        ssh \
        sudo \
        tar \
        telnet \
        vim \
        wget \
        zsh \
        gzip && \
    apt-file update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Create non-root user and add to sudoers
RUN useradd -m -s /bin/bash $USERNAME && \
    usermod -aG sudo $USERNAME && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Terraform
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor > /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" > /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Kubectl
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

# Install oc CLI
RUN curl -LO https://mirror.openshift.com/pub/openshift-v4/clients/oc/latest/linux/oc.tar.gz && \
    tar -xvf oc.tar.gz && \
    mv oc /usr/local/bin/oc && \
    chmod +x /usr/local/bin/oc && \
    rm -f oc.tar.gz README.md

# Switch to new user
USER $USERNAME

# Add aliases
RUN echo "alias ll='ls -all'" >> /home/$USERNAME/.bashrc && \
    echo "alias la='ls -A'" >> /home/$USERNAME/.bashrc && \
    echo "alias l='ls -CF'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfi='terraform init'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfa='terraform apply'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfp='terraform plan'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfm='terraform fmt'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfv='terraform validate'" >> /home/$USERNAME/.bashrc && \
    echo "alias tfd='terraform destroy'" >> /home/$USERNAME/.bashrc && \
    echo "alias k='kubectl'" >> /home/$USERNAME/.bashrc && \
    echo "alias gits='git status'" >> /home/$USERNAME/.bashrc && \
    echo "alias gitp='git pull'" >> /home/$USERNAME/.bashrc && \
    echo "alias gitb='f() { git branch \$1 && git checkout \$1; }; f'" >> /home/$USERNAME/.bashrc && \
    echo "alias gitc='f() { git add . && git commit -m \"\$1\" && git push; }; f'" >> /home/$USERNAME/.bashrc

# Set working directory
WORKDIR /home/$USERNAME/

CMD ["/bin/bash"]
