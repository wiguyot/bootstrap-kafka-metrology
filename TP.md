# TP — Métrologie Kafka (JMX/Jolokia → Telegraf → TSDB/Dashboard)

## Objectifs
- Exposer **JMX/Jolokia** des brokers.
- Ingestion via **Telegraf** vers TSDB (Influx/Prom).
- Lire les métriques clefs : **ISR, URO, lag, bytes in/out, req rate**.
- Diagnostiquer un incident contrôlé (broker suspendu).

## Prérequis
- Docker + Docker Compose.
- Accès :
  - Jolokia brokers : `http://<HOST>:<JOLOKIA_PORT>`  <!-- TODO -->
  - Telegraf → TSDB : `http://<HOST>:<TSDB_PORT>`  <!-- TODO -->
  - Dashboard (Grafana/…) : `http://<HOST>:<DASHBOARD_PORT>`  <!-- TODO -->

## Démarrage rapide
```bash
git clone <ce dépôt>
cd bootstrap-kafka-metrology
docker compose up -d
docker compose logs telegraf -f
```

## TP pas à pas

	1.	Vérifier exposition Jolokia (compose/env des brokers).
	2.	Valider Telegraf (inputs.jolokia / outputs.*) vers la TSDB.
	3.	Ouvrir le dashboard (JSON fourni ou import) ; noter 8–10 métriques clefs.
	4.	Incident : lancer le script (ex. suspend_random_broker_loop.sh) s’il est fourni.
	5.	Documenter la trajectoire des métriques pendant l’incident et la reprise.

## Critères de réussite
	•	Dashboard vivant (métriques en flux).
	•	Incident détecté via ≥ 3 métriques.
	•	Fiche d’analyse d’une page (symptôme → métrique → action).