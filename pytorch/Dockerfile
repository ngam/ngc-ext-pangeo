#
# This example Dockerfile illustrates a method to install
# additional packages on top of NVIDIA's TensorFlow container image.
#
# To use this Dockerfile, use the `docker build` command.
# See https://docs.docker.com/engine/reference/builder/
# for more information.
#
FROM nvcr.io/nvidia/pytorch:22.04-py3

# Install tree? git and vim already present
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree && \
    rm -rf /var/lib/apt/lists/

# # get jax cuda
# COPY pytorch/jax_cuda.txt /tmp/pip-tmp/
# RUN python -m pip --disable-pip-version-check --no-cache-dir \
# 	    install -r /tmp/pip-tmp/jax_cuda.txt \
# 	&& rm -rf /tmp/pip-tmp

# # rest of jax ecosystem
# COPY pytorch/jax_ecosystem.txt /tmp/pip-tmp/
# RUN python -m pip --disable-pip-version-check --no-cache-dir \
# 	    install -r /tmp/pip-tmp/jax_ecosystem.txt \
# 	&& rm -rf /tmp/pip-tmp

# pydot and graphviz for viz
COPY pytorch/viz_pkgs.txt /tmp/pip-tmp/
RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/viz_pkgs.txt \
	&& rm -rf /tmp/pip-tmp

# scipy ecosystem
COPY pytorch/sci_reqs.txt /tmp/pip-tmp/
RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/sci_reqs.txt \
	&& rm -rf /tmp/pip-tmp

# # geo ecosystem cont.
# COPY pytorch/geo_reqs.txt /tmp/pip-tmp/
# RUN python -m pip \
# 	--disable-pip-version-check \
# 	--no-cache-dir \
# 	 install -r /tmp/pip-tmp/geo_reqs.txt \
# 	&& rm -rf /tmp/pip-tmp
