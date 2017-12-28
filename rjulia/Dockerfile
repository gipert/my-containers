FROM gipert/root-cern:latest

USER root

RUN yum install -y -q libedit-devel http-parser ncurses-devel \
                      llvm3.9-libs openlibm utf8proc-devel libgit2-devel\
                      pcre2 tbb openssl-devel && \
    yum -q clean all

RUN mkdir -p /scif/julia && \
    wget -O- -q https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.2-linux-x86_64.tar.gz \
    | tar --strip-components=1 -x -z -f - -C "/scif/julia"

ENV PATH="$PATH:/scif/julia/bin" \
    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/scif/julia/lib" \
    MANPATH="$MANPATH:/scif/julia/share/man" \
    JULIA_CXX_RTTI="1"

RUN julia -e 'Pkg.clone("Cxx")' && \
    cd /root/.julia/v0.6/Cxx && git checkout tags/v0.2.0 && \
    wget -O- -q https://baltig.infn.it/gerda/baseos-binaries/raw/master/llvm-3.9.1-centos7.tar.gz \
    | tar --strip-components=1 -x -z -f - -C "/root/.julia/v0.6/Cxx/deps" && \
    julia -e 'Pkg.add("Compat")' && \
    julia -e 'Pkg.build("Cxx")'

RUN julia -e 'Pkg.add("ROOT")'

WORKDIR /data
CMD /root/.julia/v0.6/ROOT/deps/usr/bin/julia
