FROM nvcr.io/nvidia/pytorch:22.04-py3

# Install tree? git and vim already present
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null
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
