# NordTech Solutions – Infrastructure Réseau Multi-Sites

Projet d’infrastructure réseau et systèmes pour une PME multi-sites (Brest & Lyon).

## Présentation

Ce projet simule la conception et le déploiement de l’infrastructure réseau d’une entreprise en croissance, avec deux sites reliés par un VPN site-to-site.

Objectifs principaux :
- Segmentation en VLANs par service
- Redondance (HSRP, liens multiples)
- VPN IPsec site-to-site
- Durcissement de base des équipements
- Plan d’adressage cohérent et documenté

## État d’avancement

| Partie | Statut |
|--------|--------|
| Plan d’adressage IP | Terminé |
| VLANs / Trunks / Ports d’accès | Terminé |
| Redondance HSRP | Terminé |
| VPN Site-to-Site (primaire + secours) | Terminé |
| DHCP | Terminé |
| Autres services serveurs (AD, DNS, Fichiers, AAA) | En cours |
| Partie virtualisation (VMs) | À venir |
| Scripts PowerShell / automatisation | À venir |

## Architecture réseau

- **Site Brest** : `10.10.0.0/16`
- **Site Lyon** : `10.20.0.0/16`
- **Liens WAN / VPN** : `100.64.0.0/24`

Principes retenus :
- Un VLAN par service + VLANs serveurs dédiés
- VLAN de management séparé (99)
- VLAN natif inutilisé (999) pour sécuriser les trunks
- Passerelle redondante HSRP sur les SVI
- Deux tunnels VPN IPsec indépendants (primaire + secours)

## Contenu du dépôt

├── packet-tracer/          # Maquette Cisco Packet Tracer
├── configs/
│   ├── routers/            # Configurations des routeurs
│   └── switches/           # Configurations des switches
├── docs/
│   └── Plan_Adressage.pdf  # Plan d’adressage détaillé
└── README.md

## Points de sécurité

Dans le cadre de cet exercice de laboratoire :
- Les mots de passe sont volontairement simples et laissés en clair
- Les configurations sont destinées à un environnement isolé (Packet Tracer / VMs)
- Aucun de ces éléments n’est utilisé en production

Bonnes pratiques déjà mises en place :
- Accès administration en SSH uniquement
- Port-security sur les ports d’accès
- BPDU Guard + PortFast
- DHCP Snooping
- Bannière de connexion et timeout de session
- ACL de restriction sur les lignes VTY

## Compétences mobilisées

- Conception d’architecture réseau multi-sites
- Adressage IP et segmentation VLAN
- Redondance (HSRP)
- VPN IPsec site-to-site
- Durcissement de base des équipements Cisco
- Documentation technique

## Note

Ce projet a été réalisé dans un contexte d’apprentissage.  
Je suis encore junior sur ces technologies : il peut donc rester des erreurs, des approximations ou des choix perfectibles.

Tout retour ou suggestion d’amélioration est le bienvenu.

## Auteur

Projet réalisé dans le cadre d’une formation en administration d’infrastructures sécurisées, en parallèle d’une recherche d’opportunité professionnelle.
