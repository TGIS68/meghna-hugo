---
title: "Infrastructure sécurisé CentOS"
date: 2018-09-12T14:51:12+06:00
author: Mark Dinn
#image_webp: image
image: images/realisation/pro/controle-commande.jpg
description : "This is meta description"
---

#Réalisation 1 : Administration et sécurisation d'un système CentOS
Présentation
## Introduction

Dans le cadre d'un projet ayant pour but la mise en oeuvre d'un système de supervision et de contrôle commande de process industriel pour le domaine spatial, notre cellule cybersécurité EES-Clemessy avait pour objectif de sécuriser les postes et serveurs de ce système.

Nous nous préoccupons principalement de l'administration et de la sécurisation du système d'exploitation (OS), qui est ici un système d'exploitation GNU/Linux et plus précisement une distribution CentOS qui est une variante semblable à Red Hat, en version communautaire et gratuite.
Ces postes et serveurs hébergent des applications de supervision et contrôle commande développé par un autre service d'EES-Clemessy permettant d'effectuer des actions et de visualiser l'état du système.

## Mise en oeuvre

Le sécurité de l'installation est un besoin important pour le client du à la criticité du process industriel et des risques financiers, matériels ou humains.
Des contraites temps réel sont importante concernant la supervision et le contrôle commande. Pour cette raison, le serveur de supervision est installé avec un noyau temps réel qui permet de considérablement diminuer le délai d'un traitement.

L'application est développé en se basant sur les services offerts par ce noyau et permet par conséquent d'atteindre les délais souhaités.
Nous avons fait le choix d'installé ce serveur en mode core (sans interface graphique) afin de diminuer la surface d'attaque et minimiser la perte de performance du à un environnement bureatique.

Des postes clients, sont eux aussi muni d'une application dévoppé par EES-Clemessy. Cette application permet d'intéragir avec le serveur afin d'exécuter des instructions, commandes, procédures automatiques,etc.

La communication des données métiers entre les postes clients et serveurs est réalisé à travers l'implémentation du protocole OPC UA approprié pour les communications d'applications d'automatisation industrielle. C'est un standard de communication ouvert, basé sur un fonctionnement client-serveur et qui permet l'intégration de mesure de sécurité, tels que la signature et le chiffrement des échanges permettant de garantir intégrité, confidentialité et non-répudiation.

De plus la réalisation de ce projet est réalisé en groupement avec une autre entreprise qui est responsable de l'infrastructure réseau et d'administration du système nottament par la configuration des switches, pare-feu mais aussi la mise à disposition d'un serveur LDAP et  d'un serveur de centralisation des journaux auquel nous devons ratacher nos composants.

Afin de réaliser la configuration et la sécurisation du système d'exploitation et des fonctionnalités, nous avons fourni des scripts bash qui réalisent l'ensemble des actions automatiquements. 

La mise en oeuvre de cette infrastructure m'a permis de développer mes compétences en administration et sécurisation d'un OS GNU/Linux. J'ai principaleemnt développé les compétences suivantes :
- Scripting bash : développement de script bash pour le paramétrage automatique du système
- Configuration réseau : configuration des interfaces réseau, mise en place de bonding (agrégation de lien), tague de VLAN, configuration du pare-feu.
- Configuration système : configuration de fonctionnalité système tels qu'un serveur SSH,  NTP via Chrony, intégration d'un noyau temps réel, intégration dans un LDAP.
- Sécurisation du système : limitation des paquets installés, gestion des dépendances, durcissement des règles d'audit et de journalisation, limitation des services de systemd, gestion des droits d'accès classique et ACL

## Conclusion

Au final, ce projet était très intéressant et m'a permis de me familiariser avec la distribution CentOS et plus généralement sur l'administration des systèmes GNU/Linux. 
J'ai rencontré de nombreuses problématiques et anomalies qui m'ont permis de me rendre compte que l'administration et la sécurisation de ce système peut être complexe et nécessite des compétences accrues.

Compétences liées :
Cybersécurité
Administration Linux
Persévérance
