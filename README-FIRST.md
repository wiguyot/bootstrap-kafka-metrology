Ce projet sert de démonstrateur à 
- 3 brokers kafka dernière version
- 1 telegraf qui récupère des métriques des brokers et les envoie dans InfluxDB
- 1 InfluxDB 2.7
- 1 initiateur de topic
- 1 producteur pour le topic, tous les 1000 messages s'arrête aléatoirement quelques secondes
- 1 Kafdrop pour visaliser les états classiques de Kafka
- un bash "suspend_random_broker_loop.sh" suspend pendant 1 minute un broker aléatoirement. Le remet en route et patiente 1 mn avant de recommencer le cycle.

Des métrics sont relevés dans les 3 kafkas et sont envoyés dans InfluxDB.

- Kafdrop : http://localhost:9000
- InfluxDB : http://localhost:8086