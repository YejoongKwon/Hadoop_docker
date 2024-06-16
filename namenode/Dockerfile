FROM hadoop-spark-base

HEALTHCHECK CMD curl -f http://namenode:9870/ || exit 1

RUN yum -y install nano
ADD hdfs-site.xml $HADOOP_CONF_DIR

# FsImage, EditLog 파일 경로
# FsImage : block replication 개수를 mapping 시켜놓은 정보
RUN mkdir $HADOOP_HOME/dfs/name

ADD start.sh /start.sh
RUN chmod a+x /start.sh

# 9000 : IPC port (namenode <> datanode 통신을 위한 포트)
# docker container간 통신만 하면 되기때문에 local port와 매핑해줄 필요 없음
# 9870 : NameNode HTTP web ui
EXPOSE 9000 9870

RUN echo 'export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-2.el8_5.aarch64' >> /etc/hadoop/hadoop-env.sh
# RUN echo 'export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=$HADOOP_PREFIX/lib/native"'>>/etc/hadoop/hadoop-env.sh
RUN echo 'export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"'>>/etc/hadoop/hadoop-env.sh
CMD ["/start.sh", "/opt/hadoop/dfs/name"]
