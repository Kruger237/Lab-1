# TP – Routage Inter-VLAN avec Router-on-a-Stick

## Présentation

Ce TP a pour objectif de mettre en œuvre le routage inter-VLAN en utilisant la technique **Router-on-a-Stick**. Deux sites sont reliés par une liaison série et utilisent des routes statiques afin de permettre la communication entre tous les VLAN.

---

# Topologie

Le réseau est constitué de :

- 2 routeurs Cisco (R1 et R2)
- 2 switches Cisco (S1 et S2)
- 4 VLAN
- 4 machines clientes
- Une liaison série entre R1 et R2

## Organisation des VLAN

| VLAN | Réseau | Équipement |
|------|---------|------------|
| VLAN 10 | 192.168.10.0/24 | Windows |
| VLAN 20 | 192.168.20.0/24 | PC1 |
| VLAN 30 | 192.168.30.0/24 | Ubuntu |
| VLAN 40 | 192.168.40.0/24 | PC2 |

Les deux routeurs sont interconnectés par le réseau **10.0.0.0/30**.

---

# Plan d'adressage

## Routeur R1

| Interface | Adresse |
|-----------|---------|
| S0/0 | 10.0.0.1/30 |
| F0/0.10 | 192.168.10.254/24 |
| F0/0.20 | 192.168.20.254/24 |

## Routeur R2

| Interface | Adresse |
|-----------|---------|
| S0/0 | 10.0.0.2/30 |
| F0/0.30 | 192.168.30.254/24 |
| F0/0.40 | 192.168.40.254/24 |

---

# Configuration réalisée

## Switch S1

- Création des VLAN 10 et 20
- Configuration des ports d'accès
- Configuration d'un trunk vers R1

## Switch S2

- Création des VLAN 30 et 40
- Configuration des ports d'accès
- Configuration d'un trunk vers R2

## Routeur R1

- Configuration des sous-interfaces :
  - F0/0.10
  - F0/0.20
- Encapsulation IEEE 802.1Q
- Configuration de la liaison série
- Ajout des routes statiques vers les réseaux de R2

## Routeur R2

- Configuration des sous-interfaces :
  - F0/0.30
  - F0/0.40
- Encapsulation IEEE 802.1Q
- Configuration de la liaison série
- Ajout des routes statiques vers les réseaux de R1

---

# Vérifications

## Sur les switches

```bash
show vlan brief
show interfaces trunk
show mac address-table
```

## Sur les routeurs

```bash
show ip interface brief
show ip route
show running-config
```

---

# Tests de connectivité

Depuis chaque machine :

- Ping de la passerelle.
- Ping des hôtes appartenant aux autres VLAN.
- Vérification de la communication entre les deux sites.

Exemple :

```bash
ping 192.168.20.10
ping 192.168.30.10
ping 192.168.40.10
```

---

# Résultats obtenus

- Les VLAN sont correctement créés.
- Les ports sont affectés au bon VLAN.
- Les trunks fonctionnent correctement.
- Le routage inter-VLAN est opérationnel.
- Les routes statiques permettent la communication entre les deux routeurs.
- Les quatre postes communiquent entre eux sans perte de paquets.

---

# Conclusion

Ce TP a permis de mettre en œuvre le routage inter-VLAN à l'aide de la méthode **Router-on-a-Stick**. Les VLAN sont isolés au niveau 2 tout en restant interconnectés grâce aux sous-interfaces des routeurs et aux routes statiques entre les deux sites. Les tests de connectivité confirment le bon fonctionnement de l'ensemble de l'architecture.
