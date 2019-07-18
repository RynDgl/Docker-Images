FROM base-centos:1.0

ENV PYTHON_VERSION 3.7.4
ENV PATH /opt/python-3.7.4/bin:/opt/python-3.7.4/lib$PATH
ENV LANG C.UTF-8
# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on
# a Linux system *fundamentally breaks Python 3*, and that's not OK.

RUN set -ex \
    && yum install -y \
        gcc \
        make \
        bzip2-devel \
        coreutils \
        expat-devel \
        findutils \
        gdbm-devel  \
        glibc-devel.x86_64 \
        libffi-devel.x86_64 \
        libtirpc-devel.x86_64 \
        ncurses-devel.x86_64 \
        openssl-devel.x86_64 \
        readline-devel.x86_64 \
        sqlite-devel.x86_64 \
        tcl-devel.x86_64 \
        tk-devel.x86_64 \
        xz-devel.x86_64 \
        zlib-devel.x86_64 \
        util-linux.x86_64 \
        pax-utils.x86_64 \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && mkdir -p /opt/python-3.7.4 \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure \
        --enable-optimizations \
        --build="$gnuArch" \
        --enable-loadable-sqlite-extensions \
        --enable-shared \
        --with-system-expat \
        --with-system-ffi \
        --without-ensurepip \
        --prefix=/opt/python-3.7.4 \
    && make -j 24 EXTRA_CFLAGS="-DTHREAD_STACK_SIZE=0x100000" \
    && make install \
    && rm -rf /usr/src/python \
    && ln -s /opt/python-3.7.4/lib/libpython3.7m.so /lib64/libpython3.7m.so.1.0

RUN cd /opt/python-3.7.4 \
    && wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
        python3.7 get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        pip==19.1.1 \
    && rm get-pip.py \
    && pip3 install virtualenv

CMD ["/bin/bash"]