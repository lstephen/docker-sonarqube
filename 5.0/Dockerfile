FROM java:8-jre
MAINTAINER Levi Stephen <levi.stephen@gmail.com>

ENV SONARQUBE_HOME /opt/sonarqube

MKDIR /opt
WORKDIR /opt

RUN curl -LO http://dist.sonar.codehaus.org/sonarqube-5.0.zip && unzip sonarqube-5.0.zip && rm sonarqube-5.0.zip

RUN ln -s /opt/sonarqube-5.0 ${SONARQUBE_HOME}
RUN ln -s ${SONARQUBE_HOME}/bin/linux-x86-64/sonar.sh /usr/bin/sonar.sh

COPY sonar.properties ${SONARQUBE_HOME}/conf/sonar.properties

RUN ln -sf /dev/stdout ${SONARQUBE_HOME}/logs/sonar.log

EXPOSE 9000
CMD ["sonar.sh", "console"]


