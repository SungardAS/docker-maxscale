FROM centos:7
MAINTAINER kevin.mcgrath@sungardas.com

RUN rpm --import https://yum.mariadb.org/RPM-GPG-KEY-MariaDB

RUN yum install -y mariadb-embedded-devel systemtap-sdt-devel

RUN yum install -y git gcc gcc-c++ ncurses-devel bison glibc-devel cmake libgcc perl make libtool openssl-devel libaio libaio-devel librabbitmq-devel libcurl-devel pcre-devel  systemtap-sdt-devel

RUN git clone https://github.com/mariadb-corporation/MaxScale

RUN cd MaxScale \
    && mkdir build && cd build \
    && cmake .. -DWITH_SCRIPTS=N -DSTATIC_EMBEDDED=FALSE \
    && FLAGS="-Wno-unused-variable -Wno-unused-but-set-variable -Wno-unused-function" make install

RUN yum -y history undo 4 && rm -rf MaxScale

RUN mkdir -p /var/run/maxscale

VOLUME ["/var/log/maxscale/", "/var/lib/maxscale/data/data1", "/var/cache/maxscale/"]

ENTRYPOINT ["maxscale", "-d"]
