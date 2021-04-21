# AMQ Broker

Run Locally

```
docker run -it --rm -p 8161:8161 -p 61616:61616 -p 5672:5672 -e ARTEMIS_USERNAME=quarkus -e ARTEMIS_PASSWORD=quarkus vromero/activemq-artemis:2.11.0-alpine
```

Generate Keys

```
keytool -genkey -alias broker -keyalg RSA -keystore broker.ks
keytool -export -alias broker -keystore broker.ks -file broker_cert
keytool -import -alias broker -keystore client.ts -file broker_cert
keytool -genkey -alias broker -keyalg RSA -keystore broker.ts
```

```
oc create secret generic ex-aao-amqp-secret \
--from-file=broker.ks \
--from-literal=keyStorePassword=password \
--from-file=client.ts=broker.ts \
--from-literal=trustStorePassword=password
```

-Djavax.net.ssl.trustStore=/Users/stephennimmo/Projects/github/stephennimmo/amq-example/amq-broker/client.ts -Djavax.net.ssl.trustStorePassword=password