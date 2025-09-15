# TP étudiants 2025

## Prérequis
- Docker + Docker Compose.
- Prendre un moment pour comprendre le docker-compose.yml

## Démarrage rapide
```bash
docker compose up -d
docker compose logs telegraf -f
```

## Questions de TP

1. Comment est organisé le fichier docker_compose.yml
2. A la lecture du fichier docker_compose.yml expliquez l'organisation de l'application. Faites un schéma simple des relations des différents services.
3. Prenez un paragraphe "environment" d'un des services kafka et décrivez toutes les lignes.
4. Cherchez ce qu'est jolokia2 ?
5. Quel service va t il offrir et à qui ? 
6. Expliquez la fonction du service Telegraf et les élements principaux de sa configuration dans notre exemple.
7. Quel topic est utilisé dans cette application.
8. Quel bucket est utilisé dans cette application.
9. Quels sont les grandes familles de métriques dont on a la métrologie ? 
10. Sachant que la plupart des courbes disponibles pour ces measurements vont être des courbes globalement continuellement ascendantes, quel proposez vous comme fonction d'agrégation pour construite des graphiques mettant en valeur les variations.
11. Au moyen d'une telle fonction montrez ce qu'ils se passe lors de la perte d'un broker puis après quelques minutes sont retour. Vous pourrez par exemplke vous aider des commandes **docker pause kafka-2**" et **docker unpause kafka-2**". Mettez en évidence les measurements affectés au moyen d'un dashboard. Vous mettrez la requête correspondante en "Flux" d'influxDB.
12. Explorez d'autres métriques et imaginez des cas d'usages. Illustrez vos propositions par la capture d'écran du dashboard ainsi que sa requête "Flux".