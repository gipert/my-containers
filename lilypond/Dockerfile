FROM gipert/archlinux-base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm ghostscript lilypond

COPY lilyfonts.tar.xz /root/lilyfonts.tar.xz

RUN tar -xvf /root/lilyfonts.tar.xz -C /usr/share/lilypond/* && \
    rm /root/lilyfonts.tar.xz

CMD zsh
