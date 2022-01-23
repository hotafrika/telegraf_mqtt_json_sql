# telegraf_mqtt_json_sql

```bash
mosquitto_sub -h localhost -t house/sensors/data
mosquitto_pub -h localhost -t house/sensors/data -m "{\"sensorID\": \"14:7D:DA:6C:C8:37\", \"timestamp\": 1642785655.682983, \"value\": 68.3, \"type\": 1}"
```

```bash
su postgres
CREATE DATABASE mqttdata;
CREATE USER mqttuser WITH ENCRYPTED PASSWORD 'mqttpass';
GRANT ALL PRIVILEGES ON DATABASE mqttdata TO mqttuser;
```

```bash
psql mqttuser -h 127.0.0.1 -d mqttdata
create table metrics (device_id varchar(17) not null, timestamp timestamp not null, value float not null, type smallint not null);
psql mqttuser -h 127.0.0.1 -d mqttdata -c "select * from metrics"
```

			