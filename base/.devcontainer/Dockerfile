FROM janhurst/devcontainer:tools

ARG APT_MIRROR="au.archive"
RUN sudo sed -i -e "s/http:\/\/archive/http:\/\/$APT_MIRROR/" /etc/apt/sources.list

# ensure the conda path is available to root/su
RUN chmod 0640 /etc/sudoers && \
    sed -i "s/sbin:\/bin/sbin:\/bin:\/opt\/conda\/bin/g" /etc/sudoers && \
    chmod 0440 /etc/sudoers

# build-essential and other useful development and build tools
ARG DEV_PACKAGES="git git-lfs curl yarn zsh"
RUN apt-get update && apt-get install --no-install-recommends -yq software-properties-common \
    && apt-get install -yq --no-install-recommends ${DEV_PACKAGES} \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# install some common python packages in the base environment
COPY environment.yml /tmp/environment.yml
RUN mamba env update -n base -f /tmp/environment.yml \
    && rm /tmp/environment.yml

# add git azure devops authentication settings and download and install Azure DevOps Credential provider
RUN curl -sL https://raw.githubusercontent.com/microsoft/artifacts-credprovider/master/helpers/installcredprovider.sh | bash -
USER vscode
RUN git config --global credential.useHttpPath true
USER root

# Download and install the Azure Artifacts credential provider
RUN wget -qO- https://aka.ms/install-artifacts-credprovider.sh | bash

# add autoreloading configuration for IPython
USER vscode
RUN ipython profile create
RUN echo "c.InteractiveShellApp.exec_lines = ['%load_ext autoreload', '%autoreload 2']" >> /home/vscode/.ipython/profile_default/ipython_config.py
USER root
