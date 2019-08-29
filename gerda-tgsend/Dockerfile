FROM archlinux/base:latest

USER root

COPY telegram-send.conf /etc/telegram-send.conf
COPY gerda-notifier /bin/gerda-notifier

RUN pacman -Syu --noconfirm \
 && pacman -S --noconfirm zsh vim htop python-pip \
 && pip install telegram-send

CMD zsh
