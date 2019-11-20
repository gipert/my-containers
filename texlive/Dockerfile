FROM gipert/archlinux-base:latest

USER root

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm texlive-most

CMD zsh
