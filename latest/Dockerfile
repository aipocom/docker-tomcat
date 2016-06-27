FROM alpine:3.4

ENV TOMCAT_MAJOR=7 \
    TOMCAT_VERSION=7.0.70 \
    TOMCAT_HOME=/opt/tomcat \
    CATALINA_HOME=/opt/tomcat \
    CATALINA_OUT=/dev/null \
    JDBC_MYSQL_VERSION=5.1.39 \
    JDBC_POSTGRESQL_VERSION=9.4.1208

RUN mkdir -p /opt && \
    apk upgrade --update && \
    apk add --update openjdk8-jre curl tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    curl -jksSL -o /tmp/apache-tomcat.tar.gz http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    tar -C /opt -xvzf /tmp/apache-tomcat.tar.gz && \
    ln -s /opt/apache-tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME} && \
    rm -rf ${TOMCAT_HOME}/webapps/* && \
    curl -jksSL -o /tmp/mysql-connector-java.tar.gz http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-${JDBC_MYSQL_VERSION}.tar.gz && \
    tar -C /tmp -xvzf /tmp/mysql-connector-java.tar.gz && \
    cp /tmp/mysql-connector-java-${JDBC_MYSQL_VERSION}/mysql-connector-java-${JDBC_MYSQL_VERSION}-bin.jar /opt/tomcat/lib/ && \
    curl -jksSL -o /opt/tomcat/lib/postgresql-${JDBC_POSTGRESQL_VERSION}.jar http://jdbc.postgresql.org/download/postgresql-${JDBC_POSTGRESQL_VERSION}.jar && \
    apk del curl tzdata && \
    rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8080
ENTRYPOINT [ "/opt/tomcat/bin/catalina.sh", "run" ]
