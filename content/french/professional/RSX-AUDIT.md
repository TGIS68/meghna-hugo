---
title: "Audit de sécurité - Commutateur Réseau"
date: 2018-09-12T14:51:12+06:00
author:
#image_webp: image
image: images/realisation/pro/controle-commande.jpg
#description : "This is meta description"
---

## Introduction

Pour l'occasion d'une évolution d'un système de contrôle commande existant, notre client nous demande de réaliser un audit de sécurité des configurations commutateurs Cisco existant.
Les commutateurs sont des élements critiques du système d'information car ils distribuent une grande partie des données qui y transitent. Etant donnés leur rôle, une atteinte à un commutateur aurait potentiellement un impact important sur la sécurité et le fonctionnement d'un système (déni de service, écoute du trafic réseau, intrusion)

Il est donc nécessaire de les prendre en compte dans la sécurisation d'un système et renforcer leur robustesse face à des actions malveillantes ou à des erreurs de configuration.

L'infrastructure du projet est composé de 4 commutateurs physiques, compilé par 2, ce qui donne deux commutateurs logiques. Les deux commutateurs sont reliés entre eux en fibre optique afin d'assurer la communication entre les périphériques de deux batiments distants.
Par ces commutateurs transitent des données préciseuses de supervision et contrôle commande d'un process critique avec un délai très faible. Une atteinte à la disponibilité ou à l'intégrité d'un commutateur serait catastrophique pour l'infrastructure.

 ## Mise en oeuvre

Je travaille en autonomie pour réaliser cet audit en me basant sur mes compétences existantes dans ce domaine ainsi que sur des recommandations de l'ANSSI et du NIST.
J'ai commencé par étudier la configuration actuelle des commutateurs afin de mieux comprendre les éléments configurés. Les commutateurs manquaient cruellement de mesures de sécurité. La configuration était certe fonctionnel mais les risques sécurité était trop important.

Ainsi j'ai listé l'ensemble des parties de configuration qui n'était pas propice en expliquant le risque associé et en proposant des lignes de configuration qui permettrait de corriger la configuration.

J'ai notamment traité et fait des recommandations sur les aspects suivants :
- Administration du commutateur
    - Protocole et algorithme recommandés
    - Limitation des accès logique
    - Journalisation des authentifications
    - Niveau de privilège 
    - Gestion des comptes locaux
    - Politique de mots de passe, bloquage de compte
- Configuration des VLAN (access, trunk)
    - VLAN de quarantaine, VLAN par défaut et VLAN natif
    - Private VLAN
    - Routage interVLAN
    - Liste d'accès de couche 4 (ACL)
- Mécanisme liés à la disponibilité
    - Spanning tree et storm control
    - agrégation de liens

J'ai décrit l'ensemble de ces messures dans un document technique que nous avons remis au client. L'objectif était de lui faire prendre consciance des risques liés à la configuration actuelle des commutateurs et de lui proposer une prestation pour renforcer ce niveau de sécurité.

## Bilan

Cette réalisation m'a permis d'approfondir connaissance en sécurité réseau, particulièrement sur les aspects de configuration des commutateurs.
J'ai également pu me familiariser avec les différents types d'attaques réseaux ainsi que les mesures permettant de s'en protéger.

Même si les commutateurs ne doivent pas être considérés comme des équipements de sécurité, leur rôle est souvent trop négligé dans la mise en place de mesures de sécurisation du système.

## Compétences mis en oeuvre

- Administration et sécurité des réseaux
