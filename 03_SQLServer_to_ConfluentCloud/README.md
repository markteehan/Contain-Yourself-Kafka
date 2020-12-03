

# SQLServer (CDC) to Kafka
*Containerized Kafka Connect to stream from SQLServer (CDC) to Apache Kafka. *

Stream from a SQLServer database to Confluent Cloud using the Debezium CDC connector
Kafka Connect will auto-create the topics on Kafka for the listed tables.
This example streams to Confluent Cloud - See "Setup" for property substitution to stream to any Apache Kafka system.


## Networking
Open outbount ports 9092 (for the Kafka Brokers) and 443 (Confluent Cloud schema registry; or your equivalent)


## Base Container
[confluentinc/cp-kafka-connect](https://hub.docker.com/r/confluentinc/cp-kafka-connect)
Licensed under the Apache 2 license.


## Container Commands
This docker-compose modifies the container commands:
- call confluent-hub to install the Debezium SQLServer CDC connector
- iterate and check while Kafka Connect starts up
- submit a SQLServer CDC job to stream from the database to Confluent Cloud
- Resume standard container commands


## Requirements
- An Apache Kafka target system. This examples uses a [Confluent Cloud](https://www.confluent.io/confluent-cloud/tryfree) cluster (any region, any cloud provider); with an enabled Schema Registry
- a Confluent Cloud apiKey & Secret; SR basic auth credentials
- open outbound ports 9092 and 443


## Setup
edit "setenv" to set values for the required keys
If you are connecting to a no-auth Kafka system (which is not recommended; but anyway...) then remove all references to these auth properties: (xx_SSL_ENDPOINT_IDENTIFICATION_ALGORITHM, xx_SECURITY_PROTOCOL, xx_SASL_MECHANISM, xx_SASL_JAAS_CONFIG)
```
Replace...

- REPLACEME_BOOTSTRAP_SERVERS with your bootstrap servers (for example: pkc-xxxx1.asia-southeast1.gcp.confluent.cloud:9092)
- REPLACEME_APIKEY with your Confluent Cloud API Key (usually a 16 alpha-character UUID). Dont adjust the escaping or quotes.
- REPLACEME_APISECRET with your Confluent Cloud API Key (usually a long alpla-numeric UUID). Dont adjust the escaping or quotes.
- REPLACEME_SR_URL with your Confluent Cloud Schema Registry URL (for example https://psrc-xxxxx.ap-southeast-2.aws.confluent.cloud)
- REPLACEME_SR_AUTH with your (colon-delimited) Confluent CLoud Schema Registry basic Auth (for example XXX:YYYY). Dont add quotes or escape chars.
- REPLACEME_DATABASE_HOSTNAME with the hostname of the SQLServer database
- REPLACEME_DATABASE_SERVER_NAME with the server name of the SQLServer database server
- REPLACEME_DBNAME with the database name
- REPLACEME_DATABASE_USER with the username
- REPLACEME_DATABASE_PASSWORD with the password

```


## Commands

Start/Stop the container

`docker-compose up
 docker-compose down`

Check the Kafka Connect logfile

`docker logs kafka-connect`


