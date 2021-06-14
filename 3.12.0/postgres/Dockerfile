FROM geonetwork:3.12.0

RUN apt-get update && apt-get install -y postgresql-client && \
    rm -rf /var/lib/apt/lists/*

#Set PostgreSQL as default GN DB
RUN sed -i -e 's#<import resource="../config-db/${geonetwork.db.type:h2}.xml"/>#<!--<import resource="../config-db/${geonetwork.db.type:h2}.xml"/-->#g' $CATALINA_HOME/webapps/geonetwork/WEB-INF/config-node/srv.xml && \
sed -i -e 's#<!--<import resource="../config-db/postgres-postgis.xml"/> -->#<import resource="../config-db/postgres-postgis.xml"/>#g' $CATALINA_HOME/webapps/geonetwork/WEB-INF/config-node/srv.xml

RUN sed -i -e 's#<import resource="config-security-${geonetwork.security.type:default}.xml"/>#<!--<import resource="config-security-${geonetwork.security.type:default}.xml"/> -->#g' $CATALINA_HOME/webapps/geonetwork/WEB-INF/config-security/config-security.xml && \
sed -i -e 's#<!--<import resource="config-security-keycloak.xml"/> -->#<import resource="config-security-keycloak.xml"/>#g' $CATALINA_HOME/webapps/geonetwork/WEB-INF/config-security/config-security.xml

COPY ./jdbc.properties $CATALINA_HOME/webapps/geonetwork/WEB-INF/config-db/jdbc.properties

#Initializing database & connection string for GN
COPY ./docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

CMD ["catalina.sh", "run"]
