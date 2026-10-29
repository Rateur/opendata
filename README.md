<div align="center">
  <h1>Open Data</h1>
  <p>Observatoire de la parité médiatique : <a href="https://opendata2025.netlify.app/">opendata2025.netlify.app</a></p>
  <p>
    <a href="https://github.com/Rateur/opendata/stargazers">
      <img src="https://img.shields.io/github/stars/Rateur/opendata?style=for-the-badge&color=ffb300&logo=github&label=Stars" alt="GitHub Stars">
    </a>
    <a href="https://www.data.gouv.fr/reuses/observatoire-de-la-parite-mediatique">
      <img src="https://img.shields.io/badge/data.gouv.fr-R%C3%A9utilisation-0b7cff?style=for-the-badge" alt="Réutilisation data.gouv.fr">
    </a>
    <a href="https://www.python.org/">
      <img src="https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.13">
    </a>
    <a href="https://pandas.pydata.org/">
      <img src="https://img.shields.io/badge/Pandas-Dataframe-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
    </a>
    <a href="https://jupyter.org/">
      <img src="https://img.shields.io/badge/Jupyter-Lab-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter Lab">
    </a>
    <a href="https://www.chartjs.org/">
      <img src="https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white" alt="Chart.js">
    </a>
    <a href="https://www.netlify.com/">
      <img src="https://img.shields.io/badge/Netlify-00AD9F?style=for-the-badge&logo=netlify&logoColor=white" alt="Netlify">
    </a>
  </p>
</div>

<div align="center">
  <p style="margin: 10px 0 20px; font-weight: 600;">
    <a href="#ce-que-cest">Ce que c'est</a> •
    <a href="#ce-que-le-site-montre">Ce que le site montre</a> •
    <a href="#comment-cest-fait">Comment c'est fait</a> •
    <a href="#lancer-en-local">Lancer en local</a> •
    <a href="#état-et-limites">État et limites</a> •
    <a href="#équipe">Équipe</a>
  </p>
</div>

## Ce que c'est
Une page web qui compare le temps de parole des femmes et des hommes à la télévision et à la radio françaises, en 2019 et en 2020.

Elle a été réalisée en janvier 2026 pour le défi data.gouv.fr « Les Françaises et Français face à l'information ». Tout tourne dans le navigateur : pas de serveur, pas de base de données.

- Site : https://opendata2025.netlify.app/
- Défi : <a href="https://defis.data.gouv.fr/defis/les-francaises-et-francais-face-a-linformation">Les Françaises et Français face à l'information</a>
- Données : <a href="https://defis.data.gouv.fr/datasets/603ff508ef46d75437d701f4">CSA/INA 2019-2020</a> sur la parité de la parole, deux fichiers CSV (chaînes, genres de programmes)
- Réutilisation déclarée : <a href="https://www.data.gouv.fr/reuses/observatoire-de-la-parite-mediatique">Observatoire de la Parité Médiatique</a> sur data.gouv.fr

## Ce que le site montre
Quatre chiffres clés, calculés à l'ouverture de la page à partir des CSV :
- taux de parole des femmes en 2020 ;
- taux dans le sport en 2020 ;
- heures analysées en 2020 ;
- rapport entre parole des hommes et des femmes.

Quatre graphiques (Chart.js) :
- **Volume global** : heures de parole des femmes et des hommes, 2019 contre 2020.
- **Évolution par chaîne** : taux 2019 en abscisse, taux 2020 en ordonnée, pour les 20 chaînes au plus gros volume en 2020. Un point rouge est sous la diagonale (taux en baisse).
- **Genres de programmes** : les 8 genres au taux de femmes le plus élevé, plus le sport s'il n'en fait pas partie.
- **Comparatif hommes / femmes** : les 12 éditeurs au taux le plus élevé en 2020, avec un filtre Tout / Radio / TV.

### Un résultat, vérifiable dans les données
En 2020, 33 des 35 chaînes ont un taux d'expression des femmes inférieur à 50 %. Colonne utilisée : `women_expression_rate_2020` dans `data/chaines.csv`.

- Les deux exceptions : Fip (70,4 %) et France 4 (60,0 %). Pour Fip, la parole identifiée ne couvre que 4,2 % de la durée analysée (`speech_rate_2020`), soit environ 61 heures.
- La chaîne la plus proche de 50 % parmi les autres : 6TER (48,0 %). La plus basse : L'Equipe (13,0 %).
- Par genre (`data/genres_programmes.csv`, même colonne) : sport 13,1 %, musique 44,0 %.

## Comment c'est fait
- **Une seule page** : `index.html`, en HTML, CSS et JavaScript, sans framework ni étape de build.
- **Chargement des données** : `fetch` sur `data/chaines.csv` et `data/genres_programmes.csv`, lecture du CSV par une petite fonction (`parseCSV`), calculs dans le navigateur.
- **Services externes** : Chart.js et chartjs-plugin-annotation 1.0.2 (jsDelivr), polices Poppins et Roboto (Google Fonts), avatars de l'équipe (unavatar.io). La page a besoin d'une connexion pour les afficher.
- **Hébergement** : Netlify.

