FROM gipert/root-cern:latest

USER root

WORKDIR /scif
RUN mkdir -p /scif/bat/src && \
    wget -q -O- https://github.com/bat/bat/releases/download/v1.0.0/BAT-1.0.0.tar.gz \
    | tar --strip-components 1 -xz -C "/scif/bat/src" && \
    cd /scif/bat/src && ./configure --with-cuba=download --enable-parallel --prefix=/scif/bat && \
    make -j"$(nproc)" && make install

ENV PATH="$PATH:/scif/bat/bin" \
    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib64:/scif/bat/lib"

WORKDIR /data
CMD /bin/bash
