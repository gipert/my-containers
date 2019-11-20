FROM archlinux/base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S coreutils tar less findutils diffutils grep sed gawk \
 && pacman -S --noconfirm zsh vim htop texlive-most

CMD zsh
