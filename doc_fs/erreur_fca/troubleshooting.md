# Troubleshooting

Référence de la documentation : https://github.com/france-connect/sources/blob/main/back/_doc/erreurs.md

## Avant redirection vers le FI

## Code erreur `Y00000` - write EPROTO C037E49CD87F0000:error:0A00010B:SSL routines:ssl3_get_record:wrong version number:../deps/openssl/openssl/ssl/record/ssl3_record.c:355:
Pour ajouter un FI à Agent Connect, il faut faire une demande d'ouverture de flux entre Agent Connect et le Fournisseur d'Identité. Le blocage peut être de 2 natures :
- Agent Connect bloque la redirection vers ce FI -> il faut faire une demande à l'équipe ops sur leur board (ticket exemple : https://gitlab.dev-franceconnect.fr/ops/infra/-/issues/2929), en leur précisant l'URL du FI à whitelister
- le FI bloque l'appel d'Agent Connect -> il faut indiquer au FI quelle IP whitelister.

```
AC INTEG RIE : 100.67.22.12
AC PROD RIE : 100.67.22.9

AC INTEG INTERNET : 145.242.17.6
AC PROD INTERNET : 145.242.17.7
```

## Après redirection vers le FI

## Code erreur `Y020018`
Le niveau eIDAS renvoyé par le FI est plus élevé que le maximum configuré pour ce FI. Aujourd'hui, le maximum configuré pour tous les FI est par défaut `eidas1` Il faut :
- soit demander au FI partenaire de renvoyer `eidas1` (recommandé)
- soit changer la configuration du FI pour `eidas3`

### Code erreur `Y030025` - "Invalid token"
Le token a une durée de vie de 60 secondes. Il est probable que le partenaire soit en train de tester sa configuration non pas avec un script, mais en testant les routes à la main, et donc ait dépassé la durée de vie du token.

## Code erreur `Y020019`
Le FI n'existe pas. Vérifier 

## Code erreur `Y020026`
Cas de l'INSERM : une redirection de flux vers l'hybridge était présente, alors qu'il ne s'agit que d'un FI sur la prod internet (https://gitlab.dev-franceconnect.fr/ops/infra/-/merge_requests/2730/diffs)
