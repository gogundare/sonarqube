FROM openjdk:11-slim
RUN apt-get update && apt-get install -y curl gnupg2 unzip

ARG VERSION
ENV SONAR_VERSION=$VERSION
ENV SONARQUBE_HOME=/opt/sonarqube
ENV SONARQUBE_JDBC_USERNAME=sonar
ENV SONARQUBE_JDBC_PASSWORD=sonar
# Http port
EXPOSE 9000

RUN groupadd -r sonarqube && useradd -r -g sonarqube sonarqube

RUN set -x \
    && cd /opt \
    && curl -o sonarqube.zip -fSL https://binaries.sonarsource.com/CommercialDistribution/sonarqube-developer/sonarqube-developer-$SONAR_VERSION.zip \
    && unzip sonarqube.zip \
    && mv sonarqube-$SONAR_VERSION sonarqube \
    && chown -R sonarqube:sonarqube sonarqube \
    && rm sonarqube.zip* \
    && rm -rf $SONARQUBE_HOME/bin/*

VOLUME "$SONARQUBE_HOME/data"

WORKDIR $SONARQUBE_HOME
COPY run.sh $SONARQUBE_HOME/bin/
COPY plugins/* $SONARQUBE_HOME/extensions/plugins/
USER sonarqube
ENTRYPOINT ["./bin/run.sh"]