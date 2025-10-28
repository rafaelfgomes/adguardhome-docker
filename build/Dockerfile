FROM adguard/adguardhome

ARG UID
ARG GID
ARG TIMEZONE

RUN apk --no-cache update && apk add --no-cache shadow sudo tzdata libcap

RUN groupadd -g ${GID} container && useradd -m -u ${UID} -g container admin

RUN echo "admin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/admin && chmod 0440 /etc/sudoers.d/admin

RUN ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

RUN chown -R admin:container /opt/adguardhome/conf && \
    chown -R admin:container /opt/adguardhome/work && \
    chmod -R 775 /opt/adguardhome/conf && \
    chmod -R 775 /opt/adguardhome/work

RUN setcap 'CAP_NET_BIND_SERVICE=+eip CAP_NET_RAW=+eip' /opt/adguardhome/AdGuardHome

WORKDIR /opt/adguardhome/work

USER admin

ENTRYPOINT ["/opt/adguardhome/AdGuardHome"]

CMD ["--no-check-update", "-c", "/opt/adguardhome/conf/AdGuardHome.yaml", "-w", "/opt/adguardhome/work"]
