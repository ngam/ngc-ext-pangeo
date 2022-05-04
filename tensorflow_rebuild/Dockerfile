FROM nvcr.io/nvidia/tensorflow:22.04-tf2-py3

# COPY custom.patch /tmp

WORKDIR /opt/tensorflow

# RUN patch -p1 < /tmp/custom.patch

RUN ./nvbuild.sh

WORKDIR /workspace
