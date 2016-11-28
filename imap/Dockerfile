#FROM ubuntu:16.10
FROM armv7/armhf-ubuntu:16.10
MAINTAINER Heiko Hüter <ender@ender74.de>

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -y dovecot-core dovecot-imapd \
      dovecot-sieve dovecot-managesieved dovecot-antispam \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* /root/.cache /tmp/* \
    && echo "fs.inotify.max_user_watches=1048576" >> /etc/sysctl.conf \
    && mkdir /var/cache/Maildir

RUN useradd -ms /bin/bash ender \
      &&  echo "ender:1234"  | chpasswd

COPY conf.d/* /etc/dovecot/conf.d/
VOLUME ["/var/cache/Maildir/"]
EXPOSE 143 993

ENTRYPOINT ["dovecot"]
CMD ["-F", "-c", "/etc/dovecot/dovecot.conf"]
