# Hadoop

* ### Set up a single node Hadoop cluster(ie NameNode and DataNode on the same server) - `pseudo-distributed mode`
  * Install and SetUp Java 8 and Hadoop:
    * `sudo yum install java-1.8.0-openjdk -y`
    * `export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64/jre` (add it into bashrc file and PATH variable)
    * `curl -O http://mirrors.gigenet.com/apache/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz`
    * `tar -xzf hadoop-2.9.2.tar.gz`
    * `mv hadoop-2.9.2 hadoop`
  * Configure Hadoop
    * `cd hadoop`
    * Set up passwordless access to ssh 
      * `ssh-keygen && cat ~/.ssh/id_rsa.pub >>  ~/.ssh/authorized_keys`
      * verify this works by executing `ssh localhost`
    * [Optional-if JAVA_HOME Not set]
      * set JAVA_HOME in `etc/hadoop/hadoop-env.sh` by changing the line `export JAVA_HOME=${JAVA_HOME}` to `export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64/jre`
    * Set hdfs as the default file system in `etc/hadoop/core-site.xml` 
      * ```<configuration>
        <property> 
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
        </property>
        </configuration> 
         ```
     * Set the default block replication to 1 in `etc/hadoop/hdfs-site.xml`
       * ```
          <configuration>
          <property>
          <name>dfs.replication</name>
          <value>1</value>
          </property>
          </configuration>
          ```
      * Format the file system
        * `bin/hdfs namenode -format`
      * Start hadoop
        * `sbin/start-dfs.sh`
