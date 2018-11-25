FROM openjdk:8-jdk
VOLUME /tmp

MAINTAINER Donald Vines <donald_vines@hotmail.com>

ARG WAR_FILE # expects value from build script
ARG WAR_FILE # expects value from build script
ARG KEYSTORE_FILENAME=/var/ssl/daytrader/keystore.jks
ARG KEYSTORE_PASSWORD=password
ARG TRUSTSTORE_LOCATION=/var/ssl/daytrader/truststore.jks
ARG TRUSTSTORE_PASSWORD=password
ARG APP_VERSION=4.0.0
ARG APP_ARTIFACTID=daytrader-quotesapp
ARG WAR_ARTIFACTID=daytrader-quotes



# Set ssl variables
ENV DAYTRADER_KEYSTORE_FILENAME=${KEYSTORE_FILENAME}
ENV DAYTRADER_KEYSTORE_PASSWORD=${KEYSTORE_PASSWORD}
ENV DAYTRADER_TRUSTSTORE_LOCATION=${TRUSTSTORE_LOCATION}
ENV DAYTRADER_TRUSTSTORE_PASSWORD=${TRUSTSTORE_PASSWORD}

# Set app variables
ENV DAYTRADER_APP_VERSION=${APP_VERSION}
ENV DAYTRADER_APP_ARTIFACTID=${APP_ARTIFACTID}
ENV DAYTRADER_WAR_ARTIFACTID=${WAR_ARTIFACTID}

# Set database variables
ENV DAYTRADER_DATABASE_DRIVER=org.apache.derby.jdbc.EmbeddedDriver
ENV DAYTRADER_DATABASE_URL='jdbc:derby:tradesdb;create=true'
ENV DAYTRADER_DATABASE_USERNAME=
ENV DAYTRADER_DATABASE_PASSWORD=

# Set tomcat variables
ENV SERVER_PORT=4443
ENV SERVER_PORT_HTTPS=4443

# Make port visible
EXPOSE 4443

# Set service routes
ENV DAYTRADER_ACCOUNTS_SERVICE=https://daytrader-accounts
ENV DAYTRADER_GATEWAY_SERVICE=https://daytrader-gateway
ENV DAYTRADER_PORTFOLIOS_SERVICE=https://daytrader-portfolios
ENV DAYTRADER_QUOTES_SERVICE=https://daytrader-quotes

# Set logging variables
ENV DAYTRADER_LOG_FILENAME=/var/log/daytrader/$DAYTRADER_APP_ARTIFACTID-$DAYTRADER_APP_VERSION.log
ENV DAYTRADER_LOG_LEVEL=TRACE
ENV DAYTRADER_LOG_APPENDER=ConsoleAppender

# Create the database folder
RUN mkdir -p -m 0777 /var/dat/daytrader


# Create the log folder
RUN mkdir -p -m 0777 /var/log/daytrader

# Create the log file and set permissions
RUN touch $DAYTRADER_LOG_FILENAME
RUN chmod 666 $DAYTRADER_LOG_FILENAME

# Create the ssl folder
RUN mkdir -p -m 0777 /var/ssl/daytrader

# Add the truststore to the container and set permissions
ADD ${JKS_FILE} $DAYTRADER_TRUSTSTORE_LOCATION
RUN chmod 666 $DAYTRADER_TRUSTSTORE_LOCATION

# Add the application's war to the container
ADD ${WAR_FILE} app.war

ENV JAVA_OPTS="-Djavax.net.ssl.trustStore=/var/ssl/daytrader/truststore.jks -Djavax.net.ssl.trustStorePassword=password"

ENTRYPOINT exec java $JAVA_OPTS -jar app.war
