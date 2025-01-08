# Base image
FROM registry.access.redhat.com/ubi9/ubi:latest

LABEL maintainer="Openshift LightSpeed Performance And Scale"

# Install necessary tools without removing system-protected packages
RUN dnf install -y \
        dnf-plugins-core \
        git \
        make \
        jq \
        tar \
        skopeo \
        findutils \
        podman \
        python3-pip \
        gcc \
        go && \
    dnf clean all

# Set GO environment variables (to ensure it's set correctly)
ENV GOPATH=/root/go
ENV GOROOT=/usr/lib/golang
ENV PATH=$GOROOT/bin:$GOPATH/bin:$PATH

# Install kubectl
RUN curl -sSL https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable/openshift-client-linux-amd64-rhel8.tar.gz | tar -xvzf -  &&\
    mv kubectl /usr/bin && \
    chmod +x /usr/bin/kubectl && \
    rm -rf openshift-client-linux-amd64-rhel8.tar.gz

# Install yq
RUN curl -sLO https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 && \
    chmod +x yq_linux_amd64 && \
    mv yq_linux_amd64 /usr/bin/yq

# Install kustomize
RUN curl -sLO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv5.5.0/kustomize_v5.5.0_linux_amd64.tar.gz && \
    tar -xvzf kustomize_v5.5.0_linux_amd64.tar.gz && \
    mv kustomize /usr/bin/ && \
    chmod +x /usr/bin/kustomize && \
    rm -rf kustomize_v5.5.0_linux_amd64.tar.gz
