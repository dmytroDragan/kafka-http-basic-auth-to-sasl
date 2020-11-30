#Example of not working principal propagation from Basic Auth to SASL for multiple users

## Issue

For principal mapping rest server should have multiple login modules in KafkaClient jaas.
Having multiple login modules in KafkaClient jaas create SASLException on "kafka is ready" step.

```
[kafka-admin-client-thread | adminclient-1] INFO org.apache.kafka.common.network.Selector - [AdminClient clientId=adminclient-1] Failed authentication with kafka-2/172.24.0.4 (Authentication failed: Invalid username or password)
[kafka-admin-client-thread | adminclient-1] ERROR org.apache.kafka.clients.NetworkClient - [AdminClient clientId=adminclient-1] Connection to node -1 (kafka-2/172.24.0.4:9093) failed authentication due to: Authentication failed: Invalid username or password
[kafka-admin-client-thread | adminclient-1] WARN org.apache.kafka.clients.admin.internals.AdminMetadataManager - [AdminClient clientId=adminclient-1] Metadata update failed due to authentication error
org.apache.kafka.common.errors.SaslAuthenticationException: Authentication failed: Invalid username or password
[main] ERROR io.confluent.admin.utils.ClusterStatus - Error while getting broker list.
java.util.concurrent.ExecutionException: org.apache.kafka.common.errors.SaslAuthenticationException: Authentication failed: Invalid username or password
        at org.apache.kafka.common.internals.KafkaFutureImpl.wrapAndThrow(KafkaFutureImpl.java:45)
        at org.apache.kafka.common.internals.KafkaFutureImpl.access$000(KafkaFutureImpl.java:32)
        at org.apache.kafka.common.internals.KafkaFutureImpl$SingleWaiter.await(KafkaFutureImpl.java:89)
        at org.apache.kafka.common.internals.KafkaFutureImpl.get(KafkaFutureImpl.java:260)
        at io.confluent.admin.utils.ClusterStatus.isKafkaReady(ClusterStatus.java:149)
        at io.confluent.admin.utils.cli.KafkaReadyCommand.main(KafkaReadyCommand.java:150)
Caused by: org.apache.kafka.common.errors.SaslAuthenticationException: Authentication failed: Invalid username or password
```
## How to run
1. Create certificates (Type 'yes' for each trust certificate request)
```
cd security
./create_certs.sh
```
2. Run docker-compose
```
docker-compose up -d
```