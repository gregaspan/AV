FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive \
    JAVA_VERSION=17 \
    JAVA_HOME=/usr/lib/jvm/java-17-openjdk-arm64 \
    HADOOP_VERSION=3.4.1 \
    HADOOP_HOME=/opt/hadoop \
    SQOOP_VERSION=1.4.7 \
    SQOOP_HOME=/opt/sqoop \
    MYSQL_CONNECTOR_VERSION=8.4.0 \
    POSTGRESQL_CONNECTOR_VERSION=42.7.5 \
    PATH=$PATH:/opt/hadoop/bin:/opt/hadoop/sbin:/opt/sqoop/bin

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        openjdk-17-jdk \
        wget \
        curl \
        unzip \
        vim \
        net-tools \
        iputils-ping \
        gnupg \
        lsb-release && \
    rm -rf /var/lib/apt/lists/*

RUN wget -q https://dlcdn.apache.org/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar -xzf hadoop-${HADOOP_VERSION}.tar.gz -C /opt && \
    mv /opt/hadoop-${HADOOP_VERSION} ${HADOOP_HOME} && \
    rm hadoop-${HADOOP_VERSION}.tar.gz

RUN wget -q https://archive.apache.org/dist/sqoop/${SQOOP_VERSION}/sqoop-${SQOOP_VERSION}.bin__hadoop-2.6.0.tar.gz && \
    tar -xzf sqoop-${SQOOP_VERSION}.bin__hadoop-2.6.0.tar.gz -C /opt && \
    mv /opt/sqoop-${SQOOP_VERSION}.bin__hadoop-2.6.0 ${SQOOP_HOME} && \
    rm sqoop-${SQOOP_VERSION}.bin__hadoop-2.6.0.tar.gz

RUN wget -q https://repo1.maven.org/maven2/com/mysql/mysql-connector-j/${MYSQL_CONNECTOR_VERSION}/mysql-connector-j-${MYSQL_CONNECTOR_VERSION}.jar -O ${SQOOP_HOME}/lib/mysql-connector-j-${MYSQL_CONNECTOR_VERSION}.jar && \
    wget -q https://jdbc.postgresql.org/download/postgresql-${POSTGRESQL_CONNECTOR_VERSION}.jar -O ${SQOOP_HOME}/lib/postgresql-${POSTGRESQL_CONNECTOR_VERSION}.jar

ENV HBASE_HOME=/opt/dummy_hbase \
    HCAT_HOME=/opt/dummy_hcat \
    ACCUMULO_HOME=/opt/dummy_accumulo \
    ZOOKEEPER_HOME=/opt/dummy_zookeeper

RUN mkdir -p "$HBASE_HOME" "$HCAT_HOME" "$ACCUMULO_HOME" "$ZOOKEEPER_HOME"

CMD ["/bin/bash"]