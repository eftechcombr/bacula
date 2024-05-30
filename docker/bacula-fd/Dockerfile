FROM eftechcombr/bacula:15.0.2-base

RUN apt-get -y install bacula-common bacula-client

VOLUME ["/opt/bacula/etc"]

EXPOSE 9102/tcp

ENTRYPOINT ["/opt/bacula/bin/bacula-fd"]

CMD ["-f", "-c", "/opt/bacula/etc/bacula-fd.conf"]
