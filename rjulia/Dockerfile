FROM gipert/root-cern:latest

USER root

RUN yum-config-manager --add-repo https://copr.fedorainfracloud.org/coprs/nalimilan/julia/repo/epel-7/nalimilan-julia-epel-7.repo && \
    yum install -y libedit-devel julia

ENV JULIA_CXX_RTTI 1

RUN julia -e 'Pkg.add("Cxx")' && \
    julia -e 'Pkg.build("Cxx")'

RUN julia -e 'Pkg.add("ROOT")' && \
    julia -e 'Pkg.build("ROOT")'

CMD julia
