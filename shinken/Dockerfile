FROM docker/base
MAINTAINER Arnaud Chong <shine@achamo.net>
RUN sed -i.bak 's/main$/main universe/' /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install curl wget python python-setuptools nagios-plugins-extra pyro supervisor -y
RUN useradd -r shinken
RUN wget http://www.shinken-monitoring.org/pub/shinken-1.4.tar.gz
RUN tar -zxvf shinken-1.4.tar.gz
RUN cd shinken-1.4 && python setup.py install --prefix /usr --install-purelib /usr/lib/python2.7/dist-packages/ --install-layout deb
RUN rm -rf shinken-1.4.tar.gz shinken-1.4

ADD base.conf /etc/supervisor/conf.d/supervisord.conf
ADD shinken-arbiter.conf /etc/supervisor/conf.d/shinken-arbiter.conf
ADD shinken-poller.conf /etc/supervisor/conf.d/shinken-poller.conf
ADD shinken-reactionner.conf /etc/supervisor/conf.d/shinken-reactionner.conf
ADD shinken-broker.conf /etc/supervisor/conf.d/shinken-broker.conf
ADD shinken-receiver.conf /etc/supervisor/conf.d/shinken-receiver.conf
ADD shinken-scheduler.conf /etc/supervisor/conf.d/shinken-scheduler.conf

EXPOSE 50000 7767 7768 7769 7770 7771 7772 7773

ENTRYPOINT [ "/usr/bin/supervisord" ]
