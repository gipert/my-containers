FROM archlinux/base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm zsh vim htop texlive-most

CMD zsh
