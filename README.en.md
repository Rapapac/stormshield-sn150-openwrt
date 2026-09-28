# OpenWrt on the Stormshield SN150

[🇫🇷 Français](README.md) · [🇬🇧 English](README.en.md)

Community project dedicated to installing and running **OpenWrt on the Stormshield SN150**.

> [!WARNING]
> OpenWrt support for the SN150 should be considered experimental.
> Do not flash your device before backing up its contents and preparing a working recovery method.

This project is not affiliated with **Stormshield** or the **OpenWrt** project.

## Overview

The Stormshield SN150 is a network security appliance that can still be found on the second-hand market, especially in France and French-speaking communities.

Despite its age, the hardware can remain useful for:

- learning OpenWrt;
- reusing a professional network appliance;
- building a homelab router or firewall;
- experimenting with VLANs;
- running a WireGuard VPN gateway;
- testing OpenWrt networking features.

This repository aims to document, in a reproducible way:

- SN150 hardware;
- backup of the original installation;
- OpenWrt installation and boot;
- recovery options;
- physical port and interface mapping;
- generic network configuration examples;
- VLANs;
- firewalling;
- WireGuard;
- administration hardening;
- known platform limitations.

All configuration examples in this repository are intentionally generic and anonymized.

## Current project status

The currently validated setup uses:

- **Stormshield SN150**
- tested hardware reference: `SN150-XA10A-101`
- **OpenWrt 24.10.4**
- OpenWrt target: `kirkwood/generic`
- OpenWrt architecture: `arm_xscale`
- kernel architecture: `armv5tel`
- board: `stormshield,sn150`
- detected model: `Stormshield SN150 (experimental)`

The following features have been validated on the device used to build this documentation:

| Feature | Status |
|---|---|
| OpenWrt boot | ✅ Tested |
| Ethernet interfaces | ✅ Tested |
| Integrated switch | ✅ Tested |
| IPv4 routing | ✅ Tested |
| Firewall | ✅ Tested |
| VLANs | ✅ Tested |
| DHCP | ✅ Tested |
| DNS | ✅ Tested |
| WireGuard | ✅ Tested |
| SSH administration | ✅ Tested |
| Recovery procedure | 📝 Documentation in progress |
| Upgrade to other OpenWrt versions | ⚠️ Not validated |

The project intentionally documents **what has actually been tested on real hardware** rather than assuming that newer releases or additional features will automatically work.

## Tested hardware

| Component | Observed specification |
|---|---|
| Model | Stormshield SN150 |
| Tested reference | `SN150-XA10A-101` |
| SoC / CPU | Marvell Kirkwood / Feroceon 88FR131 rev 1 |
| CPU architecture | ARMv5TE |
| Cores | 1 |
| Memory | about 512 MiB |
| Boot storage | internal SDHC |
| Storage device | `/dev/mmcblk0` |
| Observed capacity | about 7.46 GiB |
| RootFS | SquashFS + ext4 overlay |
| Ethernet switch | Marvell 88E6172 |
| CPU interface | `eth0` |
| CPU ↔ switch link | 1 Gbit/s full duplex |

These values were observed on the physical unit used by this project. Other hardware revisions should be checked before applying the same procedure.

## Physical port mapping

The following mapping has been validated under OpenWrt:

| SN150 physical label | OpenWrt interface |
|---|---|
| Port `1` | `wan` |
| Port `2A` | `lan1` |
| Port `2B` | `lan2` |
| Port `2C` | `lan3` |
| Port `2D` | `lan4` |

This table only documents the hardware mapping. VLANs, LAN/WAN roles and firewall policies remain fully configurable in OpenWrt.

## Before you start

Before modifying an SN150:

1. identify the exact hardware reference and revision;
2. back up everything that can be preserved from the original system;
3. prepare and test console access and a recovery method;
4. keep copies of your backups on another computer;
5. do not replace the bootloader unless you understand and have tested the recovery process;
6. do not blindly flash an image or upgrade intended for different hardware.

A release being newer than the one documented here does not mean that it has been tested on the SN150.

## Documentation

Detailed documentation will progressively be added under [`docs/`](docs/README.md).

Planned topics include:

- hardware inventory;
- backup and recovery;
- OpenWrt installation;
- networking;
- VLANs;
- WireGuard;
- firewall;
- SSH hardening;
- DNS;
- known limitations and issues.

Generic configuration examples will live under [`configs/`](configs/README.md) and will remain separate from any real private configuration.

## Example use case

```text
Internet
   |
ISP modem / router
   |
SN150 / OpenWrt
   |
   +--- LAN
   +--- Servers
   +--- IoT
   +--- Guests
   +--- WireGuard VPN
```

This diagram is intentionally generic and does not represent the private infrastructure used during development.

## Security and anonymization

This public repository must not contain secrets or unnecessary details about a contributor's private infrastructure.

Never publish:

- WireGuard private keys;
- WireGuard preshared keys;
- private SSH keys;
- passwords;
- API tokens or secrets;
- raw, unreviewed OpenWrt backups;
- personal public IP addresses;
- personal domain or DDNS names unless intentionally public;
- unnecessary detailed private network topology.

Published configuration files will use example values and clearly identifiable placeholders.

## Contributing

Feedback, corrections, issues and pull requests are welcome.

For hardware reports, please include when possible:

- exact SN150 reference;
- hardware revision if known;
- OpenWrt version;
- boot or installation method;
- relevant logs after removing secrets and personal information.

Please **never post keys, passwords or raw backups** in an issue.
