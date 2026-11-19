# ERO2

**Étude des comportements de systèmes d’attente**

Ce projet étudie l’effet de différentes règles de priorité sur les performances d’un système de correction automatique, dans le contexte des rendus de TP prépa et de piscine C à EPITA.

L’étude s’appuie sur des données de temps de traitement, des données récupérées depuis l’intra EPITA et des simulations de plusieurs architectures de files d’attente. Le rapport théorique et l’analyse des scénarios sont disponibles dans [`Rapport.pdf`](Rapport.pdf).

## Fonctionnalités clés

- Simulation de l’arrivée et du traitement des tags de rendu
- Comparaison de plusieurs architectures de files d’attente :
  - Waterfall
  - Anti-priority
  - Channels and Dams
  - Calendar Priority
- Paramétrage du nombre de serveurs, des populations et des priorités
- Génération de graphiques et de statistiques par scénario
- Génération d’un tableau récapitulatif à partir des résultats disponibles

## Prérequis

- Python 3.11.14
- `pip`

## Installation et lancement

1. Cloner le dépôt et entrer dans le dossier du backend :

```bash
git clone git@github.com:aziiorn/ERO2.git && cd ERO2/backend
```

2. Lancer la simulation configurée dans `main.py` :

```bash
python -m main
```

La simulation utilise actuellement le cache `pushes_cache.pkl_0.1` s’il est présent. Si ce cache est absent, les tags sont générés à partir des données JSON du dossier `Scrapper/`.

Les résultats de l’exécution sont écrits dans `backend/results/Test/`.

## C’est parti !

À la fin de l’exécution, le dossier `backend/results/Test/` contient les statistiques et les graphiques du scénario, notamment :

- `stats.json`
- `entry_queue.png`
- `exit_queue.png`
- `waiting_time.png`

Les résultats déjà présents pour les autres scénarios sont conservés dans `backend/results/`.

## Générer le tableau récapitulatif

Depuis le dossier `backend`, exécuter :

```bash
python create_tables.py
```

Le tableau LaTeX est généré dans `backend/results/table_all_pop.tex`, à partir des fichiers `stats.json` disponibles pour les scénarios répertoriés dans `create_tables.py`.

## Configuration

Le scénario exécuté par défaut est défini dans `backend/main.py`. On peut notamment y modifier :

- l’architecture de file d’attente ;
- le nombre de serveurs ;
- la taille des files ;
- les priorités et leurs périodes d’application ;
- les paramètres des populations et des temps de traitement.

Les modèles et les paramètres sont principalement définis dans `backend/common/model.py`, `backend/main.py` et les fichiers de `backend/queuing/`.

## Structure du projet

```text
ERO2/
├── backend/
│   ├── common/       # Modèles et fonctions communes
│   ├── pushs/        # Génération des arrivées de tags
│   ├── queuing/      # Architectures de files d’attente
│   ├── results/      # Résultats des scénarios
│   └── main.py       # Configuration et lancement d’une simulation
├── Scrapper/         # Scraper et données d’entrée
├── Rapport.pdf       # Rapport théorique et analyse
└── README.md
```

## Membres du groupe

- Paul Pazart
- Lucas Burgaud
- Kylian Bozec
- Etienne Senigout
- Guillaume Hanry
- Pierre Braud
