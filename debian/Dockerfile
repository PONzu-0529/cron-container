FROM debian

# define
ARG USERNAME
ARG USER_UID=1000

# install and main setup
RUN apt -y update && \
    apt -y upgrade && \
    apt -y install vim sudo tzdata git cron

# add user
RUN useradd --uid ${USER_UID} --create-home --shell /bin/bash -G sudo,root ${USERNAME} && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# setting setup.sh
COPY setup.sh /var/setup.sh
RUN chmod 700 /var/setup.sh && \
    chown ${USERNAME}:${USERNAME} /var/setup.sh

# Setting Cron
COPY crontab /var/spool/cron/crontabs/root
RUN crontab /var/spool/cron/crontabs/root

CMD sh /var/setup.sh && /bin/sh