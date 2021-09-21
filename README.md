# debezium-mysql
An example using debezium and mysql with docker-compose

### The docker compose starts the Zookeeper, Kafka, Mysql and Debezium Connect.

#### After the containers getting healthy you can create a new connector, listening changes into mysql inventory database.
```
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d '{ "name": "inventory-connector", "config": { "connector.class": "io.debezium.connector.mysql.MySqlConnector", "tasks.max": "1", "database.hostname": "mysql", "database.port": "3306", "database.user": "debezium", "database.password": "dbz", "database.server.id": "184054", "database.server.name": "dbserver1", "database.include.list": "inventory", "database.history.kafka.bootstrap.servers": "kafka:9092", "database.history.kafka.topic": "dbhistory.inventory" } }'
```

#### Therefore you can get the connectors calling
```
curl -H "Accept:application/json" localhost:8083/connectors/
```

####  You can also get the connectors by their names
```
curl -i -X GET -H "Accept:application/json" localhost:8083/connectors/inventory-connector
```

#### Instaling python library
```
pip install -r requirements.txt
```

#### Running the python example
```
python kafka-example.py
```

### The aplication listen a topic called "dbserver1.inventory.customers"

#### You can see the columns, the values before and after the changes.
