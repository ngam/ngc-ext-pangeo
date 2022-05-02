#
# This example Dockerfile illustrates a method to install
# additional packages on top of NVIDIA's TensorFlow container image.
#
# To use this Dockerfile, use the `docker build` command.
# See https://docs.docker.com/engine/reference/builder/
# for more information.
#
FROM nvcr.io/nvidia/tensorflow:22.04-tf2-py3

# Install tree
# git and vim already present
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree && \
    rm -rf /var/lib/apt/lists/

RUN python -m pip \
	--disable-pip-version-check \
	--no-cache-dir \
	install --upgrade pip
COPY tensorflow/requirements.txt /tmp/pip-tmp/
RUN python -m pip \
	--disable-pip-version-check \
	--no-cache-dir \
	 install -r /tmp/pip-tmp/requirements.txt \
	&& rm -rf /tmp/pip-tmp
