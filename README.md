# Integration NFL pour Home Assistant

Ce depot distribue uniquement l'integration NFL. HACS ne gere qu'une integration
par depot : chaque nouvelle integration doit etre publiee dans son propre depot.

Cette integration interroge les API publiques ESPN et expose les entites suivantes :

- `sensor.nfl_classement_complet`
- `sensor.nfl_classement_pre_saison`
- `sensor.nfl_classement_global`
- `sensor.nfl_matchs_du_jour`
- `sensor.nfl_matchs_a_venir`
- `sensor.nfl_matchs_pre_saison`

Les donnees detaillees sont disponibles dans l'attribut `teams` pour les classements
et `games` pour les matchs.

## Installation manuelle

1. Copier `custom_components/nfl` dans `/config/custom_components/nfl`.
2. Redemarrer Home Assistant.
3. Ouvrir **Parametres > Appareils et services > Ajouter une integration**.
4. Rechercher `NFL` et valider l'ajout.
5. Ajouter la carte presente dans `sample-card.yaml` au dashboard Lovelace.

## Installation avec HACS

1. Dans HACS, ajouter `UnknownB81/HA-NFL-Integration` comme depot personnalise de type
	**Integration**.
2. Installer `NFL`, puis redemarrer Home Assistant.

L'installation ne necessite aucune cle API ESPN.

## Migration depuis la configuration YAML

Supprimer l'ancien contenu NFL de `configuration.yaml` ou de `packages/nfl.yaml`
avant d'ajouter l'integration depuis l'interface. Les deux modes ne doivent pas
fonctionner en meme temps, sinon les entites seront dupliquees.

La carte Lovelace necessite `flex-table-card` et `tabbed-card`, installables via HACS.

## Developpement

Les donnees sont rafraichies toutes les cinq minutes. Les matchs a venir couvrent
les quatorze prochains jours. Les erreurs de recuperation ESPN sont gerees par le
coordinateur Home Assistant et rendent les entites indisponibles jusqu'au prochain
rafraichissement reussi.