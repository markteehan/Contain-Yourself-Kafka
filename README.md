# Contain-Yourself-Kafka
docker-compose for various Apache Kafka and Confluent configs - handy for demos and POCs



* [JDBC MySQL to Kafka](01_mySQL_to_ConfluentCloud)
A containerized Kafka Connect to stream tables from a MySQL database to topics in Apache Kafka.
When MySQL is configured to deny external access, apps must run locally alongside the database on the same VM.
This Kafka Connect container will auto-create the topics for the listed tables, register schemas and stream database rows as kafka messages.

* [Stream to SAP - Coming Soon ](#Coming_Soon)
Coming soon...

* [CDC SQLServer to Kafka](03_SQLServer_to_ConfluentCloud)
Containerized Kafka Connect to stream from SQLServer (CDC) to Apache Kafka.
This Kafka Connect container will auto-create the topics for the listed tables, register schemas and stream database rows as kafka messages.

## Requirements
```
docker-compose is used for all containers
Internet access s needed to pull container images, confluent-hub setup and various jarfile wgets
Various firewall exclusion inbound/outbound ports are needed; listed for each container
Kafka Connect: at least 8GB RAM (16GB recommended)
Kafka Connect REST: port 8083 (reconfigurable)
```
