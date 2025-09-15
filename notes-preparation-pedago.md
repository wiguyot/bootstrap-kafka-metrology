# notes à reprendre plus tard


## Intérêts pédagogiques majeurs

•	Comprendre Kafka “en vrai” mais sans friction : un cluster multi-nœuds en KRaft dès le départ pour expliquer controller quorum, ISR, réplication, partitions — sans se noyer dans l’install.

•	Observabilité dès J1 : JMX→Jolokia→Telegraf→Influx : les étudiants voient l’effet de leurs actions (débit, latence, fetch/produce, ISR) et lient théorie ↔ métriques.

•	Parallélisme & rebalancing : avec 4 consommateurs dans un même group, tu illustres assignment par partitions, scaling horizontal, rebalances (ajout/retrait d’un consumer).

•	Culture Ops/Prod : ports, listeners, ADVERTISED_LISTENERS, santé des services, mémoire JVM, dépendances. On inculque de bons réflexes dev + plateforme.

•	Inspection rapide : Kafdrop rend tangible le contenu du cluster (topics, messages, lag). Ça motive et accélère la boucle essai → observation → déduction.

## Ce que tes apprenants vont manipuler concrètement

•	KRaft & quorum : lire/expliciter PROCESS_ROLES, CONTROLLER_LISTENER_NAMES, CONTROLLER_QUORUM_VOTERS.

•	Topologie & partitions : créer un topic “weather” (p, RF), varier ces paramètres et observer l’impact sur la conso parallèle.

•	Groupes & offsets : constater les lags, l’équilibrage lorsque des consumers arrivent/partent.
•	Métriques Kafka : via Jolokia → Telegraf → Influx (produced/consumed records, request rates, network, ISR, under-replicated, etc.).

•	Ops réseau : différence entre kafka-1:9092 interne et exposition hôte (ports mappés), rôle de ADVERTISED_LISTENERS.


## Idées d’exercices (directement exploitables)

1.	Démarrage & Sanity check (15–20 min)

    •	docker compose up -d

    •	Ouvrir Kafdrop (localhost:9000), vérifier brokers, créer/voir weather.

    •	Valider que init-producer envoie, que les 4 consumers consomment, et lire le lag.

2.	Parallélisme vs partitions (20–30 min)

    •	Recréer weather avec 1, 2, 4, 8 partitions (via topic-init ou kafka-topics).

    •	Observer assignment (1 consumer idle si partitions < consumers), débit total, lag.

    •	Question guidée : “À partir de combien de partitions les 4 consumers travaillent-ils tous ?”

3.	Réplication & ISR (20 min)

    •	Fixer RF=3, générer du trafic.

    •	Stopper kafka-2 (ex.: docker stop kafka-2) → observer ISR, under-replicated partitions et l’impact sur la prod/conso.

    •	Redémarrer kafka-2 et constater le rétablissement (ré-sync ISR).

4.	Rebalancing dynamique (15 min)

    •	Lancer/stopper consumer-4. Observer le rebalance et son effet sur le throughput et l’assignation.

5.	Métriques & diagnostic (25–30 min)

    •	Ouvrir InfluxDB (ou brancher Grafana si tu l’ajoutes) et corréler un événement (arrêt de broker, ajout de partitions) à des courbes (produce/fetch rate, request latency, ISR).
    
    •	Faire décrire par les étudiants quelle métrique ils surveilleraient en prod et pourquoi.