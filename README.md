<div align="center">
  <h1>Open Data</h1>
  <p>
    <a href="https://github.com/Rateur/opendata">
      <img src="https://img.shields.io/github/stars/Rateur/opendata?style=for-the-badge&color=ffb300&logo=github&label=Stars" alt="GitHub Stars">
    </a>
    <a href="https://www.python.org/">
      <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
    </a>
    <a href="https://www.chartjs.org/">
      <img src="https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white" alt="Chart.js">
    </a>
  </p>
</div>

## Contexte
- Defi data.gouv.fr : « Les Francaises et Francais face a l'information » (enjeux de confiance, usages et pratiques).
- Donnees ouvertes traitees en local (pas de dependance cloud) : premiers jeux CSA/INA 2019-2020 sur la parite de la parole, nettoyes en CSV.
- Objectif court terme : cadrer les sources, fixer les hypotheses et poser le cadre d'analyse avant d'alimenter le site statique et les premiers notebooks.

## Sujet
- Questions guide : comment les publics consultent, trient et jugent l'information numerique et media.
- Sorties visees : analyses reproductibles (notebooks), visualisations claires et synthese courte.
- Principe : priorite a la transparence (scripts versionnes) et a la lecture rapide des resultats.

## Equipe
<div align="center">
  <table>
    <tr>
      <td align="center">
        <a href="https://github.com/Rateur">
          <img src="https://github.com/Rateur.png" alt="Valentin PERIES" width="64" height="64" style="border-radius: 32px;">
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
      <td align="center"><sub><strong>Valentin PERIES</strong></sub></td>
      <td align="center"><sub><strong>Gautier Gavat</strong></sub></td>
      <td align="center"><sub><strong>Sabry Touam</strong></sub></td>
    </tr>
  </table>
</div>

Profils GitHub :
- Valentin PERIES : https://github.com/Rateur
- Sabry Touam : https://github.com/tousabry69-a11y
- Gautier Gavat : https://github.com/GautierGavat

## Ressources
- Defi data.gouv.fr : https://defis.data.gouv.fr/defis/les-francaises-et-francais-face-a-linformation
- Jeux CSA/INA 2019-2020 sur la parite de la parole : chaines et genres de programmes.

## Donnees disponibles
- `data/chaines.csv` : indicateurs par media/editeur/groupe (volume et taux d'expression femmes/hommes/autres, 2019-2020).
- `data/genres_programmes.csv` : indicateurs par genre de programme (volumes et taux d'expression, 2019-2020).
- `notebooks/parite_medias_eda.ipynb` : exploration initiale (parite, evolutions et pistes de visualisations).
- `notebooks/EDA.ipynb` : notebook de découverte plus large (nettoyage/aperçu des jeux avant visualisation).

## Squelette du depot
```
.
|-- README.md
|-- index.html
|-- data/
|   |-- chaines.csv
|   `-- genres_programmes.csv
`-- notebooks/
    `-- parite_medias_eda.ipynb
```
