FROM janhurst/devcontainer:ml

# install torch first, change less frequently and quite large downloads
RUN pip3 install --disable-pip-version-check --no-cache-dir torch \
    && rm -rf /tmp/pip-tmp

# install frequently changing python packages
ARG PYTHON_PACKAGES="pyarrow"
RUN pip3 install --disable-pip-version-check --no-cache-dir ${PYTHON_PACKAGES} \
    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1