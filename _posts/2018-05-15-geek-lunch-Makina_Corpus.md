---
layout: post
title : État de l'art des technologies open source pour la cartographie - focus sur le tuilage vectoriel
date: 2018-05-15
category: geek-lunch
speaker: Frédéric Bonifas, Jean-Pierre Oliva, Olivia Duval et Simon Georges
---

**Pitch initial**
Cette session a été consacrée à l'état de l'art des technologies open source pour la cartographie en matière de tuilage vectoriel. Nos intervenants travaillent chez [Makina Corpus](https://makina-corpus.com), élue entreprise Open Source de l’année au Paris Open Source Summit :
- Frédéric Bonifas, développeur carto ;
- Jean-Pierre Oliva, fondateur de Makina Corpus ;
- Olivia Duval, directrice de Makina Corpus Paris ; 
- Simon Georges, expert Drupal et SEO.


# Présentation

---

## [Makina Corpus](https://makina-corpus.com/)

* Société de Services en Logiciels Libres (SSLL)
* Développement d’applications web et mobiles
(application métier, front-end, cartographie, CMS, mobile, data)
* Audits
* Formation

---

## Tuiles

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/tuiles.png) <!-- .element style="float:right; max-width:40%" -->

Ensemble d’images de 256x256 pixels

<ul>
  <li>Images précalculées</li>
  <li>Mise en cache</li>
  <li>Au déplacement, seules les tuiles manquantes sont chargées</li>
</ul>

---

### Tuiles raster

* Format image (PNG, JPG)
* Rendu des images par le serveur
* Ressources serveur potentiellement conséquentes (stockage, CPU)
* Très classique

---

### Tuiles vectorielles

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/square-of-math.gif)<!-- .element height="300px"  -->

* Principe de tuiles conservé
* Données brutes vectorielles plutôt que des images précalculées
* Propriétés des objets accessibles
* Format binaire Protobuf
* Rendu par le client

---

# Par l'exemple

Comment représenter un GeoJSON de 400 Mo dans un navigateur web et interagir avec celui-ci ?

Les [bâtiments de Paris](https://opendata.paris.fr/explore/dataset/volumesbatisparis2011/export/) par exemple

---

## Caractéristiques et avantages des tuiles vectorielles

---

### Changement de style à la volée

* Un même jeu de tuiles pour différents contextes
* Affichage des différentes propriétés d'un objet
* N'importe quelle grandeur présente dans les données peut être utilisée

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/style.gif)

---

### Orientation et rotation de la caméra

* Rendu en 3D
* Texte toujours orienté dans le sens de lecture

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/3d.gif)

---

### Requêtes instantanées sur les objets

* Pas besoin d'un appel à une API pour obtenir les propriétés des objets
* Accès à la géométrie et aux propriétés
* Opérations géométriques sur les objets (ex : cluster, Voronoï etc.)

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/interaction.gif)

---

### Autres avantages

* Poids réduit
* Rendu amélioré pour les écrans haute-définition
* La carte peut être rendue à n'importe quelle échelle

---

### Tuiles vectorielles - exemples

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/openocean-vt-zoom.gif)

---

### Tuiles vectorielles - exemples

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/wavely.png)

---

### Tuiles vectorielles - exemples

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/170130_visu_valoiti_white.jpg)

---

### Tuiles vectorielles - exemples

