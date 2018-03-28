---
layout: post
title : Une API pour les avis urgents aux navigateurs
date: 2018-03-26
speaker: Antoine Augusti
---

En mer, il arrive que des événements puissent perturber la navigation en toute sécurité : épave, bouée disparue, phare en panne, tirs militaires etc. L'IMO (*International Maritime Organization*) et l'IHO (*International Hydrographic Organization*) imposent aux états signataires de la convention SOLAS (*Safety of Life at Sea*) de recenser et de diffuser les potentiels dangers à la navigation dans les eaux sous leurs responsabilités. Ces informations sont nommées *navigational warnings* dans les conventions internationales et appelées « avis urgents aux navigateurs » (abrégé AVURNAV) en France.

La diffusion de ces AVURNAV en France est assurée en mer par VHF, par les sémaphores notamment, après appel sur le canal 16 ou sur la fréquence 2 182 kHz, [NAVTEX][1] ou [Inmarsat][2]. Ces avis peuvent être également consultés dans les capitaineries des ports et sur [les sites des préfets maritimes][4]. Il nous semblait pertinent de regrouper ces AVURNAV en un seul lieu, facilement consommable par des systèmes informatiques. Cette volonté de proposer une API correspond à la logique d'État plateforme.

## Présentation de l'API

L'API proposée tire ses données des sites des Préfets Maritimes en France métropolitaine. En conséquence, seuls les AVURNAVs actuellement en vigueur dans les eaux sous l'autorité des Préfets Maritimes en France métropolitaine sont disponibles. Les données sont disponibles moins de 5 minutes après la publication de l'avis sur le site d'un Préfet Maritime.

L'API est disponible gratuitement et sans authentification. Une [documentation][5] est mise à la disposition des usagers ainsi qu'[un fichier de définition des endpoints][6] en Swagger 2.

Ce projet est proposé en [open source sur GitHub][7] et a été réalisé dans le cadre du programme [Entrepreneur d'Intérêt Général PrédiSauvetage][8]. L'API est réalisée en Go et est hébergée sur Heroku.

## Quelle suite ?

Pour le moment, la diffusion des *navigational warnings* n'est pas bien encadrée et chaque pays opère de la façon qu'il souhaite dans sa zone de responsabilité. Pour autant, l'IHO a mis en place un groupe de travail qui est en train de travailler sur une norme portant sur la communication des *navigational warnings*, pour une future [norme S-124][9].

Les spécifications suivent leurs cours et aucune date finale n'a été annoncée. Toutefois, le Danemark a déjà implémenté la spécification préliminaire et leur travail est disponible sur [GitHub][10] et sur [un site récapitulatif][11].

[1]: https://www.wikiwand.com/fr/Navtex
[2]: https://www.wikiwand.com/fr/Inmarsat
[3]: https://www.premar-atlantique.gouv.fr
[4]: https://www.premar-atlantique.gouv.fr
[5]: https://antoineaugusti.github.io/avurnav-api/
[6]: https://github.com/AntoineAugusti/avurnav-api/blob/master/docs.yml
[7]: https://github.com/AntoineAugusti/avurnav-api
[8]: https://entrepreneur-interet-general.etalab.gouv.fr/defi/2017/09/26/donneesauvetagemaritime/
[9]: http://iho.int/srv1/index.php?option=com_content&view=article&id=611&Itemid=850&lang=en
[10]: https://github.com/NiordOrg
[11]: http://docs.niord.org
