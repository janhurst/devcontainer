FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu-22.04

# install graphviz
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y graphviz pandoc && rm -rf /var/lib/apt/lists/*

# add autoreloading configuration for IPython
RUN mkdir -p /home/vscode/.ipython/profile_default && \
    chown -R vscode:vscode /home/vscode/.ipython && \
    echo "c.InteractiveShellApp.exec_lines = ['%load_ext autoreload', '%autoreload 2']" >> /home/vscode/.ipython/profile_default/ipython_config.py

# create some directories and fix their permissions
RUN mkdir -p /home/vscode/.cache && chown vscode:vscode /home/vscode/.cache \
    && mkdir -p /home/vscode/.local && chown vscode:vscode /home/vscode/.local \
    && mkdir -p /home/vscode/.config && chown vscode:vscode /home/vscode/.config

# VS Code overrides ENTRYPOINT and CMD when executing `docker run` by default.
# Setting the ENTRYPOINT to docker-init.sh will configure non-root access to
# the Docker socket if "overrideCommand": false is set in devcontainer.json.
# The script will also execute CMD if you need to alter startup behaviors.
ENTRYPOINT [ "/usr/local/share/docker-init.sh" ]
CMD ["sleep", "infinity"]
