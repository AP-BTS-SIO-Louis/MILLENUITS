# SP 1 - Mission 3 - Mise en place AP WIFI Commercial et invité

**SP 1 : Gestion de l'infrastructure réseau**

**Mission 3 : Mise en place de l'AP**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://github.com/AP-BTS-SIO-Louis/millenuits/raw/main/images/logo_millenuits.png)

---
## Informations générales

- **Date de création** : 23/01/2026
- **Dernière modification** : 23/01/2026
- **Auteur** : MEDO Louis

---
## Sommaire

- [A remplir]

---
## Objectif

[Insérer un l'objectif générale de la procédure]

---
## A. Mise en place physique de l'AP

**1.1 Connexion des liaisons Ethernet.** Connecter les liaisons Ethernet sur un port ayant comme vlan le COMMERCIAL.

**1.2 Vérifier le la liaison physique.** Les LEDs doivent être verte ou orange.

---
## B. Ajout du vlan invité au réseau

> Nous devons ajouté le vlan invité pour ajouter le SSID invité. 

**1.1 Création de la sous interface VLAN 15 sur le routeur.**  
```CISCO
rt_millenuits-01(config)# interface 
rt_millenuits-01(config-subif)# GigabitEthernet0/0.15
rt_millenuits-01(config-subif)# encapsulation dot1Q 15
rt_millenuits-01(config-subif)# ip address 172.40.2.142 255.255.255.240
rt_millenuits-01(config-subif)# ip nat outside
rt_millenuits-01(config-subif)# exit
```

**1.2 Configuration VLAN 15 sur le switch.**
```CISCO
! Création du vlan 15 sur le switch
sw_coeur-01(config)# vlan 15
sw_coeur-01(config)# name INVITE
sw_coeur-01(config)# ex

! Ajout du vlan 15 au port trunk (switch <=> routeur)
sw_coeur-01(config)# interface GigabitEthernet0/2
sw_coeur-01(config-if)# switchport trunk allowed vlan 10-15,51
sw_coeur-01(config-if)# ex

! Ajout du vlan 15 au port access (switch <=> switch invite)
sw_coeur-01(config)# interface FastEthernet 0/6
sw_coeur-01(config-if)# switchport mode access
sw_coeur-01(config-if)# switchport access vlan 15
sw_coeur-01(config-if)# ex
```


---



