FROM gipert/archlinux-base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm ghostscript zathura texlive-most asymptote

ENV ASYMPTOTE_PDFVIEWER="zathura"

CMD zsh
