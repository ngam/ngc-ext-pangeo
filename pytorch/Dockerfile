FROM nvcr.io/nvidia/pytorch:22.04-py3

# Install tree? git and vim already present
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree gh git-lfs && \
    rm -rf /var/lib/apt/lists/

# torch ecosystem
COPY pytorch/requirements.txt /tmp/pip-tmp/

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install dgl-cu113 \
        -f https://data.dgl.ai/wheels/repo.html

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/requirements.txt \
	&& rm -rf /tmp/pip-tmp

# common requirements
COPY requirements.txt /tmp/pip-tmp/

RUN python -m pip --disable-pip-version-check --no-cache-dir \
	    install -r /tmp/pip-tmp/requirements.txt \
	&& rm -rf /tmp/pip-tmp
