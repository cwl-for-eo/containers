FROM ubuntu:20.04

USER root

SHELL ["/bin/bash", "-c"]

ENV BASH_ENV=~/.bashrc                                          \
    MAMBA_ROOT_PREFIX=/srv/conda                                \
    PATH=/srv/conda/envs/env_snap/bin:/srv/conda/envs/env_snap/snap/bin:$PATH 

RUN apt update && \
    apt-get install -y jq libxml2-utils

ADD environment.yml /tmp/environment.yml

# Install basic commands and mamba
RUN apt-get update && \
    apt-get install -y ca-certificates wget ttf-dejavu file bash bzip2 libgfortran5  && \
    wget -qO- https://micromamba.snakepit.net/api/micromamba/linux-64/latest | tar -xvj bin/micromamba --strip-components=1 && \
    ./micromamba shell init -s bash -p ~/micromamba  && \
    apt-get clean autoremove --yes  && \
    rm -rf /var/lib/{apt,dpkg,cache,log}  && \
    cp ./micromamba /usr/bin  && \
    micromamba create -f /tmp/environment.yml && \
    rm -fr /srv/conda/pkgs                                                                                                  && \
    rm -fr /tmp/*


