FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:20

RUN wget https://github.com/jgm/pandoc/releases/download/3.1.8/pandoc-3.1.8-1-amd64.deb && \
    sudo dpkg -i pandoc-3.1.8-1-amd64.deb && \
    pandoc -v

RUN npm install -g npm@9

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
     && apt-get -y install --no-install-recommends inotify-tools