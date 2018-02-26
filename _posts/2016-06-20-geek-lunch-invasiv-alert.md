---
layout: post
title : Invasiv'Alerte
date: 2016-06-20
category: geek-lunch
speaker: Laurence Matringe et Stéphane Trainel
---

Présentation du projet développé pendant le hackathon #HackBioDiv par LM et ST

**Objectif : Détecter les populations invasives via les réseaux sociaux**

**1. Par une utilisation via l'interface de recherche des réseaux sociaux**

- Google Trends sur la recherche Frelon Asiatique : https://www.google.fr/trends/explore#q=%2Fm%2F07kf39s et une carte de France avec la localisation des recherches du terme : https://www.google.fr/trends/explore#q=/m/07kf39s&geo=FR
- Google Trends expose les résultats par entité nommée (Google Trends agrège toutes les termes de recherches qui font référence à la même chose "Frelon asiatique" ou son nom latin "vespa velutina" ou "Asian predatory wasp").
- Google Trends ajuste ses données (https://support.google.com/trends/answer/4365533?hl=fr&ref_topic=4365599) en fonction du nombre de requêtes totale pour une zone donnée, afin d'éviter les biais.
- Twitter sur la recherche Frelon asiatique : https://twitter.com/search?q=frelon%20asiatique&src=typd depuis la page de recherche avancée : https://twitter.com/search-advanced

Pistes d'explorations : 
- détecter la présence du frelon asiatique par les signes avant-coureurs des dégâts qu'il cause et que les internautes vont chercher dans le moteur de recherche ;
- comparer les résultats des réseaux sociaux avec ce qui est déclaré en mairie, et ce que les bases de données des ministères recèlent.


**2. Par une utilisation via l'API des réseaux sociaux**

Lorsqu'on veut automatiser la recherche de plusieurs termes ou enregistrer les résultats dans une base de données, on peut passer par une interrogation programmatique de services web en utilisant l'API proposée. On récupère alors non pas un page web HTML lisible par un humain comme les résultats ci-dessus, mais des données dans un format donné qui permettra ensuite une manipulation plus fine.
- Pour Twitter (il faut avoir un compte twitter) : avec son compte, possiblité d'essayer une partie de l'API ici https://dev.twitter.com/rest/tools/console ;
- Pour Google Trends, il faut passer par des librairies tierces (pour les plus aventuriers et les cool kids, c'est ici : https://www.npmjs.com/package/google-trends-api).


Le code servant à collecter les données Google Trends et Twitter issu du hackathon #HackBioDiv est ici : https://github.com/FredVest/hackbiodiv

Prérequis :
- un compte Twitter (https://twitter.com/), pour pouvoir créer une application et jouer avec l'API de Twitter
- un éditeur de texte, par exemple : https://www.sublimetext.com/
- avoir installé R https://cloud.r-project.org/
- avoir installé Python https://www.python.org/downloads/

L'utilisation de la recherche sur Twitter est limité à 7 jours. Pour des recherches sur des périodes plus longues il faut un compte payant.
