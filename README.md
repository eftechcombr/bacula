# Bacula 15.0.2 Container

[![Build Baculum](https://github.com/eftechcombr/bacula/actions/workflows/baculum-build-and-publish.yml/badge.svg)](https://github.com/eftechcombr/bacula/actions/workflows/baculum-build-and-publish.yml) [![Build Bacula](https://github.com/eftechcombr/bacula/actions/workflows/bacula-build-and-publish.yml/badge.svg)](https://github.com/eftechcombr/bacula/actions/workflows/bacula-build-and-publish.yml)

Deploy the bacula community edition on Docker Containers. 

## Images

- [x] Bacula Catalog                    eftechcombr/bacula:15.0.2-catalog
- [x] Bacula Director                   eftechcombr/bacula:15.0.2-director
- [x] Bacula Storage Daemon             eftechcombr/bacula:15.0.2-storage
- [x] Bacula File Daemon                eftechcombr/bacula:15.0.2-client
- [x] Baculum Web Gui                   eftechcombr/baculum:15.0.2-web
- [x] Baculum API                       eftechcombr/baculum:15.0.2-api

## Install Docker 

    curl -sSL https://get.docker.com | bash
    
## Install Docker-compose

    curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

## Set permission on etc/baculum 

    chmod -R a+rwx etc/baculum
    

## Download and Install Bacula Container

    git clone https://github.com/eftechcombr/bacula
    cd bacula/docker
    docker-compose up

## Tests

    docker exec -it docker_bacula-dir_1 bash
    > bconsole
    * 
    
    
## Video

[![asciicast](https://asciinema.org/a/A4skWxuqhgqtIscjkCTl2snc0.svg)](https://asciinema.org/a/A4skWxuqhgqtIscjkCTl2snc0)


## Docker Compose

docker-compose.yaml


    version: '3.1'
    services:
      db:
        image: eftechcombr/bacula:15.0.2-catalog
        restart: unless-stopped
        environment:
          POSTGRES_PASSWORD: bacula
          POSTGRES_USER: bacula
          POSTGRES_DB: bacula
        volumes:
        - pgdata:/var/lib/postgresql/data:rw
        ports:
          - 5432
      bacula-dir:
        image: eftechcombr/bacula:15.0.2-director
        restart: unless-stopped
        volumes:
          - ./etc/bacula-dir.conf:/opt/bacula/etc/bacula-dir.conf:ro
          - ./etc/bconsole.conf:/opt/bacula/etc/bconsole.conf:ro
        depends_on:
          - db
        ports:
          - 9101
      bacula-sd:
        image: eftechcombr/bacula:15.0.2-storage
        restart: unless-stopped
        depends_on:
          - bacula-dir
          - db
        volumes:
          - ./etc/bacula-sd.conf:/opt/bacula/etc/bacula-sd.conf:ro
        ports:
          - 9103
      bacula-fd:
        image: eftechcombr/bacula:15.0.2-client
        restart: unless-stopped
        depends_on:
          - bacula-sd
          - bacula-dir
        volumes:
          - ./etc/bacula-fd.conf:/opt/bacula/etc/bacula-fd.conf:ro
        ports:
          - 9102
    volumes:
      pgdata:

## Support

For technical support please contact us. 

suporte@eftech.com.br

## e-Learning 

https://www.eftech.com.br


## Reference

http://www.bacula.lat/community/baculum/ 

http://www.bacula.lat/community/script-instalacao-bacula-community-9-x-pacotes-oficiais/

https://www.bacula.org/documentation/documentation/
