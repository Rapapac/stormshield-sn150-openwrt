# Documentation

[Retour au README principal](../README.md)

Cette arborescence accueillera progressivement la documentation technique du Stormshield SN150 sous OpenWrt.

## Principe

La documentation suit trois règles :

1. **tester avant d'affirmer** : une fonction est indiquée comme testée uniquement lorsqu'elle a été validée sur le matériel ;
2. **séparer les faits des hypothèses** : les procédures encore à reconstruire ou à vérifier sont explicitement indiquées comme telles ;
3. **ne publier aucune donnée privée** : les configurations, captures et logs doivent être nettoyés avant publication.

## Langues

Le français est la langue de rédaction principale du projet.

Les pages stables pourront ensuite être traduites en anglais afin de rendre le travail utile à un public plus large.

## Documentation prévue

| Fichier prévu | Sujet | État |
|---|---|---|
| `hardware.md` | Inventaire matériel détaillé | À rédiger |
| `backup-and-recovery.md` | Sauvegarde, console et récupération | À reconstruire et valider |
| `openwrt-installation.md` | Installation / démarrage d'OpenWrt | À reconstruire et valider |
| `networking.md` | Interfaces et configuration réseau | À rédiger |
| `vlans.md` | VLAN et switch intégré | À rédiger |
| `wireguard.md` | Passerelle WireGuard | À rédiger |
| `firewall.md` | Pare-feu OpenWrt | À rédiger |
| `ssh-hardening.md` | Durcissement de l'administration SSH | À rédiger |
| `dns.md` | DNS et exemples de sécurisation | À rédiger |
| `known-limitations.md` | Limites matérielles et logicielles | À rédiger |

## Ce qui est déjà validé

Sur l'exemplaire de référence, ont déjà été observés et testés :

- démarrage d'OpenWrt 24.10.4 ;
- détection du board `stormshield,sn150` ;
- interfaces `wan`, `lan1`, `lan2`, `lan3` et `lan4` ;
- routage IPv4 ;
- VLAN ;
- DHCP et DNS ;
- pare-feu ;
- WireGuard ;
- administration SSH.

La procédure exacte ayant permis d'obtenir cet état sera documentée seulement après reconstruction et vérification des étapes.

## Contributions et preuves

Lorsqu'une procédure dépend d'une révision matérielle ou d'une version OpenWrt particulière, cette dépendance doit être indiquée.

Pour les rapports de test, privilégiez :

- commandes utilisées ;
- sortie des commandes pertinente ;
- version OpenWrt ;
- référence matérielle ;
- résultat attendu et résultat observé.

Nettoyez systématiquement les logs avant publication.