### Les données
Chaque ligne de `chaines.csv` (40 lignes) est une chaîne ; chaque ligne de `genres_programmes.csv` (13 lignes) est un genre de programme. Pour 2019 et 2020 :
- `total_declarations_duration_*` : durée analysée ;
- `women_speech_duration_*`, `men_speech_duration_*` : durée de parole des femmes et des hommes ;
- `other_duration_*` : le reste de la durée (total moins femmes moins hommes) ;
- `women_expression_rate_*` : femmes / (femmes + hommes) ;
- `speech_rate_*` : (femmes + hommes) / durée totale.

Les durées sont lues en secondes : `index.html` et `EDA.ipynb` les divisent par 3 600 pour obtenir des heures.

### Les notebooks
- `notebooks/parite_medias_eda.ipynb` : exploration avec pandas, seaborn et matplotlib. Volumes 2019 et 2020, groupes audiovisuels, radio contre TV, genres, volume contre taux. Lit `../data/`.
- `notebooks/EDA.ipynb` : analyse plus poussée. Violons radio / TV, genres, régression linéaire (scikit-learn) sur 2019 et 2020, statut par chaîne. Lit `data/chaines.csv` et `data/genres_programmes.csv`.

### Squelette du dépôt
```
.
|-- README.md
|-- index.html
|-- .gitignore
|-- data/
|   |-- chaines.csv
|   `-- genres_programmes.csv
`-- notebooks/
    |-- parite_medias_eda.ipynb
    `-- EDA.ipynb
```

## Lancer en local
### Le site
La page charge les CSV avec `fetch` : ouvrez-la depuis un serveur local, pas en double-cliquant sur le fichier.

```bash
git clone https://github.com/Rateur/opendata.git
cd opendata
python -m http.server 8000
```

Puis http://localhost:8000.

### Les notebooks
Ils lisent les CSV de `data/` par des chemins relatifs.

```bash
pip install -r requirements.txt
cd notebooks
jupyter lab
```

Ou sans interface, depuis la racine :

```bash
python -m nbconvert --to notebook --execute --output-dir /tmp notebooks/EDA.ipynb notebooks/parite_medias_eda.ipynb
```

Relancés en octobre 2026 avec Python 3.13 et les versions de `requirements.txt` : mêmes résultats que les sorties enregistrées.

## État et limites
Le site est en ligne. Les données sont des CSV versionnés : rien ne les met à jour. Le dépôt n'a ni tests, ni intégration continue, ni fichier de licence (licence : À confirmer).

Ce que les données ne permettent pas :
- **Deux années seulement.** 2019 et 2020 ne font pas une tendance. La droite de `EDA.ipynb` est ajustée sur ces deux points.
- **Couverture inégale.** `chaines.csv` compte 40 lignes : 35 ont des données 2020, 37 des données 2019, 32 les deux. Les totaux 2019 et 2020 (graphique de volume, projection du notebook) additionnent donc des chaînes différentes.
- **Durée analysée instable.** Une même chaîne change de volume d'une année à l'autre. BFMTV : 3 095 h en 2019, 1 381 h en 2020. France 4 : 141 h puis 796 h, et son taux passe de 23,5 % à 60,0 %. Cause : À confirmer.
- **Plusieurs façons de calculer une part.** En 2020, les femmes pèsent 27,7 % de la durée totale, « autres » inclus (`parite_medias_eda.ipynb`). Elles pèsent environ 35 % de la parole identifiée, femmes + hommes (chiffre clé de la page). La page donne les deux, avec leur base. Les moyennes par groupe et par média de ce notebook sont des moyennes simples de taux, non pondérées par le volume.
- **Mesure.** La page indique une segmentation audio automatique. Les fichiers ne donnent pas sa marge d'erreur : À confirmer.
- **Pas de cause.** Les CSV ne contiennent que des durées. Ils ne disent rien des sujets ni des invités. Entre 2019 et 2020, 14 chaînes reculent et 18 progressent ; les données ne permettent pas d'en attribuer la cause au confinement.

## Équipe
<div align="center">
  <table>
    <tr>
      <td align="center">
        <a href="https://github.com/Rateur">
          <img src="https://github.com/Rateur.png" alt="Valentin Périès" width="64" height="64" style="border-radius: 32px;">
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/GautierGavat">
          <img src="https://github.com/GautierGavat.png" alt="Gautier Gavat" width="64" height="64" style="border-radius: 32px;">
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/tousabry69-a11y">
          <img src="https://github.com/tousabry69-a11y.png" alt="Sabry Touam" width="64" height="64" style="border-radius: 32px;">
        </a>
      </td>
    </tr>
    <tr>
      <td align="center"><sub><strong>Valentin Périès</strong></sub></td>
      <td align="center"><sub><strong>Gautier Gavat</strong></sub></td>
      <td align="center"><sub><strong>Sabry Touam</strong></sub></td>
    </tr>
  </table>
</div>
