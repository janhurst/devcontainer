FROM mcr.microsoft.com/devcontainers/base:ubuntu

# install graphviz
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y graphviz pandoc && rm -rf /var/lib/apt/lists/*

# add configuration to allow Azure Devops to authenticate http based git repo URLs
USER vscode
RUN git config --global credential.useHttpPath true
USER root

# add autoreloading configuration for IPython
RUN mkdir -p /home/vscode/.ipython/profile_default && \
    chown -R vscode:vscode /home/vscode/.ipython && \
    echo "c.InteractiveShellApp.exec_lines = ['%load_ext autoreload', '%autoreload 2']" >> /home/vscode/.ipython/profile_default/ipython_config.py

# install azcopy
RUN wget https://aka.ms/downloadazcopy-v10-linux -O - | tar -xzvf - \
    && sudo cp azcopy_linux_amd64*/azcopy /usr/bin/azcopy \
    && sudo chmod 755 /usr/bin/azcopy

# create some directories and fix their permissions
RUN mkdir -p /home/vscode/.cache && chown vscode:vscode /home/vscode/.cache \
    && mkdir -p /home/vscode/.local && chown vscode:vscode /home/vscode/.local \
    && mkdir -p /home/vscode/.config && chown vscode:vscode /home/vscode/.config

# VS Code overrides ENTRYPOINT and CMD when executing `docker run` by default.
# Setting the ENTRYPOINT to docker-init.sh will configure non-root access to
# the Docker socket if "overrideCommand": false is set in devcontainer.json.
# The script will also execute CMD if you need to alter startup behaviors.
ENTRYPOINT [ "/usr/local/share/docker-init.sh" ]
VOLUME [ "/var/lib/docker" ]
CMD ["sleep", "infinity"]
