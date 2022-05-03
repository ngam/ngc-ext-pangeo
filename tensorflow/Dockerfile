FROM nvcr.io/nvidia/tensorflow:22.04-tf2-py3

# Install tree? git and vim already present
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree && \
    rm -rf /var/lib/apt/lists/

# tensorflow+jax ecosystem
COPY tensorflow/requirements.txt /tmp/pip-tmp/

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install jax[cuda11_cudnn82] \
        -f https://storage.googleapis.com/jax-releases/jax_releases.html

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/requirements.txt \
	&& rm -rf /tmp/pip-tmp

# common requirements
COPY requirements.txt /tmp/pip-tmp/

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/requirements.txt \
	&& rm -rf /tmp/pip-tmp
