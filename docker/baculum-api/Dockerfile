FROM eftechcombr/bacula:15.0.2-director

RUN curl https://www.bacula.org/downloads/baculum/baculum.pub | apt-key add -

COPY baculum.list /etc/apt/sources.list.d/baculum.list

RUN apt update && \
  apt -y install \
  php-bcmath \
	php*-mbstring \
	php-fpm \
	baculum-common \
	bacula-console \
  baculum-api \
	baculum-api-apache2 \
	supervisor 

RUN curl -OL https://gitlab.bacula.org/bacula-community-edition/bacula-community/-/archive/Branch-15.0/bacula-community-Branch-15.0.tar.gz \
  && tar zxf bacula-community-Branch-15.0.tar.gz \
  && cd bacula-community-Branch-15.0/gui/baculum/ \
  && cp -Rf index.php assets protected themes /usr/share/baculum/htdocs/ || echo ok 

COPY sudoers-baculum /etc/sudoers.d/sudoers-baculum 

RUN usermod -aG bacula www-data && \
  chown -R www-data:bacula /opt/bacula/working /opt/bacula/etc && \
  chmod -R g+rwx /opt/bacula/working /opt/bacula/etc && \
  a2enmod rewrite && \
  a2ensite baculum-api

COPY timezone.ini /etc/php.d/timezone.ini

COPY confs/supervisord.conf /etc/supervisord.conf

VOLUME ["/opt/bacula/etc","/etc/baculum"]

EXPOSE 9096/tcp

RUN mkdir -p /run/php

ENTRYPOINT ["/usr/bin/supervisord"]

# CMD ["/usr/bin/supervisord"]
# CMD ["sleep", "50000"]
