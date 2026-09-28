# Stormshield SN150 sous OpenWrt

[🇫🇷 Français](README.md) · [🇬🇧 English](README.en.md)

Projet communautaire consacré à l'installation et à l'utilisation d'**OpenWrt sur le Stormshield SN150**.

> [!WARNING]
> Le support du SN150 sous OpenWrt doit être considéré comme expérimental.
> Ne flashez pas votre équipement sans avoir préalablement sauvegardé son contenu et préparé une méthode de récupération fonctionnelle.

Ce projet n'est affilié ni à **Stormshield** ni au projet **OpenWrt**.

## Présentation

Le Stormshield SN150 est une appliance réseau que l'on trouve notamment sur le marché de l'occasion en France et dans l'espace francophone.

Bien que le matériel soit ancien, il peut encore constituer une plateforme intéressante pour :

- découvrir OpenWrt ;
- recycler une appliance réseau professionnelle ;
- créer un routeur ou pare-feu pour un homelab ;
- expérimenter avec les VLAN ;
- héberger une passerelle VPN WireGuard ;
- tester différentes fonctions réseau d'OpenWrt.

L'objectif de ce dépôt est de documenter de manière reproductible :

- le matériel du SN150 ;
- la sauvegarde de l'installation d'origine ;
- l'installation et le démarrage d'OpenWrt ;
- les possibilités de récupération en cas de problème ;
- la correspondance des interfaces et ports physiques ;
- des exemples de configuration réseau ;
- les VLAN ;
- le pare-feu ;
- WireGuard ;
- le durcissement de l'administration ;
- les limitations connues de cette plateforme.

Les configurations présentées dans ce dépôt sont volontairement génériques et anonymisées. Elles doivent être adaptées à chaque environnement.

## État actuel du projet

La configuration actuellement validée utilise :

- **Stormshield SN150**
- référence matérielle testée : `SN150-XA10A-101`
- **OpenWrt 24.10.4**
- cible OpenWrt : `kirkwood/generic`
- architecture OpenWrt : `arm_xscale`
- architecture noyau : `armv5tel`
- board : `stormshield,sn150`
- modèle détecté : `Stormshield SN150 (experimental)`

Sur le matériel utilisé pour développer cette documentation, les fonctions suivantes ont été validées :

| Fonction | État |
|---|---|
| Démarrage OpenWrt | ✅ Testé |
| Interfaces Ethernet | ✅ Testé |
| Switch intégré | ✅ Testé |
| Routage IPv4 | ✅ Testé |
| Pare-feu | ✅ Testé |
| VLAN | ✅ Testé |
| DHCP | ✅ Testé |
| DNS | ✅ Testé |
| WireGuard | ✅ Testé |
| Administration SSH | ✅ Testé |
| Procédure de récupération | 📝 Documentation en cours |
| Mise à jour vers d'autres versions OpenWrt | ⚠️ Non validée |

Cette documentation décrit en priorité **ce qui a réellement été testé sur le matériel**, plutôt que de supposer qu'une fonctionnalité ou une version plus récente fonctionnera automatiquement.

## Matériel testé

| Élément | Caractéristique observée |
|---|---|
| Modèle | Stormshield SN150 |
| Référence testée | `SN150-XA10A-101` |
| SoC / CPU | Marvell Kirkwood / Feroceon 88FR131 rev 1 |
| Architecture CPU | ARMv5TE |
| Cœurs | 1 |
| Mémoire | environ 512 MiB |
| Stockage de démarrage | SDHC interne |
| Périphérique de stockage | `/dev/mmcblk0` |
| Capacité observée | environ 7,46 GiB |
| RootFS | SquashFS + overlay ext4 |
| Switch Ethernet | Marvell 88E6172 |
| Interface CPU | `eth0` |
| Lien CPU ↔ switch | 1 Gbit/s full duplex |

Ces informations correspondent au matériel réellement observé sur l'exemplaire utilisé pour ce projet. Une autre révision matérielle doit être vérifiée avant d'appliquer la même procédure.

## Correspondance des ports physiques

La correspondance suivante a été validée sous OpenWrt :

| Marquage physique SN150 | Interface OpenWrt |
|---|---|
| Port `1` | `wan` |
| Port `2A` | `lan1` |
| Port `2B` | `lan2` |
| Port `2C` | `lan3` |
| Port `2D` | `lan4` |

Cette table décrit uniquement la correspondance matérielle. Les VLAN, rôles LAN/WAN et règles de pare-feu restent entièrement configurables dans OpenWrt.

## Avant de commencer

Avant toute modification du SN150 :

1. identifiez précisément la référence et la révision de votre matériel ;
2. sauvegardez ce qui peut l'être sur le système d'origine ;
3. préparez et testez l'accès console et la méthode de récupération ;
4. conservez une copie de vos sauvegardes sur une autre machine ;
5. ne remplacez pas le bootloader sans comprendre et avoir testé la procédure de récupération ;
6. n'appliquez pas aveuglément une image ou une mise à jour OpenWrt destinée à un autre matériel.

Le fait qu'une version soit plus récente que celle documentée ici ne signifie pas qu'elle a été testée sur le SN150.

## Documentation

La documentation détaillée sera construite progressivement dans [`docs/`](docs/README.md).

Les futures sections couvriront notamment :

- inventaire matériel ;
- sauvegarde et récupération ;
- installation OpenWrt ;
- interfaces réseau ;
- VLAN ;
- WireGuard ;
- pare-feu ;
- durcissement SSH ;
- DNS ;
- limitations et problèmes connus.

Les exemples de configuration seront placés dans [`configs/`](configs/README.md) et resteront séparés de toute configuration personnelle réelle.

## Exemple d'utilisation

```text
Internet
   |
modem / routeur opérateur
   |
SN150 / OpenWrt
   |
   +--- LAN
   +--- Servers
   +--- IoT
   +--- Guests
   +--- WireGuard VPN
```

Ce schéma est volontairement générique et ne représente pas l'infrastructure privée ayant servi aux tests.

## Sécurité et anonymisation

Ce dépôt public ne doit contenir aucun secret ni information permettant de reproduire l'infrastructure privée d'un contributeur.

Ne publiez notamment jamais :

- clé privée WireGuard ;
- preshared key WireGuard ;
- clé SSH privée ;
- mot de passe ;
- token ou secret d'API ;
- sauvegarde OpenWrt complète non nettoyée ;
- adresse IP publique personnelle ;
- nom de domaine ou DDNS personnel si sa publication n'est pas volontaire ;
- topologie privée détaillée non nécessaire au projet.

Les fichiers de configuration publiés ici utiliseront des valeurs d'exemple et des placeholders clairement identifiables.

## Contributions

Les retours, corrections, issues et pull requests sont les bienvenus.

Pour qu'un retour matériel soit exploitable, indiquez si possible :

- la référence exacte du SN150 ;
- la révision matérielle si elle est connue ;
- la version OpenWrt utilisée ;
- la méthode de démarrage ou d'installation ;
- les logs pertinents après suppression des secrets et informations personnelles.

Merci de **ne jamais poster de clés, mots de passe ou sauvegardes brutes** dans une issue.
