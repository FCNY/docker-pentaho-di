FROM java:jre

MAINTAINER Aloysius Lim

ENV PDI_RELEASE=6.1 \
    PDI_VERSION=6.1.0.1-196 \
    PDI_HOME=/opt/pentaho-di \
    KETTLE_HOME=/pentaho-di

RUN curl -L -o /tmp/pdi-ce-${PDI_VERSION}.zip \
      http://downloads.sourceforge.net/project/pentaho/Data%20Integration/${PDI_RELEASE}/pdi-ce-${PDI_VERSION}.zip && \
    unzip -q /tmp/pdi-ce-${PDI_VERSION}.zip -d $PDI_HOME && \
    rm /tmp/pdi-ce-${PDI_VERSION}.zip

RUN wget -P $PDI_HOME/data-integration/lib http://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.35/mysql-connector-java-5.1.35.jar


ENV PATH=$PDI_HOME/data-integration:$PATH

EXPOSE 8080

RUN mkdir -p $KETTLE_HOME/.kettle /docker-entrypoint.d /templates

COPY carte_config*.xml /templates/

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["carte.sh", "/pentaho-di/carte_config.xml"]
