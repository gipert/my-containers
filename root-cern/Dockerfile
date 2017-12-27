FROM gipert/centos-base:latest

USER root
WORKDIR /tmp

RUN yum install -y xorg-x11-fonts-Type1 fftw-devel libXmu-devel \
                   libXi-devel libX11-devel libXext-devel \
                   libXft-devel libXpm-devel libzip-devel \
                   mesa-libGLU-devel gsl-devel python-devel graphviz-devel \
                   libjpeg-devel libpng-devel giflib-devel libtiff-devel \ 
                   libxml2-devel openssl-devel fttw-devel && \
    yum -q clean all && \

RUN mkdir -p /tmp/src /tmp/build /scif/root && \
   wget -O- -q https://root.cern.ch/download/root_v6.10.08.source.tar.gz \
   | tar --strip-components 1 -xz -C "/tmp/src"

WORKDIR /tmp/build
RUN cmake -DCMAKE_INSTALL_PREFIX="/scif/root" \
          -Dx11=ON \
          -Dunuran=ON \
          -Dtable=ON \
          -Droofit=ON \
          -Dminuit2=ON \
          -Dhttp=ON \
          -Dgdml=ON \
          -Dfail-on-missing=ON \
          /tmp/src && \
    cmake --build . - --j"$(nproc)" && \
    make install

ENV ROOTSYS         "/scif/root" \
    PATH            "$ROOTSYS/bin:$PATH" \
    LD_LIBRARY_PATH "$ROOTSYS/lib:$LD_LIBRARY_PATH" \
    MANPATH         "$ROOTSYS/man:$MANPATH" \
    PYTHONPATH      "$ROOTSYS/lib:$PYTHONPATH"

WORKDIR /data
CMD /scif/root/bin/root
