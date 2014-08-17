FROM debian:testing
MAINTAINER Juien Furgerot <julien.furgerot@gmail.com>

RUN echo "deb http://debian.mirrors.ovh.net/debian/ testing main" > /etc/apt/sources.list

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y apt-utils
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y postgresql-9.3-pgrouting phppgadmin 
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git make gcc libpq-dev

RUN echo "local all all md5" > /etc/postgresql/9.3/main/pg_hba.conf
RUN echo "host all all 0.0.0.0/0 md5" >> /etc/postgresql/9.3/main/pg_hba.conf

RUN service postgresql start && \
    su postgres -c "psql -c \"create user docker with password 'docker';\"" && \
    su postgres -c "psql -c \"create database comtimes owner docker;\"" && \
    su postgres -c "psql -d comtimes -c \"create extension postgis;\"" && \
    su postgres -c "psql -d comtimes -c \"create extension pgrouting;\"" && \
    service postgresql stop


RUN sed -i.bak '/^allow/d;s/# allow/allow/' /etc/apache2/conf.d/phppgadmin
RUN ln -s /etc/apache2/conf.d/phppgadmin /etc/apache2/conf-enabled/phppgadmin.conf

ADD data/ /data
WORKDIR /data
RUN git clone https://github.com/justjkk/gtfs2pgrouting.git
RUN cd gtfs2pgrouting/Release && make

RUN service postgresql start && \
	cd gtfs2pgrouting && \
	./Release/gtfs2pgrouting -d comtimes -u docker -p docker /data/gtfs-transilien/ && \
	service postgresql stop

# FOR BUILD ONLY
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y vim

EXPOSE 5432
EXPOSE 80

CMD ["/bin/bash"]
