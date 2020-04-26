---
title: "Contrôle d'accès par 802.1X"
date: 2018-09-12T14:51:12+06:00
author:
#image_webp: image
image: images/realisation/pro/RSX-RADIUS.jpg
#description : "This is meta description"
---

## Introduction

Dans le cadre de la réalisation d'un projet de contrôle commande possédant de nombreux postes opérateurs et une infrastructure réseau importante, le client soumet des exigences en terme d'authentification réseau sur son système. Le standard 802.1X s'appuie sur des protocoles et des solutions de serveur d'authentification AAA ((Authentication, Authorization, Accounting)) pour assurer le contrôle d'accès des équipements d'une infrastructure réseau.

Le réseau d'un système d'information est aujourd'hui la cible de nombreuses attaque. Notamment les attaques d'écoutes et d'hommes du milieu sont facilement réalisable si le réseau n'est pas protégé. Par conséquent, l'accès au réseau d'un système d'information doit être contrôlé afin de prévenir les intrusions et attaques liées.

Après une rapide étude sur les solutions de serveur d'authentification possible, le choix de notre équipe c'est orienté sur le protocole Radius à travers la solution FreeRadius.
Le serveur d'authentification permet, en plus de gérer l’authentification des utilisateurs et l’attribution de leurs droits (autorisations), de tracer les authentifications et les commandes entrées (accounting) par les utilisateurs dans un but d’imputabilité.

Le contrôle d’accès distant est de loin la méthode à privilégier pour les connexions sur toutes les lignes (y compris console), car elle permet non seulement de s’appuyer sur une gestion centralisée des comptes utilisateurs, mais aussi de conserver une traçabilité des demandes d’accès directement au niveau du service de contrôle d’accès.

Quand on parle de contrôle d'accès 802.1X on peut parler de deux choses :
- Le contrôle d'accès pour la gestion des comptes d'administrations des composants du réseau (switches, routeurs)
- Le contrôle d'accès pour les ressources qui accèdent au réseau (client)

Dans cette réalisation nous mettont en oeuvre les deux types de contrôle d'accès à travers la solution FreeRadius.

## Mise en oeuvre

Je travaille en autonomie pour mettre en oeuvre cette solution. J'ai pu me procurer le matériel nécessaire (un poste de test pour le client, une VM pour le server et un switch) pour commencer à réaliser des essais sur une petite infrastructure.
La solution FreeRadius est une solution libre de serveur RADIUS. Elle sera supporté par une VM installé avec un système d'exploitation CentOS.
L'objectif dans un premier lieu est de faire en sorte que lorsqu'un composant se connecte à une des interfaces du switches l'accès au réseau ne lui soit pas accordé tant qu'il n'est pas authentifié.
La méthode retenu pour l'authentification est via le protocole EAP-TLS. C'est un protocole d'authentification mutuelle qui impose l'utilisation de certificat côté client et côté serveur en plus du mot de passe.
Cette authentification est réalisée à l’aide d’un handshake TLS ainsi l'échange du mot de passe n'est pas réalisé en clair sur le réseau. Contraitement au mot de passe, le certificat permet d'identifier la source et la destination lors de l'authentification. De plus, même si le mot de passe est découvert, il ne sera d'aucune utilité sans le certificat du client car le serveur RADIUS est configuré pour n'autoriser uniquement les demandes d'authentification qui proviennet de certificat identifier avec l'attribut "Common Name".
Le mode de fonctionnement est le suivant : tous les ports sont activés par défaut mais dans un état bloqué. Lorsqu’un terminal se branche, un processus d’authentification démarre. Si l’authentification réussit, le port est débloqué et la machine cliente accède au VLAN auquel le port a été rattaché. Dansle cas contraire, le port reste bloqué. C'est pour cette raison qu'on parle d'autorisation.

La configuration du switch est assez légère. En effet ce dernier ne joue que un rôle de "passeur" dans cette authentification. Il ne possède aucun secret, son rôle est juste de relayer les demandes d'authentification des clients vers le serveur et de prendre les actions lors qu'une authentification est réussi.
Dans la configuration global il faut spécifier l'adresse IP, port du serveur RADIUS. Il faut également spécifier une clé prépartagée qui sera utilisé pour protéger les échanges entre le serveur et le switch.

En plus d'authentifier et d'autoriser les ressources qui se connectent au réseau, je configure le serveur afin qu'il puisse gérer les comptes d'administration du switch. Par défaut l'authentification sur un commutateur est réalisé localement. Ainsi les secrets des comptes adminsitrateurs sont stockés sur une base local au switch sous forme de condensat. Hors l'utilisation du contrôle d'accès distant permet non seulement de s'appuyer sur une gestion centralisée des comptes mais aussi de conserver une meilleur traçabilité des demandes d'accès.
Ainsi plus de risque de compromission des secrets stockés localement sur le switch, les comptes local d'administrateur peuvent être désactivés. Lorsqu'un administrateur se connectera sur le switch, sa demande d'authentification est relayer vers le serveur RADIUS qui autorisera ou non sa connexion.
Il a quand même fallu définir un cas dégradé si par exemple le serveur RADIUS n'est plus joignable après X minutes, un profil local resterait accessible mais avec des droits limités.

J'ai rencontré quelques difficultés dans la configuration de l'authentification RADIUS. Les certificats clients que je générait pour faire mes essais ne possédait pas rôles (ou usages) suffisants c'est à dire : chiffrement de clé, signature numérique et authentification du client. De plus cette technologie étant nouvelle pour moi j'ai pris du temps pour effectuer des recherches et comprendre les mécanismes et méthodes d'authentification possible afin de séléctionner celle qui était le plus adapté.
Après un moment, je suis arrivé à une configuration stable et fonctionnel que j'ai finalement déployé sur la plateforme du projet et documenter l'ensemble des éléments liés (documentations techniques, procédures d'installation, d'utilisation et de maintenance)

## Bilan

Cette réalisation à été très enrichissante et m'a permis de me familiariser avec le contrôle d'acès 802.1X via un serveur RADIUS. J'ai également amélioré mes connaissances en terme de configuration de commutateur Cisco et de mise en oeuvre de la solution FreeRadius.
Peut importe la solution RADIUS choisit les principes d'authentification d'autorisation et de traçabilité sont les mêmes.
J'ai aussi pu étudier le protocole TACACS+, propriétaire Cisco, qui à été envisagé pour l'authentification des administrateurs sur les switches. Cette solution est plus perfomante et sécurisé cependant elle n'a pas été retenu car elle n'est pas supporté par la solution FreeRadius.

## Compétences mis en oeuvre
- Administration et sécurité des réseaux
- Administration système GNU/Linux
- Persévérance
