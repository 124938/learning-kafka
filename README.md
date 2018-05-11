## Overview

* Kafka is a distributed streaming platform, which has following capabilities:
  * **Publish & Subscribe** : It let's you publish and subscribe to streams of records/messages i.e. it allows to read and write stream of data like a messaging system.
  * **Process** : It let's you write scalable stream processing application that react to events in a real time.
  * **Store** : It let's you store streams of data safely in a distributed, replicated, fault-tolerant cluster.

* Kafka is generally used for two broad classes of applications:
  * Building real-time streaming data pipelines that reliably get data between systems or applications
  * Building real-time streaming applications that transform or react to the streams of data

## Architecture

### Few Important Concepts
* Kafka is run as a cluster on one or more servers.
* The Kafka cluster stores streams of records/messages in categories called topics.
* Each record consists of a key, a value and a timestamp.

### Core APIs
* **The Producer API** - It allows an application to publish a stream records to one of more Kafka topics.
* **The Consumer API** - It allows an application to subscribe to one or more topics and process the stream of records.
* **The Stream API** - It allows an application to act as a stream processor, consuming an input stream from one or more topics and producing an output stream to one of more topics, effectively transforming the input streams to output streams.
* **The Connector API** - It allows building and running reusable producers or consumers that connect Kafka topics to existing applications or data systems.

  ![Alt text](_images/_1_kafka_api.png?raw=true "Kafka API")

### Communication
* In Kafka the communication between client and kafka cluster is done with a simple, high-performance, language agnostic TCP protocol.
* Kafka client provides supports for many languages like java, c++, python, ruby, many more..


## Setup

### Step-1: Download kafka binaries

* Download kafka binaries

~~~
asus@asus-GL553VD:~/tech_soft$ wget http://www-us.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz

--2018-05-11 17:12:07--  http://www-us.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz
Resolving www-us.apache.org (www-us.apache.org)... 140.211.11.105
Connecting to www-us.apache.org (www-us.apache.org)|140.211.11.105|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 56969154 (54M) [application/x-gzip]
Saving to: ‘kafka_2.11-1.1.0.tgz’

kafka_2.11-1.1.0.tgz                               100%[================================================================================================================>]  54.33M  5.62MB/s    in 10s     

2018-05-11 17:12:18 (5.25 MB/s) - ‘kafka_2.11-1.1.0.tgz’ saved [56969154/56969154]
~~~

* Extract kafka binaries

~~~
asus@asus-GL553VD:~/tech_soft$ tar -xzf kafka_2.11-1.1.0.tgz
~~~

* Verify kafka binaries

~~~
asus@asus-GL553VD:~/tech_soft$ cd kafka_2.11-1.1.0 

asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ ls -ltr
total 52
-rw-r--r-- 1 asus asus   336 Mar 24 04:21 NOTICE
-rw-r--r-- 1 asus asus 28824 Mar 24 04:21 LICENSE
drwxr-xr-x 2 asus asus  4096 Mar 24 04:24 config
drwxr-xr-x 3 asus asus  4096 Mar 24 04:24 bin
drwxr-xr-x 2 asus asus  4096 Mar 24 04:24 site-docs
drwxr-xr-x 2 asus asus  4096 May 11 17:13 libs
~~~

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ cd bin/
~~~

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0/bin$ ls -ltr
total 132
-rwxr-xr-x 1 asus asus  968 Mar 24 04:21 zookeeper-shell.sh
-rwxr-xr-x 1 asus asus 1001 Mar 24 04:21 zookeeper-server-stop.sh
-rwxr-xr-x 1 asus asus 1393 Mar 24 04:21 zookeeper-server-start.sh
-rwxr-xr-x 1 asus asus  867 Mar 24 04:21 zookeeper-security-migration.sh
-rwxr-xr-x 1 asus asus 1722 Mar 24 04:21 trogdor.sh
-rwxr-xr-x 1 asus asus  958 Mar 24 04:21 kafka-verifiable-producer.sh
-rwxr-xr-x 1 asus asus  958 Mar 24 04:21 kafka-verifiable-consumer.sh
-rwxr-xr-x 1 asus asus  863 Mar 24 04:21 kafka-topics.sh
-rwxr-xr-x 1 asus asus  945 Mar 24 04:21 kafka-streams-application-reset.sh
-rwxr-xr-x 1 asus asus  870 Mar 24 04:21 kafka-simple-consumer-shell.sh
-rwxr-xr-x 1 asus asus  997 Mar 24 04:21 kafka-server-stop.sh
-rwxr-xr-x 1 asus asus 1376 Mar 24 04:21 kafka-server-start.sh
-rwxr-xr-x 1 asus asus 7864 Mar 24 04:21 kafka-run-class.sh
-rwxr-xr-x 1 asus asus  874 Mar 24 04:21 kafka-replica-verification.sh
-rwxr-xr-x 1 asus asus  868 Mar 24 04:21 kafka-replay-log-producer.sh
-rwxr-xr-x 1 asus asus  874 Mar 24 04:21 kafka-reassign-partitions.sh
-rwxr-xr-x 1 asus asus  959 Mar 24 04:21 kafka-producer-perf-test.sh
-rwxr-xr-x 1 asus asus  886 Mar 24 04:21 kafka-preferred-replica-election.sh
-rwxr-xr-x 1 asus asus  862 Mar 24 04:21 kafka-mirror-maker.sh
-rwxr-xr-x 1 asus asus  863 Mar 24 04:21 kafka-log-dirs.sh
-rwxr-xr-x 1 asus asus  869 Mar 24 04:21 kafka-delete-records.sh
-rwxr-xr-x 1 asus asus  871 Mar 24 04:21 kafka-delegation-tokens.sh
-rwxr-xr-x 1 asus asus  948 Mar 24 04:21 kafka-consumer-perf-test.sh
-rwxr-xr-x 1 asus asus  871 Mar 24 04:21 kafka-consumer-groups.sh
-rwxr-xr-x 1 asus asus  944 Mar 24 04:21 kafka-console-producer.sh
-rwxr-xr-x 1 asus asus  945 Mar 24 04:21 kafka-console-consumer.sh
-rwxr-xr-x 1 asus asus  864 Mar 24 04:21 kafka-configs.sh
-rwxr-xr-x 1 asus asus  873 Mar 24 04:21 kafka-broker-api-versions.sh
-rwxr-xr-x 1 asus asus  861 Mar 24 04:21 kafka-acls.sh
-rwxr-xr-x 1 asus asus 1418 Mar 24 04:21 connect-standalone.sh
-rwxr-xr-x 1 asus asus 1421 Mar 24 04:21 connect-distributed.sh
drwxr-xr-x 2 asus asus 4096 Mar 24 04:21 windows
~~~
 
### Step-2: Start the server

* As kakfa uses Zookeeper, first needs to start a Zookeeper server

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/zookeeper-server-start.sh config/zookeeper.properties

