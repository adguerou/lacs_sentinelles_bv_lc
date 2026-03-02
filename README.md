# Bassin versant et occupation du sol
Ce dépot git permet le calcul des bassins versants et occupation du sol des lacs Sentinelles. Ces analyses sont basées sur les MNTs issus du [lidar HD de l'IGN](https://geoservices.ign.fr/lidarhd) et l'analyse des données du satellite Sentinel-2 pour l'occupation du sol.

Figures et statisitques sont ainsi générées, ce qui a permis entre autres d'obtenir les animations 3D mis en ligne sur le site internet pour chaque lac du réseau [[exemple]](https://www.lacs-sentinelles.org/fr/lacs/lac-danterne#:~:text=atteint%2012%20m.-,Animation%203D%20%3A,-%3D%3E%20Vue%203D%20du)

## 1. Téléchargement
Ce dépot doit être cloner localement en suivant ces instructions suivant le système d'exploitation: 
* https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository

Un simple téléchargement peut aussi se faire pour plus de simplicité.


## 2. Dépendances
Pour faire tourner les codes de ce dépot, un autre module python est nécessaire pour faciliter le traitement des données spatialisés, ainsi que le téléchargement deux dépots de données:

### Code
* pyce: https://github.com/adguerou/pyce.git

Son installation passe par la création d'un environement python, avec [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) par exemple, puis:

``cd <install_directory>``

``pip install -e .``

### Données
* grille lidar HD: [https://zenodo.org/uploads/18790013](https://zenodo.org/records/18790013?preview=1&token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6IjRlNGJjMGIzLTNiMzMtNDEyMi1iZjQwLTFiNmQxODc4NDU4NiIsImRhdGEiOnt9LCJyYW5kb20iOiI5ZGNmYmNjZGZiMDkzNThmYjU1MzU2ZjVhOTkxMjA1YyJ9.eOJ33NP09cPBJ83OyBPXAkqT9EDCpvsP4CNyTEddsF7z7CGRvW4PaK8hu2wSGyKla65xRF_rOPgvlpiHiq6Qxg)
* MNTs procéssés: [https://zenodo.org/uploads/18790210](https://zenodo.org/records/18790210?preview=1&token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6IjM3ZmZiZTg2LTljOWEtNDZlZS1hZjljLWJhMjc4YTU4MjBlNyIsImRhdGEiOnt9LCJyYW5kb20iOiIyMDlmNmIwMTZkOGZhYWQ0NTQ3YjlmNzQ4YmQzNzYyZCJ9.IG-FC5kuOY2OrbHHfGMAbZsURajLFJuQTdwW6otJo4j0wO9i6WSq560bD5-foLv1Ka9xEg2VSDr6GJ1wJeyv4Q)

Une fois ces téléchargement réalisés, les dossiers <mark>dem_main_lakes/</mark> et <mark>dem_extra_lakes/</mark> sont à copiés et renomer <mark>dem/</mark> dans les dossiers respectifs <mark>"/data/main_lakes/."</mark> et <mark>"/data/extra_lakes/."</mark> en local (obtenu à partir du repo GIT). Cela permet d'avoir la structure nécessaire des sous dossiers pour le bon fonctionnement du processing. 

## 3. Contenus des dossiers

* analysis/: notebook à exécuter pour calculer les bassins versants et extraire les occupation du sols
* data/: données (MNT et occuation du sol) brutes et processées
* delivery/: fichiers finaux / les mêmes que diffusé par Lacs Sentinelles
* qgis/: fichier de style pour l'occupation du sol sous QGIS

## 4. How to

L'analyse se fait à partir des notebooks situés dans le dossier "analysis". Des commentaires tout au long de ces derniers expliquent dans un certains détails la procédure à suivre. Du travail manuel sous QGIS est également nécessaire et mentionné.

Les notebooks **01_main_ls_bc_lc. ipynb** et **02_extra_bv_lc font.ipynb** font typiquement la même chose, simplement sur des listes de lacs différents, et dans un contexte de nouveau lac à rajouter à une liste déjà existante pour le notebook 02. C'est donc ce notebook (le 02) qu'il faudra utiliser pour de potentiel futur lacs. Le notebook **xx_lc_guerou_et_al_2026.ipynb** est simplement là pour illustrer comment l'occupation du sol à été calculé mais n'est pas reproductible tel quel. Les données d'occupation du sol sont de toutes façon disponibles sur toute la zone alpine et pyrénéennes (voir section ci dessous)

Ces notebooks 01 et 02 comportent 4 sections:
  1. Creation des MNTs
  2. Calcul des bassins versants
  3. Création des produits du dossier delivery (dont l'occupation du sols)
  4. Creátion du fichier de statistiques et des figures

### Les MNTs
Les MNTs du lidar HD n'étaient pas disponible début 2024 lors des premiers travaux. Un travail préliminaire était donc nécessaire (section 1) mais à l'heure actuelle cette étape peut être évitée (longue et technique) en sautant les section $1.3 et $1.4.4 (du notebook 02), en ayant téléchargé les dalles MNT directement sur le site IGN auparavant [téléchargement ici](https://cartes.gouv.fr/telechargement/IGNF_MNT-LIDAR-HD).

### Les bassins versants
Le code qui réalise cette opération est basé sur ce module python [pysheds](https://github.com/pysheds/pysheds?tab=readme-ov-file) et suit les mêmes étapes. Le traitement du "flattening" des lacs ainsi que la gestion de plusieurs bassin versants à été automatisé du mieux possible. Certaines manips comme la définition des éxutoirs ("outlet") reste cependant manuelle sous QGis (car également plus simple à visualiser).

### Création des produits
Le dossier **delivery/** est créé dans la section $3 du notebook et contient les choses suivantes: 

 * A "lake_by_lake" folder containing the data grouped by lake.
 * A "lake_by_region" folder containing the data grouped by the following regions: "Alps", "Pyrenees", and "Corse".
 * A "statistics" folder with the lake, water sheds and landcover surfaces statistics.
 * An "ancillary" folder containing the coordinates of the lakes
 * A "figure" folder containing all the summary plots

#### Lakes data / "lake_by_lake" folder
Three types of products are available for each lake: 
	- the lake extent in .shp format (geolocated shapefile) - "lacsSentinelles_lakes_<lake>.shp"
	- the water shed extent in .shp format (geolocated shapefile) - "lacsSentinelles_sheds_<lake>.shp"
	- a landcover map in .shp format (geolocated shapefile) - "lacsSentinelles_landcoverS2_2017_2023_<lake>.shp"
	- a summary plot in .png format - "lacsSentinelles_<lake>.png"


#### Regional data / "lake_by_region" folder
Lake, water sheds and landcover data are grouped by the following regions: "Alps", "Pyrenees" and "Corsica". This is the same data as in "lake_by_lake" folder.

#### Ancillary
The lakes center and outlet coordinates are available in "lacsSentinelles_coords_<date_run>.csv" files. This is in EPSG:2154 projection/


### Statistics
Two summary tables are available: 
 * "lacsSentinelles_statistics.csv": lists the lake, water sheds and landcover surfaces for all the lakes
 * "lacsSentinelles_statistics_percent.csv": lists the land landcover percentage as compare to the water shed surface for all the lakes

Some metadata such lake altitude, water shed mean and max altitude are also indicated in these summary tables. 

### Occupation du sol
Les données d'occupation du sol sont directement disponibles dans le dossier **data/** et sont clipés au bassin versant des lacs considérés lors de l'analyse (section $3). Ces cartes sont issus des travaux de Guerou et al (2026) présenté succintement dans le notebook **xx_lc_guerou_et_al_2026.ipynb**. Un fichier de style Qgis est disponible dans le dossier **qgis/** qui donne également la correspondance landcover <-> code LC.

## 5. Methods
Pour la curiosité des personnes intéressées, voici quelques détails supplémentaires des méthodes utilisées pour ces analyses

### Water sheds
We processed lidarHD classified point cloud data from IGN program to 1m resolution and used python module 'pysheds' (Bartos  2020) to delineate water sheds. To improve water shed delineation, we previously flattened all lake surfaces thanks to the 'sheds.py' module from 'aguerou' git repository (https://github.com/adguerou/pyce/blob/main/src/pyce/sheds.py). We used lake's coordinates avaialble in the ancillary folder for such processing.

### Landcover
The landcover data of the 30 lakes of Lacs Sentinelles have been obtained using Sentinel-2 data over summer months (15th of July to 15th of August) over the 2017-2024 period. The vegetation has been mapped using a combination of the NARI (Bayle et al. 2019) anc NCRI satellite indices that we used to feed a random forest algorithm trained on >20.000 points over the European Alps. Water extent has been mapped using a mix of NDWI index and manual editing of the water surface obtained from the lidar data. Glacier surfaces come from the RGI database as of 2015 (Pfeffer et al. 2014 / Paul et al. 2015).


# Terms of use
Data are free of use for non-profit work only, and under conditions of citing the different sources as follow:

"The water sheds  have been obtained from lidarHD IGN data and python module 'pysheds' from Bartos et al. (2020, Pysheds: simple and fast watershed delineation in python). The landcover maps and statistics have been produced using Copernicus Sentinel-2 data through Google Earth Engine platform (Gorelick et al., 2017. Google Earth Engine: Planetary-scale geospatial analysis for everyone. Remote Sensing of Environment) and processed partially with python module 'geemap' (Wu, Q., 2020. geemap: A Python package for interactive mapping with Google Earth Engine. The Journal of Open Source Software, 5(51), 2305). We used data from Bayle et al. (2019) and applied the method presented in Guerou et al. (submitted) to train the landcover classifier."  


