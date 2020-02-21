FROM tomcat:7.0-jre8

MAINTAINER Dirk Stenger <stenger@lat-lon.de>
MAINTAINER Torsten Friebe <friebe@lat-lon.de>

# add common libs
ADD teamengine-web-*-common-libs.zip /root/
RUN cd /root/ && unzip -q teamengine-web-*-common-libs.zip -d /usr/local/tomcat/lib

# add TEAM engine console
ADD teamengine-console-*-base.zip /root/
RUN cd /root/ && unzip -q teamengine-console-*-base.zip -d /root/te_base
ADD teamengine-console-*-bin.zip /root/
RUN cd /root/ && unzip -o -q teamengine-console-*-bin.zip -d /root/te_base

# set TE_BASE
ENV JAVA_OPTS="-Xms1024m -Xmx2048m -DTE_BASE=/root/te_base -Djava.awt.headless=true"

ADD ets-*-ctl.zip /root/
RUN cd /root/ && for file in ets-*-ctl.zip; do unzip -q $file -d /root/te_base/scripts; done

ADD ets-*-deps.zip /root/
RUN cd /root/ && for file in ets-*-deps.zip; do unzip -q -o $file -d /root/te_base/resources/lib; done

RUN mkdir /root/te_base/forms
ADD wms.xml /root/te_base/forms

CMD cd /root/te_base/bin/unix && ./test.sh -source=/root/te_base/scripts/wms/1.3.0/ctl/main.xml -form=/root/te_base/forms/wms.xml && ./viewlog.sh  -logdir=/root/te_base/users/root -session=s0001