# CI02 — Prévision de l'indice des importations de blé au Maroc

Projet pédagogique illustratif préparé avec IA ; respecter la consigne de ne pas coder avant la séance d'évaluation.

## Dossiers

- `data/raw/` : CSV FAOSTAT original
- `notebooks/` : notebook Google Colab fourni
- `figures/` : 6 graphiques produits sur la base jointe
- `rapport/` : rapport PDF et tableau des métriques
- `presentation/` : 6 diapositives PowerPoint et PDF
- `video/` : script pour enregistrement individuel (pas de vidéo personnelle fabriquée)

## Exécution

Installer les dépendances :

```bash
pip install -r requirements.txt
```

Ouvrir le notebook sur Google Colab et monter Google Drive.

Chemin du fichier CSV :

```python
DATA_PATH = "/content/drive/MyDrive/CC PARTIE B/FAOSTAT_data_en_11-19-2026.csv"
```

Les résultats du rapport proviennent du protocole documenté dans le rapport et doivent être vérifiés par exécution du notebook.

## Attention

La cible est un indice de quantité importée, base 2014–2016 = 100, et non un volume en tonnes.

Vérifier les droits de redistribution avant de publier le CSV sur GitHub.

Le dépôt GitHub, les trois commits durant la séance et le tag `remise-finale` sont à créer par l'étudiant.
