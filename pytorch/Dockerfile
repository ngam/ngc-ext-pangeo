FROM nvcr.io/nvidia/pytorch:22.04-py3

# Install tree? git and vim already present
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get update && apt-get install -y --no-install-recommends \
        tree gh git-lfs sqlite3 libsqlite3-dev libtiff-dev && \
    rm -rf /var/lib/apt/lists/

# install geos
RUN wget -O /tmp/geos-3.10.2.tar.bz2 http://download.osgeo.org/geos/geos-3.10.2.tar.bz2 \
	&& tar xvfj /tmp/geos-3.10.2.tar.bz2 --directory=/tmp/ \
	&& cd /tmp/geos-3.10.2 \
	&& mkdir _build \
	&& cd _build \
	&& cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. \
	&& make \
	&& ctest \
	&& make install
	
# install PROJ
RUN wget -O /tmp/proj-8.2.1.tar.gz https://download.osgeo.org/proj/proj-8.2.1.tar.gz \
	&& tar xvfz /tmp/proj-8.2.1.tar.gz --directory=/tmp/ \
	&& cd /tmp/proj-8.2.1 \
	&& mkdir _build \
	&& cd _build \
	&& cmake .. \
	&& cmake --build . \
	&& cmake --build . --target install 

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
