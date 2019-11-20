FROM archlinux/base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm coreutils tar less findutils diffutils grep sed gawk

CMD zsh
