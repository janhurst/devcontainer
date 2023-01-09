FROM janhurst/devcontainer:base

# install torch first, change less frequently and quite large downloads
RUN pip3 install --disable-pip-version-check --no-cache-dir torch \
    && rm -rf /tmp/pip-tmp

# install python (note updated later via dev container python feature)
ARG PYTHON_PACKAGES="dvc fastapi plotly dash dash-bootstrap-components dash_cytoscape flask_caching joblib uvicorn pandas numpy adal"
RUN pip3 install --disable-pip-version-check --no-cache-dir ${PYTHON_PACKAGES} \
    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1