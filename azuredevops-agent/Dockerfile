FROM --platform=linux/amd64 bitnami/kubectl:latest as kubectl
FROM --platform=linux/amd64 ubuntu:20.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -qq --no-install-recommends \
    apt-transport-https \
    apt-utils \
    ca-certificates \
    curl \
    git \
    iputils-ping \
    jq \
    lsb-release \
    software-properties-common \
    libicu66 \
    python \
    python3-pip

RUN  pip3 install ansible
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash
COPY --from=kubectl /opt/bitnami/kubectl/bin/kubectl /usr/local/bin/

# Can be 'linux-x64', 'linux-arm64', 'linux-arm', 'rhel.6-x64'.
ENV TARGETARCH=linux-x64

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

ENTRYPOINT [ "./start.sh" ]