---
title: "Zone Délimitarisée (DMZ)"
date: 2018-09-12T14:51:12+06:00
author:
#image_webp: image
image: images/realisation/pro/controle-commande.jpg
#description : "This is meta description"
---

## Introduction

Durant la réalisation d'un projet de sécurisation d'un système informatique de contrôle commande existant, nous mettons en oeuvre une zone démilitarisée pour cloisonner et filtrer les flux entre deux systèmes de niveau de sécurité hétérogène.
La quasi totalité des systèmes d'informations est interconnecté avec un autre réseau, très souvent Internet. Dans des contextes industriels, le système informatique peut être interconnecté avec le réseau d'un partenaire ou d'un constructeur.
L'interconnexion d'un système constitue aujourd'hui, de manière incontestable, une source importante de menaces. 

Pour certains SI, l'interconnexion avec Internet permet de mettre à disposition des services tel que des serveurs web, service collaboratifs, serveur de messagerie et de permettre biensur l'accès à Internet aux collaborateurs.
Dans l'objectif de renforcer les mesures de sécurité de cette interconnexion, la première étape commence par identifier formellement les besoins nécessaires liés à l'interconnexion. Souvent les besoins sont mal définie et donc les configurations trop permissives. Ce travail préliminaire permettra de facilier le travail dans l'établissement de matrices des flux et de règles de contrôles d'accès.

Dans le contexte du projet, le système de contrôle commande est relié aux SI bureautiques et à Internet. Par conséquent le risque de menace augmente de manière significative.
Après avoir défini avec notre client, les besoins liés à l'interconnexion de son système, nous lui proposons une architecture technique d'interconnexion via une zone démilitarisée DMZ.

Pour rappel, une DMZ est un concept utilisé pour séparer deux zones de confiance hétérogène grâce à des pare-feux rélisant un filtrage de part et d'autre.

 ## Mise en oeuvre

Nous travaillons en équipe de deux pour la définition et la réalisation de la DMZ.
L'architecture se compose de deux firewalls par lesquel le lien d'interconnexion passe. Les deux firewalls sont de constructeur différent ce qui permet en cas de vulnérabiltié découverte sur un des deux firewalls de conserver un niveau de sécurité acceptable.

Entre les deux firewalls, au sein même de la DMZ dans la zone de services exposés, un serveur est présent et accessible par les deux zones de confiance via des protocoles web. 

Le premier travail à été de construire une matrice des flux qui permet de lister l'ensemble des flux jusqu'à la couche 4 du modèle OSI.
Ce travail permettra de base de travail lors de la configuration mais il permet surtout de pouvoir identifier chaque flux et de le justifier.

Nous reportons également une fonctionnalité de tunnel VPN pour l'accès au système de contrôle commande par le personnel de maintenance à travers Internet.
Nous choisissons d'utiliser la technologie VPN SSL qui permet à des utilisateurs distants d'accéder de manière sécurisée aux ressources du système informatique du client. Toutes les communications entre l'utilisateur distant et le site central sont alors encapsulées et protégées via un tunnel chiffré en SSL.

En plus des règles de filtrage standard mise en oeuvre, nous utilisons la fonctionnalité de prévension intrusion (IPS) qui permet de réaliser une analyse en temps réel des différents flux transport et applicatif transitant par le firewall pour identifier et bloquer les menaces. Ces analyses sont réalisés grâce à des modules d'inspection dédiés à chaque protocole comme par exemple HTTP, FTP, etc.

Malheuresement les mécanismes de protection traitionnels à base de signature ne sont plus autant efficace. Pour répondre à ce nouvelle besoin, des technologies de nouvelle génération voit le jour basé sur l'analyse comportemental.

Contrairement au système de détection d'intruction (IDS), le système de prévention d'intrusion est actif et va pouvoir stopper le trafic suspect en bloquant les ports. Ces nouvelles technologies ne sont pas infaillible et possèdent quelques inconvénients comme :
- Bloquer du traffic légitime ;
- Autoriser du traffic illégitime ;
- Ils peuvent faire l'objet de vulnérabilité et donc être exploité et détourner ;
- L'analyse augmente la charge du processeur ;
- Le contenu des flux chiffrés ne sera pas analyser.

Nous avons défini une politique d'analyse pour certaines règles afin de s'assurer des ports réseaux utilisés, de restreindre certaines commandes, analyse sur les signatures. L'analyse comportemental à été précédé d'une phase d'apprentissage pour fixer un fonctionnement "normal". Par le suite, l'IPS bloquera toute situation qui divergera du niveau de fonctonnement de référence.

L'analyse comportemental à une réel plusvalue car permet de détecter et bloquer les nouveaux types d'attaques.

## Bilan

Cette réalisation m'a permis d'approfondir connaissance en sécurité réseau, particulièrement sur les aspects de configuration des commutateurs.
J'ai également pu me familiariser avec les différents types d'attaques réseaux ainsi que les mesures permettant de s'en protéger.

Même si les commutateurs ne doivent pas être considérés comme des équipements de sécurité, leur rôle est souvent trop négligé dans la mise en place de mesures de sécurisation du système.

## Compétences mis en oeuvre

- Administration et sécurité des réseaux
