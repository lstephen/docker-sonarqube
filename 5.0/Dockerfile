FROM java:8-jdk
MAINTAINER Levi Stephen <levi.stephen@gmail.com>

RUN apt-get update && apt-get install -y curl unzip

ENV SONARQUBE_HOME /opt/sonarqube
ENV SONARQUBE_VERSION 5.0.1

WORKDIR /opt

RUN curl -LO http://dist.sonar.codehaus.org/sonarqube-${SONARQUBE_VERSION}.zip \
 && unzip sonarqube-${SONARQUBE_VERSION}.zip && rm sonarqube-${SONARQUBE_VERSION}.zip

RUN ln -s /opt/sonarqube-${SONARQUBE_VERSION} ${SONARQUBE_HOME} \
 && ln -s ${SONARQUBE_HOME}/bin/linux-x86-64/sonar.sh /usr/bin/sonar.sh

# Update plugins
RUN rm -f ${SONARQUBE_HOME}/lib/bundled-plugins/*
RUN curl -L http://repository.codehaus.org/org/codehaus/sonar-plugins/java/sonar-java-plugin/3.0/sonar-java-plugin-3.0.jar \
         -o ${SONARQUBE_HOME}/lib/bundled-plugins/sonar-java-plugin-3.0.jar

RUN rm -rf ${SONARQUBE_HOME}/extensions/plugins \
 && ln -s ${SONARQUBE_HOME}/lib/bundled-plugins ${SONARQUBE_HOME}/extensions/plugins

COPY sonar.properties ${SONARQUBE_HOME}/conf/sonar.properties

RUN ln -sf /dev/stdout ${SONARQUBE_HOME}/logs/sonar.log
EXPOSE 9000
CMD ["sonar.sh", "console"]

