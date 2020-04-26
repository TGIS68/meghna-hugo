---
title: "Infrastructure sécurisé Active Directory"
date: 2018-09-12T14:51:12+06:00
author: Mark Dinn
#image_webp: image
image: images/realisation/pro/controle-commande.jpg
description : "This is meta description"
---

## Introduction

Dans le cadre d'une migration d'un système numérique de contrôle commande de processus industriel dans le domaine de distribution éléctrique, le client exprime à travers son cahier des charges des besoins de centralisation utilisateurs ainsi qu'un besoin de renforcer la sécurité de son infrastructure.

Pour répondre à ce cahier des charges, notre cellule cybersécurité propose la mise en oeuvre d'une architecture Microsoft Active Directory pour la centralisation des authentifications, comptes et ressources.
Pour renforcer le niveau de sécurité du système, l'ensemble des postes et serveurs subissent un durcissement par l'application de règles de sécurité diffusées par l'Active Directory.

## Mise en oeuvre

Nous avons travaillé en équipe avec deux autres collaborateurs pour la réalisation de ce projet.

Un contrôleur de domaine est un élément critique d’un système dans tous les aspects de sécurité :
-	Confidentialité : Il héberge des clés secrètes utilisées par le système et ses utilisateurs pour le chiffrement et l’authentification.
-	Intégrité : Il héberge et publie les fichiers de configuration qui sont appliquées aux différents éléments du système, y compris la configuration de sécurité.
-	Disponibilité : L’accès aux fonctions du contrôleur de domaine est nécessaire pour l’authentification des ordinateurs et des utilisateurs, et pour le bon fonctionnement du système en général.
 De fait, il consistue une cible privilégiée pour une personne malveillante. 

Par conséquent, l'Active Directory est installé sur deux controlleurs de domaine répliqué. Ces serveurs sont installés en Windows Server 2016 Core. Le mode est une installation minime qui ne contient l'environnement graphique complet. 
L'avantage de cette installation est que par définition ce mode limite la surface d'attaque du serveur car utilise moins de service et fonctionnalité.
Le désaventage est que seul une console powershell permet d'intéragir avec le serveur et ces fonctionnalités.

Pour limiter les erreurs et faciliter l'administration, la mise en oeuvre d'un poste d'administration est la bienvenue. Microsoft propose de nombreux outils d'administration à distance, qui permettent d'installer, configurer et maintenir le service Active Directory. Ce poste est dédié à cette utilsiation et les accès logique au système sont reservés aux administrateurs préalablement identifié et autorisé.

Active Directory est une technologie complexe qui propose de nombreuses options de configuration. Il propose notamment une fonctionnalité, les stratégies de groupe (Group Policy Object - GPO) qui sont des configuration pouvant être appliqué à un groupe d'utilisateurs ou d'ordinateurs. Elles sont principalement utilisée pour :
- Imposer un niveau de sécurité ;
- Créer des configurations communes ;
- Simplifier le process d'installation des ordianteurs.

Le système de stratégie de groupe est souple et très puissant, le pannel de stratégie proposé est nombreux. Cependant ces stratégies ne sont pas suffisante pour assurer un niveau de sécurité des postes et serveurs optimales. Nous avons réalisé un travail important afin de définir pour les versions serveurs et clientes de Windows, les services, fonctionnalités et applications nécessaires au fonctionnement du système dans le but de désactiver tout ce qui ne l'est pas.
C'était un travail important mais nécessaire pour limiter fortement la surface d'attaque car de nombreuses vulnérabilités résident dans ces composants logicielles qui sont parfois présent mais non nécessaire.

La configuration globale du système peut prendre un temps considérable si elle est réalisé manuellement. Par chance le language de scipting Windows Powershell répond parfaitement à cette problématique.
En développant un script écrit en Powershell, nous arrivons à faciliter les opérations d'installations et de configuration en les rendant automatique.

## Conclustion
Cette réalisaton m'a permis de mettre en pratique les compétences que je possédait déjà sur les environnements Microsoft Windows et Active Directory et m'a permis d'en acquérir d'autre, notamment sur le fonctionnement avancé du système d'exploitation et du service Active Directory.
Les environnements Microsoft Windows ont beau l'air simple de configuration du à l'environnement graphique, ils peuvent complexes lors qu'on décide de durcir le système ou de mettre en oeuvre des fonctionnalités avancées.









L'active Directory est supporté à travers de deux controlleurs de domaine redondant installé en Windows Server 2016 core.
Le choix de l'installation en mode core permet principalement de réduire la surface d'attaque des serveurs en limittant l'installation de l'environnement graphique complet.
La Configuration des controlleurs de domaine devient cependant plus "difficile" et doit être réalisé en Powershell.


J'ai eu la chance d'être désigné comme leader technique sur ce projet ainsi j'ai pu dès le stade de l'offre suivre ce projet en passsant par les différents cycles de vie du projet.
J'ai du suivre les différents points techniques du projet
- Etude prémilinaire : Définition des besoins en terme de protection contre les menaces
      - Etude du contexte 
      - Analyse de risque cybersécurité
      - Expression des exigences et objectifs cybersécurité
      - Plannification
- Etude détaillé : 
      - Définition des mesures cybersécurité
      - Définition des références matériels et choix des technologies
      - Dossier d'architecture préliminaire
      - Revue de conception détaillée
- Réalisation  :
      - Déploiement des mesures et configurations
      - Suivi des tâches techniques
      - Résolution d'anomalie
      - Réunion d'avancement
      - Veille de vulnérabilité et mise à jour
- Validation : 
      - Test des mesures de sécurité
      - Enumération des risques résiduels

Nous avons procédé au durcissement du système d'exploitation Windows et notamment par la désactivation des services et fonctionnalités inutiles, la désactivation des protocoles obselètes ou non sécurisé. Un travail important et minutieux à été réalisé sur cette partie. Le déploiement et l'installation des configurations est réalisé de manière automatique à travers des scripts powershell que nous avons développé.
La difficulté à résidé dans le maintien de la fonction de contrôle commande assurée par une solution SIEMENS. En effet il a fallu tenir compte des exigences de configuration fournit par le constructeur et parfois ajuster les mesures de sécurité pour assurer une continuité.

