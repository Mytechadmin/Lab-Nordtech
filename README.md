# NordTech Solutions – Infrastructure Réseau Multi-Sites

Projet d’infrastructure réseau et systèmes pour une PME multi-sites (Brest & Lyon).

Ce dépôt documente la conception, la configuration et la mise en œuvre d’une architecture réseau redondante reliant deux sites via un VPN IPsec site-to-site.

---

## Présentation

Simulation d’une infrastructure réseau d’entreprise en croissance comprenant :

- Deux sites géographiquement distincts (Brest et Lyon)
- Segmentation en VLANs par service + isolation des serveurs
- Redondance de passerelle (HSRP) et de liens
- VPN IPsec site-to-site (tunnel primaire + tunnel de secours)
- Durcissement de base des équipements Cisco
- Plan d’adressage cohérent et documenté

---

## Architecture

| Élément              | Détail                                      |
|----------------------|---------------------------------------------|
| Site Brest           | `10.10.0.0/16`                              |
| Site Lyon            | `10.20.0.0/16`                              |
| Liens WAN / VPN      | `100.64.0.0/24`                             |
| Passerelle           | HSRP (IP virtuelle `.1`)                    |
| VPN                  | IPsec site-to-site (crypto map)             |
| AAA                  | TACACS+ (centralisé sur Brest)              |

### Principes de design

- Un VLAN par service + VLANs serveurs dédiés
- VLAN de management séparé (99)
- VLAN natif inutilisé (sécurisation des trunks)
- Passerelle redondante HSRP sur les SVI des switches L3
- Deux tunnels VPN IPsec indépendants (primaire + secours)
- Bascule automatique via HSRP : le trafic suit le routeur actif

---

## État d’avancement

| Partie                                      | Statut     |
|---------------------------------------------|------------|
| Plan d’adressage IP                         | Terminé    |
| VLANs / Trunks / Ports d’accès              | Terminé    |
| Redondance HSRP                             | Terminé    |
| VPN Site-to-Site (primaire + secours)       | Terminé    |
| DHCP                                        | Terminé    |
| AAA / TACACS+                               | Terminé    |
| Services serveurs (AD, DNS, Fichiers…)      | En cours   |
| Partie virtualisation (VMs)                 | À venir    |
| Scripts PowerShell / automatisation         | À venir    |

---

## Contenu du dépôt├── packet-tracer/
NordTechLAB.pkt              # Maquette complète Cisco Packet Tracer
configs/
routers/                     # Configurations de 2 routeurs
switches/                    # Configurations de 2 switches
docs/
Plan_Adressage_NordTech.pdf  # Plan d’adressage détaillé
captures/                    # Captures d’écran (topologie, show…)
README.mdtext---

## Topologie

![Topologie NordTech](docs/captures/topologie.png)

<img width="1413" height="747" alt="image" src="https://github.com/user-attachments/assets/e5451801-ae08-417d-84be-5ee207d352e5" />


---

## Points de sécurité

Dans le cadre de ce laboratoire :

- Les mots de passe sont volontairement simples et laissés en clair
- Les configurations sont destinées à un environnement isolé (Packet Tracer / VMs)
- Aucun de ces éléments n’est utilisé en production

**Bonnes pratiques déjà mises en place :**

- Accès administration en SSH uniquement
- Restriction des lignes VTY par ACL
- Port-security sur les ports d’accès
- BPDU Guard + PortFast
- DHCP Snooping
- Bannière de connexion + timeout de session
- AAA avec TACACS+ (fallback local)

---

## Compétences mobilisées

- Conception d’architecture réseau multi-sites
- Adressage IP et segmentation VLAN
- Redondance de passerelle (HSRP)
- VPN IPsec site-to-site
- Durcissement de base des équipements Cisco
- Documentation technique

---

## Note

Ce projet a été réalisé dans un contexte d’apprentissage.

Je suis encore junior sur ces technologies : il peut donc rester des erreurs, des approximations ou des choix perfectibles.

Tout retour ou suggestion d’amélioration est le bienvenu.

---

## Auteur

Projet réalisé dans le cadre d’une formation en administration d’infrastructures sécurisées, en parallèle d’une recherche d’opportunité professionnelle.
