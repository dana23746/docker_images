# syntax=docker/dockerfile:1

FROM debian:bookworm-slim

ARG USERNAME=dana

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    dnsutils \
    git \
    gnupg \
    iputils-ping \
    net-tools \
    openssh-client \
    sudo \
    telnet \
    vim \
    wget \
    zsh \
    gzip \
    traceroute \
    nmap \
    netcat-openbsd \
    tcpdump \
    software-properties-common \
    unzip \
    lsb-release \
    jq \
    htop \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Create user and add to sudoers
RUN useradd -m -s /bin/bash $USERNAME && \
    usermod -aG sudo $USERNAME && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Terraform
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor > /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" > /etc/apt/sources.list.d/hashicorp.list && \
    apt-get update && apt-get install -y terraform && \
    rm -rf /var/lib/apt/lists/*

# Install kubectl
# Set kubectl version explicitly
RUN curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
RUN sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
RUN echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
RUN sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list
RUN sudo apt-get update
RUN sudo apt-get install -y kubectl


# Install oc CLI
RUN curl -LO https://mirror.openshift.com/pub/openshift-v4/clients/oc/latest/linux/oc.tar.gz && \
    tar -xvf oc.tar.gz && mv oc /usr/local/bin/oc && chmod +x /usr/local/bin/oc && \
    rm -f oc.tar.gz README.md

# Switch to user
USER $USERNAME
WORKDIR /home/$USERNAME

# Aliases and shortcuts
RUN echo "\
alias ll='ls -alF'\n\
alias la='ls -A'\n\
alias l='ls -CF'\n\
alias tfi='terraform init'\n\
alias tfa='terraform apply'\n\
alias tfp='terraform plan'\n\
alias tfm='terraform fmt'\n\
alias tfv='terraform validate'\n\
alias tfd='terraform destroy'\n\
alias k='kubectl'\n\
alias gits='git status'\n\
alias gitp='git pull'\n\
alias gitb='f() { git branch \$1 && git checkout \$1; }; f'\n\
alias gitc='f() { git add . && git commit -m \"\$1\" && git push; }; f'\n\
" >> ~/.bashrc

CMD ["/bin/bash"]
