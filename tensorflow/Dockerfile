FROM nvcr.io/nvidia/tensorflow:22.04-tf2-py3

# Install tree? git and vim already present
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree gh git-lfs && \
    rm -rf /var/lib/apt/lists/

# Install GEOS:
RUN wget -O /tmp/geos-3.10.2.tar.bz2 http://download.osgeo.org/geos/geos-3.10.2.tar.bz2 \
	&& tar xvfj /tmp/geos-3.10.2.tar.bz2 --directory=/tmp/ \
	&& cd /tmp/geos-3.10.2 \
	&& mkdir _build \
	&& cd _build \
	&& cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. \
	&& make \
	&& ctest \
	&& make install

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
