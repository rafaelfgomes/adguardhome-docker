FROM adguard/adguardhome

ARG UID
ARG GID
ARG TIMEZONE

RUN apk --no-cache update && apk add --no-cache shadow sudo

RUN groupadd -g ${GID} container && useradd -m -u ${UID} -g container admin

RUN echo "admin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/admin && chmod 0440 /etc/sudoers.d/admin

RUN ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

RUN usermod -aG root admin

WORKDIR /opt/adguardhome/work

USER admin

ENTRYPOINT ["/opt/adguardhome/AdGuardHome"]

CMD ["--no-check-update", "-c", "/opt/adguardhome/conf/AdGuardHome.yaml", "-w", "/opt/adguardhome/work"]
