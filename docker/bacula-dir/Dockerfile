FROM eftechcombr/bacula:15.0.2-base

RUN apt-get -y install bacula-postgresql \
  && for i in `ls /opt/bacula/bin`; do if [ ! -z /usr/sbin/$i ]; then ln -s /opt/bacula/bin/$i /usr/sbin/$i; fi; done 

VOLUME ["/opt/bacula/etc"]

EXPOSE 9101/tcp

ENTRYPOINT ["/opt/bacula/bin/bacula-dir"]

CMD ["-f", "-c", "/opt/bacula/etc/bacula-dir.conf"]
