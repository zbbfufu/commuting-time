commuting-time
==============

![Isochrone map from Atelier01](/atelier01-screenshot.png?raw=true)

English
-------

> The aim of this project is the generation of isochronous maps from public transit datas in [GTFS][GTFS] format.
> These maps help to visualize geographical areas in a range limited by transit time from one location.
> 
> There are already some software components to achieve this goal.
> The work on this project will be to integrate these components into a "turnkey" software.
> There will be research and documentation, as well as some components to be developed (GUI, business services, ...).

Français
--------
> L'objectif de ce projet est la génération de cartes isochrone à partir de données de transport au format [GTFS][GTFS].
> Ces cartes facilitent la visualisation des zones géographiques accessibles en un temps limité en transport en commun à partir d'un lieu donné.
> 
> Il existe déjà un certain nombre de composants logiciels permettant d'atteindre cet objectif.
> Le travail sur ce projet sera d'intégrer ces différents composants pour en faire un logiciel "clé en main".
> Il y aura de la recherche et de la documentation, ainsi que quelques composants à développer (interface graphique, services métier, ...).

Status updates
--------------
- *2014-08-21* : completed dockerfile. you can build and run to get a postgres with postgis and pgrouting, and a phppgadmin web interface. User for both postgres and web ui is docker/docker. GTFS data are loaded in "commtimes" database, schema "gtfs".
- *2014-08-17* : create a dockerfile ready for pgrouting. GTFS datas successfully loaded in database with gtfs2pgrouting, but not computed for routing !? Should investigate. If gtfs2pgrouting do not more than loading in db, it should be better to load gtfs from web application in front of postgresql.
- *2014-07-18* : fill this README and push a proof of concept over openlayer and geojson
- *2014-07-17* : project is alive


Data
----
This project targets [GTFS][GTFS] as data source format.
Here are some provider for thoses datas :

* http://opendata.stif.info/explore/dataset/offre-horaires-tc-gtfs-idf/ : public transit from all operators associated with the "stif" association, Île-de-France, France.
* http://data.ratp.fr/explore/dataset/offre-transport-de-la-ratp-format-gtfs/ : public transit operated by RATP in Paris proper, France
* https://ressources.data.sncf.com/explore/dataset/sncf-ter-gtfs/ : French regional trains operated by SNCF
* https://ressources.data.sncf.com/explore/dataset/sncf-intercites-gtfs/ : French "city-to-city" trains operated by SNCF
* https://ressources.data.sncf.com/explore/dataset/sncf-transilien-gtfs/ : public transit (trains, subway, buses, streetcar) operated by SNCF in Île-de-France, France
* https://ressources.data.sncf.com/explore/dataset/sncf-tram-train-ter-pdl-gtfs/ : public transit in Pays-de-la-Loire, France
* http://data.keolis-rennes.com/fr/les-donnees/donnees-telechargeables.html : public transit in Rennes, France

Feel free to add other providers :)


Technical
---------

Here is some useful components and documentations :

- [postGIS][PGIS] and [pgRouting project][PGR] are geographical and routing extensions for [postgresql][PG] (note : both available as debian package)
- [gtfs2pgrouting] is for importing GTFS into pgrouting
- [OpenLayers 3][ol3] and [LeafLetJS][leafletjs]  are js libs to display data layers over geo maps

- [Google transit][GoogleGTFS] is the google page for GTFS specification
- [MMPTR-Tutorial] is a small tutorial for gtfs and pgrouting
- [Anita Graser blog][AnitaGraser] contains useful tips to calculate isochrones with pgrouting.
- [Atelier01] : Someone did what we expect to have at end, but not complete enough, and not open-sourced

Installation
------------
Todo

License
-------
Affero GPL


**Free Software, Hell Yeah!**
[GTFS]:http://fr.wikipedia.org/wiki/General_Transit_Feed_Specification
[GoogleGTFS]:https://developers.google.com/transit
[PG]:http://www.postgresql.org
[PGIS]:http://www.postgis.net
[PGR]:http://pgrouting.org
[gtfs2pgrouting]:https://github.com/justjkk/gtfs2pgrouting
[MMPTR-Tutorial]:https://github.com/pgRouting/pgrouting/wiki/MMPTR-Tutorial
[AnitaGraser]:http://anitagraser.com/tag/pgrouting/
[Atelier01]:http://www.atelier01.net/metro/paris/isochrone?latlng=48.86191977558759,2.3466110229492188
[ol3]:http://openlayers.org
[leafletjs]:http://leafletjs.com
