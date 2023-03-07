FROM mcr.microsoft.com/devcontainers/miniconda:3

# ARG APT_MIRROR="au.archive"
# RUN sudo sed -i -e "s/http:\/\/archive/http:\/\/$APT_MIRROR/" /etc/apt/sources.list

# ensure the conda path is available to root/su
RUN chmod 0640 /etc/sudoers && \
    sed -i "s/sbin:\/bin/sbin:\/bin:\/opt\/conda\/bin/g" /etc/sudoers && \
    chmod 0440 /etc/sudoers

# install some common python packages in the base environment
RUN conda install -c conda-forge mamba \
    && conda clean -afy
COPY environment.yml /tmp/environment.yml
RUN mamba env update -n base -f /tmp/environment.yml \
    && mamba clean -afy \
    && rm /tmp/environment.yml

# add configuration to allow Azure Devops to authenticate http based git repo URLs
USER vscode
RUN git config --global credential.useHttpPath true
USER root

# add autoreloading configuration for IPython
RUN mkdir -p /home/vscode/.ipython/profile_default && \
    chown -R vscode:vscode /home/vscode/.ipython && \
    echo "c.InteractiveShellApp.exec_lines = ['%load_ext autoreload', '%autoreload 2']" >> /home/vscode/.ipython/profile_default/ipython_config.py

# configure conda
USER vscode
RUN conda init bash
RUN mamba init bash
USER root

# VS Code overrides ENTRYPOINT and CMD when executing `docker run` by default.
# Setting the ENTRYPOINT to docker-init.sh will configure non-root access to
# the Docker socket if "overrideCommand": false is set in devcontainer.json.
# The script will also execute CMD if you need to alter startup behaviors.
ENTRYPOINT [ "/usr/local/share/docker-init.sh" ]
VOLUME [ "/var/lib/docker" ]
CMD ["sleep", "infinity"]