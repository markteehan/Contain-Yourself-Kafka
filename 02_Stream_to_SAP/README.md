

# MySQL to Kafka
*Containerized Kafka Connect to stream using JDBC from MySQL to Apache Kafka. Single-file setup*

MySQL may be configured to deny external access so that apps must run locally alongside the database on the same VM.
A local containerized Kafka Connect can stream tables from the database to topics in Apache Kafka.
Kafka Connect will auto-create the topics on dest; for the listed tables as well as the offsets/config/status topics (these will be single-partition).
This example streams to Confluent Cloud - See "Setup" for property substitution to stream to any Apache Kafka system.


## Networking
Open outbount ports 9092 (for the Kafka Brokers) and 443 (Confluent Cloud schema registry; or your equivalent)


## Base Container
[confluentinc/cp-kafka-connect](https://hub.docker.com/r/confluentinc/cp-kafka-connect)
Licensed under the Apache 2 license.


## Container Commands
This docker-compose modifies the container commands:
- call confluent-hub to install the JDBC Source plugin
- download and unzip the mySQL jarfile required for connection
- iterate and check while Kafka Connect starts up
- submit a JDBCSource job to stream from the database to Confluent Cloud
- Resume standard container commands


## Requirements
- An Apache Kafka target system. This examples uses a [Confluent Cloud](https://www.confluent.io/confluent-cloud/tryfree) cluster (any region, any cloud provider); with an enabled Schema Registry
- a Confluent Cloud apiKey & Secret; SR basic auth credentials
- open outbound ports 9092 and 443 on the MySQL VM


## Setup
If you are connecting to a no-auth Kafka system (which is not recommended; but anyway...) then remove all references to these auth properties: (xx_SSL_ENDPOINT_IDENTIFICATION_ALGORITHM, xx_SECURITY_PROTOCOL, xx_SASL_MECHANISM, xx_SASL_JAAS_CONFIG)
```
Replace...
- REPLACEME_BOOTSTRAP_SERVERS with your bootstrap servers (for example: pkc-xxxx1.asia-southeast1.gcp.confluent.cloud:9092)
- REPLACEME_APIKEY with your Confluent Cloud API Key (usually a 16 alpha-character UUID). Dont adjust the escaping or quotes.
- REPLACEME_APISECRET with your Confluent Cloud API Key (usually a long alpla-numeric UUID). Dont adjust the escaping or quotes.
- REPLACEME_SR_URL with your Confluent Cloud Schema Registry URL (for example https://psrc-xxxxx.ap-southeast-2.aws.confluent.cloud)
- REPLACEME_SR_AUTH with your (colon-delimited) Confluent CLoud Schema Registry basic Auth (for example XXX:YYYY). Dont add quotes or escape chars.
- REPLACEME_DB_HOSTNAME with the name of the mySQL database server (for example mysql-hostname)
- REPLACEME_DBNAME with the mySQL database name (for example my-database)
- REPLACEME_TABLE with the mySQL table name (for example dept)
```


## Commands

Start/Stop the container

`docker-compose up
 docker-compose down`

Check the Kafka Connect logfile

`docker logs kafka-connect`


## Credits

Robin Moffat for the neat technique to pull the mysql jarfile and wait for Connect to startup. https://github.com/rmoff
