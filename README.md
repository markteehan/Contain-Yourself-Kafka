# Contain-Yourself-Kafka
docker-compose for various Apache Kafka and Confluent configs - handy for demos and POCs



* [MySQL to Kafka](01_mySQL_to_ConfluentCloud)
A containerized Kafka Connect to stream tables from a MySQL database to topics in Apache Kafka.
When MySQL is configured to deny external access, apps must run locally alongside the database on the same VM.
This Kafka Connect container will auto-create the topics for the listed tables, register schemas and stream database rows as kafka messages.

* [Coming Soon ](#Coming_Soon)


## Requirements
docker-compose is used for all containers
Internet access to pull container images, confluent-hub setup and various required wgets
Various inbound/outbound ports are needed; listed for each container
VM recommendation for Kafka Connect is at least 16GB RAM
Kafka Connect REST: port 8083 (reconfigurable)
