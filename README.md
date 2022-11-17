### pulsar-aircraft-pinot

Apache Pulsar to Apache Pinot for ADS-B / Aircraft Data

### Create Pinot Schema

````
aircraft 

  alt_baro INT,
  alt_geom INT,
  baro_rate INT,
  category STRING,
  emergency STRING,
  flight VARCHAR,
  gs FLOAT,
  gva INT,
  hex STRING,
  lat FLOAT,
  lon FLOAT,
  mach FLOAT,
  messages INT,
  nac_p INT,
  nac_v INT,
  nav_altitude_mcp INT,
  nav_heading FLOAT,
  nav_qnh FLOAT,
  nic INT,
  nic_baro INT,
  rc INT,
  rssi FLOAT,
  sda INT,
  seen FLOAT,
  seen_post FLOAT,
  sil INT,
  sil_type STRING,
  speed FLOAT,
  squawk INT,
  track FLOAT,
  version INT
 
  

````

### Flink SQL

````
CREATE CATALOG pulsar WITH (
   'type' = 'pulsar-catalog',
   'catalog-service-url' = 'pulsar://localhost:6650',
   'catalog-admin-url' = 'http://localhost:8080'
);

USE CATALOG pulsar;

SHOW CURRENT DATABASE;
SHOW DATABASES;

set table.dynamic-table-options.enabled = true;

use `public/default`;

show tables;

describe aircraft;


Flink SQL> describe aircraft;
+------------------+--------+------+-----+--------+-----------+
|             name |   type | null | key | extras | watermark |
+------------------+--------+------+-----+--------+-----------+
|         alt_baro |    INT | TRUE |     |        |           |
|         alt_geom |    INT | TRUE |     |        |           |
|        baro_rate |    INT | TRUE |     |        |           |
|         category | STRING | TRUE |     |        |           |
|        emergency | STRING | TRUE |     |        |           |
|           flight | STRING | TRUE |     |        |           |
|               gs | DOUBLE | TRUE |     |        |           |
|              gva |    INT | TRUE |     |        |           |
|              hex | STRING | TRUE |     |        |           |
|              lat | DOUBLE | TRUE |     |        |           |
|              lon | DOUBLE | TRUE |     |        |           |
|             mach | DOUBLE | TRUE |     |        |           |
|         messages |    INT | TRUE |     |        |           |
|            nac_p |    INT | TRUE |     |        |           |
|            nac_v |    INT | TRUE |     |        |           |
| nav_altitude_mcp |    INT | TRUE |     |        |           |
|      nav_heading | DOUBLE | TRUE |     |        |           |
|          nav_qnh | DOUBLE | TRUE |     |        |           |
|              nic |    INT | TRUE |     |        |           |
|         nic_baro |    INT | TRUE |     |        |           |
|               rc |    INT | TRUE |     |        |           |
|             rssi | DOUBLE | TRUE |     |        |           |
|              sda |    INT | TRUE |     |        |           |
|             seen | DOUBLE | TRUE |     |        |           |
|        seen_post | DOUBLE | TRUE |     |        |           |
|              sil |    INT | TRUE |     |        |           |
|         sil_type | STRING | TRUE |     |        |           |
|            speed | DOUBLE | TRUE |     |        |           |
|           squawk |    INT | TRUE |     |        |           |
|            track | DOUBLE | TRUE |     |        |           |
|          version |    INT | TRUE |     |        |           |
+------------------+--------+------+-----+--------+-----------+
31 rows in set


> show create table aircraft;
CREATE TABLE `pulsar`.`public/default`.`aircraft` (
  `alt_baro` INT,
  `alt_geom` INT,
  `baro_rate` INT,
  `category` VARCHAR(2147483647),
  `emergency` VARCHAR(2147483647),
  `flight` VARCHAR(2147483647),
  `gs` DOUBLE,
  `gva` INT,
  `hex` VARCHAR(2147483647),
  `lat` DOUBLE,
  `lon` DOUBLE,
  `mach` DOUBLE,
  `messages` INT,
  `nac_p` INT,
  `nac_v` INT,
  `nav_altitude_mcp` INT,
  `nav_heading` DOUBLE,
  `nav_qnh` DOUBLE,
  `nic` INT,
  `nic_baro` INT,
  `rc` INT,
  `rssi` DOUBLE,
  `sda` INT,
  `seen` DOUBLE,
  `seen_post` DOUBLE,
  `sil` INT,
  `sil_type` VARCHAR(2147483647),
  `speed` DOUBLE,
  `squawk` INT,
  `track` DOUBLE,
  `version` INT
) WITH (
  'connector' = 'pulsar',
  'topics' = 'persistent://public/default/aircraft',
  'format' = 'json',
  'admin-url' = 'http://localhost:8080',
  'service-url' = 'pulsar://localhost:6650'
) 

````

### Apache Pinot References

* https://dev.startree.ai/docs/pinot/recipes/pulsar
* https://github.com/startreedata/pinot-recipes/tree/main/recipes/pulsar
* https://docs.pinot.apache.org/basics/getting-started
* https://docs.pinot.apache.org/basics/components/exploring-pinot
* https://github.com/apache/pinot/blob/master/pinot-tools/src/main/resources/examples/stream/airlineStats/airlineStats_schema.json

### Code References

* https://github.com/tspannhw/pulsar-adsb-function
* https://github.com/tspannhw/FLiP-Py-ADS-B
