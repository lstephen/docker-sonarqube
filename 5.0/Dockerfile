FROM java:8-jre
MAINTAINER Levi Stephen <levi.stephen@gmail.com>

ENV SONARQUBE_HOME /opt/sonarqube

MKDIR /opt
WORKDIR /opt

RUN curl -LO http://dist.sonar.codehaus.org/sonarqube-5.0.zip && unzip sonarqube-5.0.zip && rm sonarqube-5.0.zip

RUN ln -s /opt/sonarqube-5.0 ${SONARQUBE_HOME}
RUN ln -s ${SONARQUBE_HOME}/bin/linux-x86-64/sonar.sh /usr/bin/sonar.sh

# Update plugins
RUN rm ${SONARQUBE_HOME}/lib/bundled-plugins/*
RUN curl -L http://repository.codehaus.org/org/codehaus/sonar-plugins/java/sonar-java-plugin/2.9.1/sonar-java-plugin-2.9.1.jar -o ${SONARQUBE_HOME}/lib/bundled-plugins/sonar-java-plugin-2.9.1.jar

VOLUME ${SONARQUBE_HOME}/extensions/plugins

COPY sonar.properties ${SONARQUBE_HOME}/conf/sonar.properties

RUN ln -sf /dev/stdout ${SONARQUBE_HOME}/logs/sonar.log

EXPOSE 9000
CMD ["sonar.sh", "console"]


