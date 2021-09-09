# Arretes Ministeriels

Jeu de donnée des arrêtés ministériels enrichis de conditions d'application

## metadata

Il s'agit des métadonnées des arrêtés ministériels ICPE, le schéma est décrit [ici](https://envinorma.github.io/envinorma-data/envinorma.models.html#envinorma.models.am_metadata.AMMetadata).

Chaque fichier est un dictionnaire qui peut-être chargé par la méthode `AMMetadata.from_dict` de la [librairie Envinorma](https://github.com/Envinorma/envinorma-data).

## ams

Il s'agit des arrêtés ministériels au format Envinorma, le schéma est décrit [ici](https://envinorma.github.io/envinorma-data/envinorma.models.html#envinorma.models.arrete_ministeriel.ArreteMinisteriel).

Chaque fichier est un dictionnaire qui peut-être chargé par la méthode `ArreteMinisteriel.from_dict` de la [librairie Envinorma](https://github.com/Envinorma/envinorma-data).

# Exemple d'utilisation : appliquer un jeu de paramètres à un arrêté ministériel

Ce script montre comment générer la version d'un arrêté ministériel étant donnée la connaissance d'un paramètre.
Il suppose que la [librairie Envinorma](https://github.com/Envinorma/envinorma-data) a été installée.

**1. Cloner le dépôt**

```sh
git clone https://github.com/Envinorma/arretes-ministeriels
cd arretes-ministeriels
```

**2. Script**

```python
from datetime import date

from envinorma.models import ArreteMinisteriel
from envinorma.parametrization import Parametrization, ParameterEnum
from envinorma.parametrization.apply_parameter_values import apply_parameter_values_to_am


am_id = 'JORFTEXT000018332514'
am = ArreteMinisteriel.from_dict(json.load(open(f'ams/{am_id}.json')))

parameter_values = {ParameterEnum.DATE_AUTORISATION.value: date.today()}
am_with_warnings = apply_parameter_values_to_am(am, parameter_values)

```

`am_with_warnings` est la version de l'arrêté ministériel pour les classements dont on sait que la date d'autorisation est égale à la date du jour.
