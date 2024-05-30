FROM debian:12

ENV BACULA_VERSION 15.0.2
ENV DISTRO bookworm
ENV DEBIAN_FRONTEND noninteractive
ENV EMAIL suporte@eftech.com.br

# get your key on: https://www.bacula.org/bacula-binary-package-download/
ENV BACULA_KEY 5cee4d079821e

RUN   apt-get install apt-transport-https && \
  apt-get update && \
  apt-get -y install gnupg2 curl dbconfig-common && \
  curl https://bacula.org/downloads/Bacula-4096-Distribution-Verification-key.asc | apt-key add - && \
  echo "deb https://www.bacula.org/packages/${BACULA_KEY}/debs/${BACULA_VERSION} ${DISTRO} main" > /etc/apt/sources.list.d/bacula-community.list && \
  apt-get update
  
# RUN apt-get -y install bacula-postgresql
# RUN for i in `ls /opt/bacula/bin`; do if [ ! -z /usr/sbin/$i ]; then ln -s /opt/bacula/bin/$i /usr/sbin/$i; fi; done 

