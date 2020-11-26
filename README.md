# Contain-Yourself-Kafka
docker-compose for various Apache Kafka and Confluent configs - handy for demos and POCs



__01_mySQL_to_ConfluentCloud__
*Containerized Kafka Connect to stream using JDBC from MySQL to Apache Kafka. Single-file setup*
MySQL may be configured to deny external access; so that apps must run locally alongside the database on the same VM.
A containerized Kafka Connect can stream tables from the database to topics in Apache Kafka.

*Description* 
Stream database tables from MySQL to Apache Kafka.
Co-host when external database access cannot be configured.
Open outbount ports 9092 (for the Kafka Brokers) and 443 (Confluent Cloud schema registry)

*Base Container*
confluentinc/cp-kafka-connect

*Container Commands*
- call confluent-hub to install the JDBC Source plugin
- download and unzip the mySQL jarfile required for connection
- submit a JDBCSource job to stream from the database to Confluent Cloud

Kafka Connect will auto-create the topics on dest; for the listed tables as well as the offsets/config/status topics (these will be single-partition).

*Requirements*
- A Confluent Cloud cluster on any cloud provider; with an enabled Schema Registry
- a Confluent Cloud apiKey & Secret; SR basic auth credentials
- open outbound ports 9092 and 443

*Setup*
If you are connecting to a no-auth Kafka system (which is not recommended; but anyway...) then remove all references to these auth properties: (xx_SSL_ENDPOINT_IDENTIFICATION_ALGORITHM, xx_SECURITY_PROTOCOL, xx_SASL_MECHANISM, xx_SASL_JAAS_CONFIG)

- Replace REPLACEME_BOOTSTRAP_SERVERS with your bootstrap servers (for example: pkc-xxxx1.asia-southeast1.gcp.confluent.cloud:9092)
- Replace REPLACEME_APIKEY with your Confluent Cloud API Key (usually a 16 alpha-character UUID). Dont adjust the escaping or quotes.
- Replace REPLACEME_APISECRET with your Confluent Cloud API Key (usually a long alpla-numeric UUID). Dont adjust the escaping or quotes.
- Replace REPLACEME_SR_URL with your Confluent Cloud Schema Registry URL (for example https://psrc-xxxxx.ap-southeast-2.aws.confluent.cloud)
- Replace REPLACEME_SR_AUTH with your (colon-delimited) Confluent CLoud Schema Registry basic Auth (for example XXX:YYYY). Dont add quotes or escape chars.

*Commands*
Start the container | stop the container
`docker-compose up
 docker-compose down`

Check the Kafka Connect logfile
`docker logs kafka-connect`

*credits*
Robin Moffat for the neat technique to pull the mysql jarfile. https://github.com/rmoff