![](https://mtes-mct.github.io/numerique/media/2018-05-15-geek-lunch-Makina_Corpus/moodwalkr-profiles.gif)

---

# Solutions techniques

---

## Générer des tuiles vectorielles


* Utilisation de tuiles vectorielles existantes
* Serveur : [t-rex](https://github.com/t-rex-tileserver/t-rex)
* Depuis un GeoJSON : [Tippecanoe](https://github.com/mapbox/tippecanoe)
* Depuis PostGIS : Function *ST_AsMVT*

---

## [t-rex](https://github.com/t-rex-tileserver/t-rex)

* *Servir facilement des tuiles vectorielles depuis une base PostGIS*
* Création des tuiles et serveur intégré
* Paramétrage fin des couches et des niveaux de zoom

---

<!-- .slide: class="alternate" -->
## t-rex : Création de la base PostGIS

```sh
dbname=bbl
dbuser=gisuser
dbpass=corpus
sudo -u postgres -s -- psql -c "CREATE USER ${dbuser} WITH PASSWORD '${dbpassword}';"
sudo -u postgres -s -- psql -c "CREATE DATABASE ${dbname} OWNER ${dbuser};"
sudo -u postgres -s -- psql -d ${dbname} -c "CREATE EXTENSION postgis;"
```

Ou avec PgAdmin

---

<!-- .slide: class="alternate" -->
## t-rex : Importer des données OSM

* Récupérer des données OSM
* Installer `osm2pgsql`
* `sudo -u postgres -s -- osm2pgsql -d ${dbname} data.osm`

---

<!-- .slide: class="alternate" -->
## t-rex : Générer des tuiles vectorielles

* [Installer t-rex](http://t-rex.tileserver.ch/)
* Générer automatiquement un fichier de conf:
```
t_rex genconfig --dbconn postgresql://gisuser:corpus@localhost/bbl
```
* Servir les tuiles:
```
t_rex serve --config trexconfig.toml
```

**⚠ `query_limit` et `geometry_type`**

---

## [Tippecanoe](https://github.com/mapbox/tippecanoe)

* *Conserver l'aspect des données quel que soit le niveau de zoom*
* Gestion de gros jeux de données
* Nombreuses stratégies de simplification et aggrégation

---

<!-- .slide: class="alternate" -->
## Tippecanoe : Générer les tuiles

* Conversion du GeoJSON en tuiles vectorielles :
```
tippecanoe
-o volumesbatisparis2011.mbtiles
--maximum-zoom=g
--drop-smallest-as-needed
--read-parallel
--detect-shared-borders
volumesbatisparis2011.geojson
```

&rarr; Fichier *Mbtiles*

---

<!-- .slide: class="alternate" -->
## Tippecanoe : Servir les tuiles

* Pas de serveur intégré à Tippecanoe, on utilise [tileserver-gl](https://github.com/klokantech/tileserver-gl) par exemple

```
docker run --rm -it -v $(pwd):/data -p 8080:80 klokantech/tileserver-gl
```

---



## Visualiser des tuiles vectorielles
## Bibliothèques JavaScript

---

### [Leaflet](http://leafletjs.com/)

* Créé en 2011 par Vladimir Agafonkin, travaillant à l'époque chez Cloudmade
* Porté par Mapbox et par la communauté maintenant
* Volonté de fournir une bibliothèque OpenSource légère, performante et simple d'utilisation
* Très nombreux plugins
* Pour les tuiles vectorielles : [mapbox-gl-leaflet](https://github.com/mapbox/mapbox-gl-leaflet) et [Leaflet.VectorGrid](https://github.com/Leaflet/Leaflet.VectorGrid)

---

### [OpenLayers](https://openlayers.org/)

* Bibliothèque historique
* Gère nativement de nombreux formats (tuiles vectorielles...)
* Nombreuses méthodes natives

---

### [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/)

* Bibliothèque open source, très largement maintenue principalement par Mapbox
* Le bon choix pour les tuiles vectorielles
* Encore peu de communautés et de plugins
* Problèmes de performance dans Firefox

---

## Tuiles et rendu

---

## Autres outils ##

* Studio libre de création de style
  * [Maputnik](https://maputnik.github.io/)
* dans QGIS
  * Plugin *Vector Tiles Reader*
* Avec GDAL
  * [Gestion des tuiles vectorielles](http://www.gdal.org/drv_mvt.html) depuis la version 2.3 (Mai 2018)

---

## Difficultés avec les tuiles vectorielles

- Quelle bibliothèque JS choisir ?
- Gestion de gros volumes de données (tuning PostGIS)
- Choix de simplification aux petites échelles
- Évolution rapide des outils

---

# Discussion et questions

---

# Pour aller plus loin

* [Spécification](https://github.com/mapbox/vector-tile-spec/tree/master/2.1)
* [Liste d'outils autour des tuiles vectorielles](https://github.com/mapbox/awesome-vector-tiles/)
