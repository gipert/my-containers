FROM gipert/archlinux-base:latest

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm texlive-most

COPY asymptote.PKGBUILD /opt/src/PKGBUILD

RUN cd /opt/src && source ./PKGBUILD && \
    pacman -S --noconfirm --needed --asdeps \
      "${makedepends[@]}" "${depends[@]}" wget base-devel && \
    prepare && build && check && package

CMD zsh
