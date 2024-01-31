FROM sebge2/hadoop-base:latest
MAINTAINER sgerard <sgerard@emasphere.com>

# Definir variáveis de ambiente
ENV HADOOP_INSTALL /usr/local/hadoop
ENV HDFS_NAMENODE_DIR /root/hdfs/namenode
ENV ZOOKEEPER_DIR /root/zookeeper
ENV HDFS_DATANODE_DIR /root/hdfs/datanode

# Copiar arquivos de configuração e scripts
ADD files/hadoop/* /tmp/
ADD files/init/* /tmp/

# Criar diretórios necessários
RUN mkdir -p $HDFS_NAMENODE_DIR && \
    mkdir -p $ZOOKEEPER_DIR && \ 
    mkdir -p $HDFS_DATANODE_DIR

# Mover arquivos de configuração para o diretório apropriado
RUN mv /tmp/hdfs-site.xml $HADOOP_INSTALL/etc/hadoop/hdfs-site.xml && \ 
    mv /tmp/core-site.xml $HADOOP_INSTALL/etc/hadoop/core-site.xml && \
    mv /tmp/mapred-site.xml $HADOOP_INSTALL/etc/hadoop/mapred-site.xml && \
    mv /tmp/yarn-site.xml $HADOOP_INSTALL/etc/hadoop/yarn-site.xml && \
    mv /tmp/stop-hadoop.sh ~/stop-hadoop.sh && \
    mv /tmp/start-hadoop.sh ~/start-hadoop.sh && \
    mv /tmp/run-wordcount.sh ~/run-wordcount.sh && \ 
    mv /tmp/start-ssh-serf.sh ~/start-ssh-serf.sh  && \ 
    mv /tmp/configure-members.sh ~/configure-members.sh 

# Dar permissões adequadas aos scripts e diretórios
RUN chmod +x ~/start-hadoop.sh && \
    chmod +x ~/stop-hadoop.sh && \
    chmod +x ~/run-wordcount.sh && \
    chmod +x ~/start-ssh-serf.sh && \
    chmod +x ~/configure-members.sh  && \
    chmod 1777 /tmp

# Formatar o namenode
RUN $HADOOP_INSTALL/bin/hdfs namenode -format

# Expor as portas necessárias
EXPOSE 22 7373 7946 9000 50010 50020 50070 50075 50090 50475 8030 8031 8032 8033 8040 8042 8060 8088 50060

# Comando padrão para iniciar o contêiner
CMD /root/start-ssh-serf.sh && bash
