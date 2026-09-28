# Exemples de configuration

[Retour au README principal](../README.md)

Ce dossier accueillera des **exemples génériques et anonymisés** de configuration OpenWrt pour le Stormshield SN150.

Il ne doit jamais devenir une copie brute de `/etc/config/` provenant d'un routeur en production.

## Règles d'anonymisation

Avant de publier un exemple, remplacer ou supprimer au minimum :

- noms d'utilisateurs personnels ;
- noms d'hôtes privés ;
- adresses MAC ;
- adresses IP publiques ;
- domaines et DDNS personnels ;
- réservations DHCP réelles ;
- clés SSH ;
- clés WireGuard privées ;
- clés WireGuard publiques lorsqu'elles identifient un pair réel ;
- preshared keys ;
- mots de passe et hashes de mots de passe ;
- tokens et secrets d'API ;
- commentaires contenant des noms de personnes ou de machines privées.

## Valeurs d'exemple

Pour les futurs fichiers, préférer des valeurs manifestement génériques, par exemple :

```text
LAN             10.10.10.0/24
Servers         10.10.20.0/24
IoT             10.10.30.0/24
Guests          10.10.40.0/24
WireGuard       10.10.100.0/24

Router WG       10.10.100.1
Laptop          10.10.100.10
Phone           10.10.100.20
```

Pour les secrets :

```text
<ROUTER_PRIVATE_KEY>
<PEER_PUBLIC_KEY>
<PRESHARED_KEY>
<DDNS_HOSTNAME>
```

Ces valeurs sont uniquement documentaires et doivent être remplacées par l'utilisateur.

## Fichiers prévus

À mesure que la documentation sera validée, ce dossier pourra contenir notamment :

- `network.example` ;
- `firewall.example` ;
- `dhcp.example` ;
- `wireguard.example`.

Chaque fichier devra être relu manuellement avant publication afin de vérifier qu'aucune donnée privée n'y subsiste.
