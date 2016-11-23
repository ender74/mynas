FROM ubuntu:16.10
MAINTAINER Heiko Hüter <ender@ender74.de>

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -y minidlna \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* /root/.cache /tmp/* \
    && echo "fs.inotify.max_user_watches=1048576" >> /etc/sysctl.conf

COPY minidlna.conf /etc/

EXPOSE 1900/udp 8200

ENTRYPOINT ["minidlnad"]
CMD ["-R", "-d", "-f", "/etc/minidlna.conf"]
