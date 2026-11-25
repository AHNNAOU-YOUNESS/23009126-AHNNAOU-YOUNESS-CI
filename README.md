# CI02 — Prévision de l'indice des quantités de blé importées au Maroc

Projet de régression sur série temporelle, réalisé dans le cadre de la filière Commerce International (ENCG Settat, UHP1), année universitaire 2026–2027.

| | |
|---|---|
| **Étudiant** | AHNNAOU Youness — Apogée 23009126 |
| **Professeur** | Abderrahim Larhlimi |
| **Sujet** | CI02 — Prévision des importations agricoles (catégorie A, régression et prévision) |
| **Source des données** | FAOSTAT, domaine *Trade Indices* (export du 19/11/2026) |

## Problématique

> Comment prévoir l'évolution des quantités annuelles de blé importées par le Maroc à partir de l'historique des échanges commerciaux ?

- **Périmètre :** un pays (Maroc), un produit (blé), fréquence annuelle, 64 observations (1961–2024).
- **Cible :** l'**indice des quantités importées** (base 100 = 2014–2016), et non un tonnage. Toutes les erreurs sont exprimées en points d'indice.
- **Critère de réussite :** battre la référence naïve (valeur de l'année précédente) en MAE et en RMSE.

## Méthode en bref

- **Variables :** les valeurs des 3 années précédentes (`lag1`, `lag2`, `lag3`).
- **Découpage chronologique :** entraînement 1964–2005 (42), validation 2006–2014 (9), test 2015–2024 (10). Aucun mélange aléatoire.
- **Modèles :** référence naïve, Ridge (α choisi sur la validation parmi 0,1 / 1 / 10 / 100), Random Forest (200 arbres, profondeur 4).
- **Test utilisé une seule fois**, après réentraînement sur entraînement + validation.
- **Graine aléatoire :** 42.

## Résultats principaux (test 2015–2024)

| Modèle | MAE | RMSE | R² |
|---|---:|---:|---:|
| **Ridge** (α = 0,1) | **22,47** | **28,59** | −0,75 |
| Random Forest | 23,65 | 29,64 | −0,88 |
| Naïf (année précédente) | 25,90 | 33,21 | −1,36 |

- Ridge est le meilleur des trois, avec environ 13 % de MAE en moins que la référence naïve.
- Les R² sont tous négatifs : aucun modèle ne fait mieux que la moyenne des valeurs du test. Le gain reste modeste et le classement est indicatif (10 années de test, un seul découpage).
- Prévision exploratoire pour 2025 : environ 120,3 points d'indice, à lire comme un ordre de grandeur incertain.

Ces valeurs proviennent de l'exécution du notebook. Elles se reproduisent en le réexécutant avec le même fichier CSV.

## Structure du dépôt

```
.
├── README.md
├── DECLARATION_IA.md          # déclaration d'utilisation de l'IA
├── requirements.txt           # dépendances Python
├── data/
│   └── raw/                   # CSV FAOSTAT original (FAOSTAT_data_en_11-19-2026.csv)
├── notebooks/
│   └── projet_CI02.ipynb      # notebook Google Colab exécuté de bout en bout
├── figures/                   # graphiques et tableaux produits par le notebook
├── rapport/
│   ├── rapport.pdf            # rapport PDF
│   └── rapport.tex            # source LaTeX (XeLaTeX)
├── presentation/              # 6 diapositives : PDF + source PPTX
├── video/                     # script et vidéo explicative individuelle (60 à 90 s)
└── docs/                      # fiche du sujet et références (Markdown)
```

## Exécution

### Sur Google Colab (recommandé)

1. Placer le CSV dans Google Drive, par exemple dans `MyDrive/CC PARTIE B/`.
2. Ouvrir `notebooks/projet_CI02.ipynb` dans Colab et exécuter les cellules dans l'ordre. Le notebook monte Google Drive automatiquement.
3. Si le fichier est ailleurs, modifier la variable au début du notebook :

```python
DATA_PATH = "/content/drive/MyDrive/CC PARTIE B/FAOSTAT_data_en_11-19-2026.csv"
```

### En local

```bash
pip install -r requirements.txt
```

Dans le notebook, remplacer `DATA_PATH` par le chemin relatif du CSV (`data/raw/FAOSTAT_data_en_11-19-2026.csv`), puis exécuter toutes les cellules. Hors Colab, le montage de Drive est ignoré automatiquement.

### Compiler le rapport

```bash
cd rapport
xelatex rapport.tex && xelatex rapport.tex
```

Le dossier `figures/` doit se trouver à côté de `rapport.tex`.

## Limites

- Peu d'observations (64 années, 10 pour le test) et un seul découpage évalué.
- Chocs climatiques et commerciaux non modélisés ; aucune variable explicative externe.
- Cible exprimée en indice : elle ne donne pas directement les volumes en tonnes.
- Une bonne performance hors échantillon n'établit pas de relation causale.
- Projet pédagogique : les prévisions ne doivent pas servir à une décision commerciale ou économique réelle.

## Utilisation de l'IA

Un assistant d'IA a été utilisé pour une partie du travail (cadrage, aide au code, préparation des livrables). Le détail est donné dans [`DECLARATION_IA.md`](DECLARATION_IA.md).

## Source des données

FAOSTAT — Organisation des Nations unies pour l'alimentation et l'agriculture (FAO), domaine *Trade Indices* : <https://www.fao.org/faostat>. Les données restent soumises aux conditions d'utilisation de la FAO.
