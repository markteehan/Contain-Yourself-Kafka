# Contain-Yourself-Kafka
docker-compose for various Apache Kafka and Confluent configs - handy for demos and POCs



* [MySQL to Kafka](#01_mySQL_to_ConfluentCloud)
A containerized Kafka Connect to stream tables from a MySQL database to topics in Apache Kafka.
When MySQL is configured to deny external access, apps must run locally alongside the database on the same VM.
This Kafka Connect container will auto-create the topics for the listed tables, register schemas and stream database rows as kafka messages.

* [Coming Soon ](#Coming_Soon)