[2018-05-11 17:30:13,723] INFO Reading configuration from: config/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
[2018-05-11 17:30:13,732] INFO autopurge.snapRetainCount set to 3 (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-05-11 17:30:13,732] INFO autopurge.purgeInterval set to 0 (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-05-11 17:30:13,732] INFO Purge task is not scheduled. (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-05-11 17:30:13,732] WARN Either no config or no quorum defined in config, running  in standalone mode (org.apache.zookeeper.server.quorum.QuorumPeerMain)
[2018-05-11 17:30:13,760] INFO Reading configuration from: config/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
[2018-05-11 17:30:13,761] INFO Starting server (org.apache.zookeeper.server.ZooKeeperServerMain)
[2018-05-11 17:30:13,777] INFO Server environment:zookeeper.version=3.4.10-39d3a4f269333c922ed3db283be479f9deacaa0f, built on 03/23/2017 10:13 GMT (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,777] INFO Server environment:host.name=asus-GL553VD (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,777] INFO Server environment:java.version=1.8.0_162 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,777] INFO Server environment:java.vendor=Oracle Corporation (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:java.home=/usr/lib/jvm/java-8-openjdk-amd64/jre (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:java.class.path=/home/asus/tech_soft/kafka_2.11-1.1.0/bin/../libs/aopalliance-repackaged-2.5.0-b32.jar:/home/asus/tech_soft/kafka_2.11-1.1.0/bin/../[2018-05-11 17:30:13,778] INFO Server environment:java.io.tmpdir=/tmp (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:java.compiler=<NA> (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:os.name=Linux (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:os.arch=amd64 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:os.version=4.4.0-122-generic (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:user.name=asus (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:user.home=/home/asus (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,778] INFO Server environment:user.dir=/home/asus/tech_soft/kafka_2.11-1.1.0 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,790] INFO tickTime set to 3000 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,790] INFO minSessionTimeout set to -1 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,790] INFO maxSessionTimeout set to -1 (org.apache.zookeeper.server.ZooKeeperServer)
[2018-05-11 17:30:13,838] INFO binding to port 0.0.0.0/0.0.0.0:2181 (org.apache.zookeeper.server.NIOServerCnxnFactory)
~~~

* Start Kafka server (Refer below c)

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/kafka-server-start.sh config/server.properties

[2018-05-11 17:31:26,126] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)
[2018-05-11 17:31:26,349] INFO starting (kafka.server.KafkaServer)
[2018-05-11 17:31:26,349] INFO Connecting to zookeeper on localhost:2181 (kafka.server.KafkaServer)
[2018-05-11 17:31:26,379] INFO [ZooKeeperClient] Initializing a new session to localhost:2181. (kafka.zookeeper.ZooKeeperClient)
[2018-05-11 17:31:26,383] INFO Client environment:zookeeper.version=3.4.10-39d3a4f269333c922ed3db283be479f9deacaa0f, built on 03/23/2017 10:13 GMT (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,383] INFO Client environment:host.name=asus-GL553VD (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,383] INFO Client environment:java.version=1.8.0_162 (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,383] INFO Client environment:java.vendor=Oracle Corporation (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,383] INFO Client environment:java.home=/usr/lib/jvm/java-8-openjdk-amd64/jre (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:java.library.path=/usr/java/packages/lib/amd64:/usr/lib/x86_64-linux-gnu/jni:/lib/x86_64-linux-gnu:/usr/lib/x86_64-linux-gnu:/usr/lib/jni:/lib:/usr/lib (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:java.io.tmpdir=/tmp (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:java.compiler=<NA> (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:os.name=Linux (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:os.arch=amd64 (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:os.version=4.4.0-122-generic (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:user.name=asus (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:user.home=/home/asus (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,384] INFO Client environment:user.dir=/home/asus/tech_soft/kafka_2.11-1.1.0 (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,385] INFO Initiating client connection, connectString=localhost:2181 sessionTimeout=6000 watcher=kafka.zookeeper.ZooKeeperClient$ZooKeeperClientWatcher$@7f0eb4b4 (org.apache.zookeeper.ZooKeeper)
[2018-05-11 17:31:26,394] INFO Opening socket connection to server localhost/127.0.0.1:2181. Will not attempt to authenticate using SASL (unknown error) (org.apache.zookeeper.ClientCnxn)
[2018-05-11 17:31:26,404] INFO [ZooKeeperClient] Waiting until connected. (kafka.zookeeper.ZooKeeperClient)
[2018-05-11 17:31:26,412] INFO Socket connection established to localhost/127.0.0.1:2181, initiating session (org.apache.zookeeper.ClientCnxn)
[2018-05-11 17:31:26,508] INFO Session establishment complete on server localhost/127.0.0.1:2181, sessionid = 0x1634f12ac1b0000, negotiated timeout = 6000 (org.apache.zookeeper.ClientCnxn)
[2018-05-11 17:31:26,514] INFO [ZooKeeperClient] Connected. (kafka.zookeeper.ZooKeeperClient)
[2018-05-11 17:31:26,916] INFO Cluster ID = MeKYpfdkSuWHrxBjRqOvaQ (kafka.server.KafkaServer)
[2018-05-11 17:31:26,946] WARN No meta.properties file under dir /tmp/kafka-logs/meta.properties (kafka.server.BrokerMetadataCheckpoint)
[2018-05-11 17:31:26,992] INFO KafkaConfig values: 
  advertised.host.name = null
  advertised.listeners = null
  advertised.port = null
  alter.config.policy.class.name = null
  alter.log.dirs.replication.quota.window.num = 11
  alter.log.dirs.replication.quota.window.size.seconds = 1
  authorizer.class.name = 
  auto.create.topics.enable = true
  auto.leader.rebalance.enable = true
  background.threads = 10
  broker.id = 0
  broker.id.generation.enable = true
  broker.rack = null
  compression.type = producer
  connections.max.idle.ms = 600000
  controlled.shutdown.enable = true
  controlled.shutdown.max.retries = 3
  controlled.shutdown.retry.backoff.ms = 5000
  controller.socket.timeout.ms = 30000
  create.topic.policy.class.name = null
  default.replication.factor = 1
  delegation.token.expiry.check.interval.ms = 3600000
  delegation.token.expiry.time.ms = 86400000
  delegation.token.master.key = null
  delegation.token.max.lifetime.ms = 604800000
  delete.records.purgatory.purge.interval.requests = 1
  delete.topic.enable = true
  fetch.purgatory.purge.interval.requests = 1000
  group.initial.rebalance.delay.ms = 0
  group.max.session.timeout.ms = 300000
  group.min.session.timeout.ms = 6000
  host.name = 
  inter.broker.listener.name = null
  inter.broker.protocol.version = 1.1-IV0
  leader.imbalance.check.interval.seconds = 300
  leader.imbalance.per.broker.percentage = 10
  listener.security.protocol.map = PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SSL
  listeners = null
  log.cleaner.backoff.ms = 15000
  log.cleaner.dedupe.buffer.size = 134217728
  log.cleaner.delete.retention.ms = 86400000
  log.cleaner.enable = true
  log.cleaner.io.buffer.load.factor = 0.9
  log.cleaner.io.buffer.size = 524288
  log.cleaner.io.max.bytes.per.second = 1.7976931348623157E308
  log.cleaner.min.cleanable.ratio = 0.5
  log.cleaner.min.compaction.lag.ms = 0
  log.cleaner.threads = 1
  log.cleanup.policy = [delete]
  log.dir = /tmp/kafka-logs
  log.dirs = /tmp/kafka-logs
  log.flush.interval.messages = 9223372036854775807
  log.flush.interval.ms = null
  log.flush.offset.checkpoint.interval.ms = 60000
  log.flush.scheduler.interval.ms = 9223372036854775807
  log.flush.start.offset.checkpoint.interval.ms = 60000
  log.index.interval.bytes = 4096
  log.index.size.max.bytes = 10485760
  log.message.format.version = 1.1-IV0
  log.message.timestamp.difference.max.ms = 9223372036854775807
  log.message.timestamp.type = CreateTime
  log.preallocate = false
  log.retention.bytes = -1
  log.retention.check.interval.ms = 300000
  log.retention.hours = 168
  log.retention.minutes = null
  log.retention.ms = null
  log.roll.hours = 168
  log.roll.jitter.hours = 0
  log.roll.jitter.ms = null
  log.roll.ms = null
  log.segment.bytes = 1073741824
  log.segment.delete.delay.ms = 60000
  max.connections.per.ip = 2147483647
  max.connections.per.ip.overrides = 
  max.incremental.fetch.session.cache.slots = 1000
  message.max.bytes = 1000012
  metric.reporters = []
  metrics.num.samples = 2
  metrics.recording.level = INFO
  metrics.sample.window.ms = 30000
  min.insync.replicas = 1
  num.io.threads = 8
  num.network.threads = 3
  num.partitions = 1
  num.recovery.threads.per.data.dir = 1
  num.replica.alter.log.dirs.threads = null
  num.replica.fetchers = 1
  offset.metadata.max.bytes = 4096
  offsets.commit.required.acks = -1
  offsets.commit.timeout.ms = 5000
  offsets.load.buffer.size = 5242880
  offsets.retention.check.interval.ms = 600000
  offsets.retention.minutes = 1440
  offsets.topic.compression.codec = 0
  offsets.topic.num.partitions = 50
  offsets.topic.replication.factor = 1
  offsets.topic.segment.bytes = 104857600
  password.encoder.cipher.algorithm = AES/CBC/PKCS5Padding
  password.encoder.iterations = 4096
  password.encoder.key.length = 128
  password.encoder.keyfactory.algorithm = null
  password.encoder.old.secret = null
  password.encoder.secret = null
  port = 9092
  principal.builder.class = null
  producer.purgatory.purge.interval.requests = 1000
  queued.max.request.bytes = -1
  queued.max.requests = 500
  quota.consumer.default = 9223372036854775807
  quota.producer.default = 9223372036854775807
  quota.window.num = 11
  quota.window.size.seconds = 1
  replica.fetch.backoff.ms = 1000
  replica.fetch.max.bytes = 1048576
  replica.fetch.min.bytes = 1
  replica.fetch.response.max.bytes = 10485760
  replica.fetch.wait.max.ms = 500
  replica.high.watermark.checkpoint.interval.ms = 5000
  replica.lag.time.max.ms = 10000
  replica.socket.receive.buffer.bytes = 65536
  replica.socket.timeout.ms = 30000
  replication.quota.window.num = 11
  replication.quota.window.size.seconds = 1
  request.timeout.ms = 30000
  reserved.broker.max.id = 1000
  sasl.enabled.mechanisms = [GSSAPI]
  sasl.jaas.config = null
  sasl.kerberos.kinit.cmd = /usr/bin/kinit
  sasl.kerberos.min.time.before.relogin = 60000
  sasl.kerberos.principal.to.local.rules = [DEFAULT]
  sasl.kerberos.service.name = null
  sasl.kerberos.ticket.renew.jitter = 0.05
  sasl.kerberos.ticket.renew.window.factor = 0.8
  sasl.mechanism.inter.broker.protocol = GSSAPI
  security.inter.broker.protocol = PLAINTEXT
  socket.receive.buffer.bytes = 102400
  socket.request.max.bytes = 104857600
  socket.send.buffer.bytes = 102400
  ssl.cipher.suites = []
  ssl.client.auth = none
  ssl.enabled.protocols = [TLSv1.2, TLSv1.1, TLSv1]
  ssl.endpoint.identification.algorithm = null
  ssl.key.password = null
  ssl.keymanager.algorithm = SunX509
  ssl.keystore.location = null
  ssl.keystore.password = null
  ssl.keystore.type = JKS
  ssl.protocol = TLS
  ssl.provider = null
  ssl.secure.random.implementation = null
  ssl.trustmanager.algorithm = PKIX
  ssl.truststore.location = null
  ssl.truststore.password = null
  ssl.truststore.type = JKS
  transaction.abort.timed.out.transaction.cleanup.interval.ms = 60000
  transaction.max.timeout.ms = 900000
  transaction.remove.expired.transaction.cleanup.interval.ms = 3600000
  transaction.state.log.load.buffer.size = 5242880
  transaction.state.log.min.isr = 1
  transaction.state.log.num.partitions = 50
  transaction.state.log.replication.factor = 1
  transaction.state.log.segment.bytes = 104857600
  transactional.id.expiration.ms = 604800000
  unclean.leader.election.enable = false
  zookeeper.connect = localhost:2181
  zookeeper.connection.timeout.ms = 6000
  zookeeper.max.in.flight.requests = 10
  zookeeper.session.timeout.ms = 6000
  zookeeper.set.acl = false
  zookeeper.sync.time.ms = 2000
 (kafka.server.KafkaConfig)
[2018-05-11 17:31:26,997] INFO KafkaConfig values: 
  advertised.host.name = null
  advertised.listeners = null
  advertised.port = null
  alter.config.policy.class.name = null
  alter.log.dirs.replication.quota.window.num = 11
  alter.log.dirs.replication.quota.window.size.seconds = 1
  authorizer.class.name = 
  auto.create.topics.enable = true
  auto.leader.rebalance.enable = true
  background.threads = 10
  broker.id = 0
  broker.id.generation.enable = true
  broker.rack = null
  compression.type = producer
  connections.max.idle.ms = 600000
  controlled.shutdown.enable = true
  controlled.shutdown.max.retries = 3
  controlled.shutdown.retry.backoff.ms = 5000
  controller.socket.timeout.ms = 30000
  create.topic.policy.class.name = null
  default.replication.factor = 1
  delegation.token.expiry.check.interval.ms = 3600000
  delegation.token.expiry.time.ms = 86400000
  delegation.token.master.key = null
  delegation.token.max.lifetime.ms = 604800000
  delete.records.purgatory.purge.interval.requests = 1
  delete.topic.enable = true
  fetch.purgatory.purge.interval.requests = 1000
  group.initial.rebalance.delay.ms = 0
  group.max.session.timeout.ms = 300000
  group.min.session.timeout.ms = 6000
  host.name = 
  inter.broker.listener.name = null
  inter.broker.protocol.version = 1.1-IV0
  leader.imbalance.check.interval.seconds = 300
  leader.imbalance.per.broker.percentage = 10
  listener.security.protocol.map = PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SSL
  listeners = null
  log.cleaner.backoff.ms = 15000
  log.cleaner.dedupe.buffer.size = 134217728
  log.cleaner.delete.retention.ms = 86400000
  log.cleaner.enable = true
  log.cleaner.io.buffer.load.factor = 0.9
  log.cleaner.io.buffer.size = 524288
  log.cleaner.io.max.bytes.per.second = 1.7976931348623157E308
  log.cleaner.min.cleanable.ratio = 0.5
  log.cleaner.min.compaction.lag.ms = 0
  log.cleaner.threads = 1
  log.cleanup.policy = [delete]
  log.dir = /tmp/kafka-logs
  log.dirs = /tmp/kafka-logs
  log.flush.interval.messages = 9223372036854775807
  log.flush.interval.ms = null
  log.flush.offset.checkpoint.interval.ms = 60000
  log.flush.scheduler.interval.ms = 9223372036854775807
  log.flush.start.offset.checkpoint.interval.ms = 60000
  log.index.interval.bytes = 4096
  log.index.size.max.bytes = 10485760
  log.message.format.version = 1.1-IV0
  log.message.timestamp.difference.max.ms = 9223372036854775807
  log.message.timestamp.type = CreateTime
  log.preallocate = false
  log.retention.bytes = -1
  log.retention.check.interval.ms = 300000
  log.retention.hours = 168
  log.retention.minutes = null
  log.retention.ms = null
  log.roll.hours = 168
  log.roll.jitter.hours = 0
  log.roll.jitter.ms = null
  log.roll.ms = null
  log.segment.bytes = 1073741824
  log.segment.delete.delay.ms = 60000
  max.connections.per.ip = 2147483647
  max.connections.per.ip.overrides = 
  max.incremental.fetch.session.cache.slots = 1000
  message.max.bytes = 1000012
  metric.reporters = []
  metrics.num.samples = 2
  metrics.recording.level = INFO
  metrics.sample.window.ms = 30000
  min.insync.replicas = 1
  num.io.threads = 8
  num.network.threads = 3
  num.partitions = 1
  num.recovery.threads.per.data.dir = 1
  num.replica.alter.log.dirs.threads = null
  num.replica.fetchers = 1
  offset.metadata.max.bytes = 4096
  offsets.commit.required.acks = -1
  offsets.commit.timeout.ms = 5000
  offsets.load.buffer.size = 5242880
  offsets.retention.check.interval.ms = 600000
  offsets.retention.minutes = 1440
  offsets.topic.compression.codec = 0
  offsets.topic.num.partitions = 50
  offsets.topic.replication.factor = 1
  offsets.topic.segment.bytes = 104857600
  password.encoder.cipher.algorithm = AES/CBC/PKCS5Padding
  password.encoder.iterations = 4096
  password.encoder.key.length = 128
  password.encoder.keyfactory.algorithm = null
  password.encoder.old.secret = null
  password.encoder.secret = null
  port = 9092
  principal.builder.class = null
  producer.purgatory.purge.interval.requests = 1000
  queued.max.request.bytes = -1
  queued.max.requests = 500
  quota.consumer.default = 9223372036854775807
  quota.producer.default = 9223372036854775807
  quota.window.num = 11
  quota.window.size.seconds = 1
  replica.fetch.backoff.ms = 1000
  replica.fetch.max.bytes = 1048576
  replica.fetch.min.bytes = 1
  replica.fetch.response.max.bytes = 10485760
  replica.fetch.wait.max.ms = 500
  replica.high.watermark.checkpoint.interval.ms = 5000
  replica.lag.time.max.ms = 10000
  replica.socket.receive.buffer.bytes = 65536
  replica.socket.timeout.ms = 30000
  replication.quota.window.num = 11
  replication.quota.window.size.seconds = 1
  request.timeout.ms = 30000
  reserved.broker.max.id = 1000
  sasl.enabled.mechanisms = [GSSAPI]
  sasl.jaas.config = null
  sasl.kerberos.kinit.cmd = /usr/bin/kinit
  sasl.kerberos.min.time.before.relogin = 60000
  sasl.kerberos.principal.to.local.rules = [DEFAULT]
  sasl.kerberos.service.name = null
  sasl.kerberos.ticket.renew.jitter = 0.05
  sasl.kerberos.ticket.renew.window.factor = 0.8
  sasl.mechanism.inter.broker.protocol = GSSAPI
  security.inter.broker.protocol = PLAINTEXT
  socket.receive.buffer.bytes = 102400
  socket.request.max.bytes = 104857600
  socket.send.buffer.bytes = 102400
  ssl.cipher.suites = []
  ssl.client.auth = none
  ssl.enabled.protocols = [TLSv1.2, TLSv1.1, TLSv1]
  ssl.endpoint.identification.algorithm = null
  ssl.key.password = null
  ssl.keymanager.algorithm = SunX509
  ssl.keystore.location = null
  ssl.keystore.password = null
  ssl.keystore.type = JKS
  ssl.protocol = TLS
  ssl.provider = null
  ssl.secure.random.implementation = null
  ssl.trustmanager.algorithm = PKIX
  ssl.truststore.location = null
  ssl.truststore.password = null
  ssl.truststore.type = JKS
  transaction.abort.timed.out.transaction.cleanup.interval.ms = 60000
  transaction.max.timeout.ms = 900000
  transaction.remove.expired.transaction.cleanup.interval.ms = 3600000
  transaction.state.log.load.buffer.size = 5242880
  transaction.state.log.min.isr = 1
  transaction.state.log.num.partitions = 50
  transaction.state.log.replication.factor = 1
  transaction.state.log.segment.bytes = 104857600
  transactional.id.expiration.ms = 604800000
  unclean.leader.election.enable = false
  zookeeper.connect = localhost:2181
  zookeeper.connection.timeout.ms = 6000
  zookeeper.max.in.flight.requests = 10
  zookeeper.session.timeout.ms = 6000
  zookeeper.set.acl = false
  zookeeper.sync.time.ms = 2000
 (kafka.server.KafkaConfig)
[2018-05-11 17:31:27,010] INFO [ThrottledRequestReaper-Fetch]: Starting (kafka.server.ClientQuotaManager$ThrottledRequestReaper)
[2018-05-11 17:31:27,010] INFO [ThrottledRequestReaper-Produce]: Starting (kafka.server.ClientQuotaManager$ThrottledRequestReaper)
[2018-05-11 17:31:27,011] INFO [ThrottledRequestReaper-Request]: Starting (kafka.server.ClientQuotaManager$ThrottledRequestReaper)
[2018-05-11 17:31:27,024] INFO Log directory '/tmp/kafka-logs' not found, creating it. (kafka.log.LogManager)
[2018-05-11 17:31:27,029] INFO Loading logs. (kafka.log.LogManager)
[2018-05-11 17:31:27,032] INFO Logs loading complete in 3 ms. (kafka.log.LogManager)
[2018-05-11 17:31:27,038] INFO Starting log cleanup with a period of 300000 ms. (kafka.log.LogManager)
[2018-05-11 17:31:27,039] INFO Starting log flusher with a default period of 9223372036854775807 ms. (kafka.log.LogManager)
[2018-05-11 17:31:27,232] INFO Awaiting socket connections on 0.0.0.0:9092. (kafka.network.Acceptor)
[2018-05-11 17:31:27,251] INFO [SocketServer brokerId=0] Started 1 acceptor threads (kafka.network.SocketServer)
[2018-05-11 17:31:27,260] INFO [ExpirationReaper-0-Produce]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,261] INFO [ExpirationReaper-0-Fetch]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,261] INFO [ExpirationReaper-0-DeleteRecords]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,267] INFO [LogDirFailureHandler]: Starting (kafka.server.ReplicaManager$LogDirFailureHandler)
[2018-05-11 17:31:27,287] INFO Creating /brokers/ids/0 (is it secure? false) (kafka.zk.KafkaZkClient)
[2018-05-11 17:31:27,317] INFO Result of znode creation at /brokers/ids/0 is: OK (kafka.zk.KafkaZkClient)
[2018-05-11 17:31:27,319] INFO Registered broker 0 at path /brokers/ids/0 with addresses: ArrayBuffer(EndPoint(asus-GL553VD,9092,ListenerName(PLAINTEXT),PLAINTEXT)) (kafka.zk.KafkaZkClient)
[2018-05-11 17:31:27,322] WARN No meta.properties file under dir /tmp/kafka-logs/meta.properties (kafka.server.BrokerMetadataCheckpoint)
[2018-05-11 17:31:27,427] INFO [ExpirationReaper-0-topic]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,429] INFO [ExpirationReaper-0-Heartbeat]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,429] INFO [ExpirationReaper-0-Rebalance]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
[2018-05-11 17:31:27,430] INFO Creating /controller (is it secure? false) (kafka.zk.KafkaZkClient)
[2018-05-11 17:31:27,442] INFO Result of znode creation at /controller is: OK (kafka.zk.KafkaZkClient)
[2018-05-11 17:31:27,445] INFO [GroupCoordinator 0]: Starting up. (kafka.coordinator.group.GroupCoordinator)
[2018-05-11 17:31:27,445] INFO [GroupCoordinator 0]: Startup complete. (kafka.coordinator.group.GroupCoordinator)
[2018-05-11 17:31:27,446] INFO [GroupMetadataManager brokerId=0] Removed 0 expired offsets in 1 milliseconds. (kafka.coordinator.group.GroupMetadataManager)
[2018-05-11 17:31:27,466] INFO [ProducerId Manager 0]: Acquired new producerId block (brokerId:0,blockStartProducerId:0,blockEndProducerId:999) by writing to Zk with path version 1 (kafka.coordinator.transaction.ProducerIdManager)
[2018-05-11 17:31:27,476] INFO [TransactionCoordinator id=0] Starting up. (kafka.coordinator.transaction.TransactionCoordinator)
[2018-05-11 17:31:27,477] INFO [Transaction Marker Channel Manager 0]: Starting (kafka.coordinator.transaction.TransactionMarkerChannelManager)
[2018-05-11 17:31:27,477] INFO [TransactionCoordinator id=0] Startup complete. (kafka.coordinator.transaction.TransactionCoordinator)
[2018-05-11 17:31:27,496] INFO [/config/changes-event-process-thread]: Starting (kafka.common.ZkNodeChangeNotificationListener$ChangeEventProcessThread)
[2018-05-11 17:31:27,503] INFO Kafka version : 1.1.0 (org.apache.kafka.common.utils.AppInfoParser)
[2018-05-11 17:31:27,503] INFO Kafka commitId : fdcf75ea326b8e07 (org.apache.kafka.common.utils.AppInfoParser)
[2018-05-11 17:31:27,504] INFO [KafkaServer id=0] started (kafka.server.KafkaServer)
~~~

### Step 3: Create a topic

* Create a sample topic called `shrey_test`

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/kafka-topics.sh \
  --create \
  --zookeeper localhost:2181 \
  --replication-factor 1 \
  --partitions 1 \
  --topic shrey_test

WARNING: Due to limitations in metric names, topics with a period ('.') or underscore ('_') could collide. To avoid issues it is best to use either, but not both.
Created topic "shrey_test".
~~~

* Verify newly created topic from command line

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/kafka-topics.sh \
  --list \
  --zookeeper localhost:2181

shrey_test  
~~~

* Verify newly created topic under file system

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ cd /tmp/kafka-logs

asus@asus-GL553VD:/tmp/kafka-logs$ ls -ltr -R
.:
total 20
-rw-rw-r-- 1 asus asus    0 May 11 17:31 cleaner-offset-checkpoint
-rw-rw-r-- 1 asus asus   54 May 11 17:31 meta.properties
drwxrwxr-x 2 asus asus 4096 May 11 17:41 shrey_test-0
-rw-rw-r-- 1 asus asus   19 May 11 17:45 recovery-point-offset-checkpoint
-rw-rw-r-- 1 asus asus    4 May 11 17:45 log-start-offset-checkpoint
-rw-rw-r-- 1 asus asus   19 May 11 17:46 replication-offset-checkpoint

./shrey_test-0:
total 0
-rw-rw-r-- 1 asus asus        0 May 11 17:41 leader-epoch-checkpoint
-rw-rw-r-- 1 asus asus        0 May 11 17:41 00000000000000000000.log
-rw-rw-r-- 1 asus asus 10485760 May 11 17:41 00000000000000000000.index
-rw-rw-r-- 1 asus asus 10485756 May 11 17:41 00000000000000000000.timeindex
~~~

### Step-4: Publish some messages

* Kafka comes with a command line client that will take input from a file or from standard input and send it out as messages to the Kafka cluster (By default, each line will be sent as a separate message)

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/kafka-console-producer.sh \
  --broker-list localhost:9092 \
  --topic shrey_test

>This is a first message
>Another message
>Hi 
>Hello World!!!!!
~~~

### Step-4: Start a consumer

* Kafka also has a command line consumer that will dump out messages to standard output.

~~~
asus@asus-GL553VD:~/tech_soft/kafka_2.11-1.1.0$ bin/kafka-console-consumer.sh \
  --bootstrap-server localhost:9092 \
  --topic shrey_test \
  --from-beginning

This is a first message
Another message
Hi 
Hello World!!!!!
~~~

### Step-5: Verify kafka logs

~~~
asus@asus-GL553VD:/tmp/kafka-logs/shrey_test-0$ ls -ltr
total 8

-rw-rw-r-- 1 asus asus 10485760 May 11 17:41 00000000000000000000.index
-rw-rw-r-- 1 asus asus 10485756 May 11 17:41 00000000000000000000.timeindex
-rw-rw-r-- 1 asus asus        8 May 11 17:48 leader-epoch-checkpoint
-rw-rw-r-- 1 asus asus      506 May 11 17:51 00000000000000000000.log
~~~

## Typical Use Cases

* **Messaging** - Kafka works well as a replacement for a more traditional message broker 

* **Website Activity Tracking** - Activity tracking is often very high volume as many activity messages are generated for each user page view

* **Metrics** - Kafka is often used for operational monitoring data

* **Log Aggregation** - Many people use Kafka as a replacement for a log aggregation solution (Use of flume & kafka complements each other for this use case)

* **Stream Processing** - Apart from Kafka Streams, alternative open source stream processing tools include Apache Storm, Apache Samza, Apache Spark, Apache Flink etc.
