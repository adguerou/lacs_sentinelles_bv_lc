# Bassin versant et occupation du sol
Ce dépot git permet le calcul des bassins versants et occupation du sol des lacs Sentinelles. Ces analyses sont basées sur les MNTs issus du [lidar HD de l'IGN](https://geoservices.ign.fr/lidarhd) et l'analyse des données du satellite Sentinel-2 pour l'occupation du sol.

Figures et statisitques sont ainsi générées, ce qui a permi entre autres d'obtenir les animations 3D mis en ligne sur le site internet pour chaque lac du réseau [[exemple]](https://www.lacs-sentinelles.org/fr/lacs/lac-danterne#:~:text=atteint%2012%20m.-,Animation%203D%20%3A,-%3D%3E%20Vue%203D%20du)

## Téléchargement et installation
Ce dépot doit être cloner localement en suivant ces instructions suivant le système d'exploitation: 
* https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository

## Dépendances
Pour faire tourner les codes de ce dépot, un autre module python est nécessaire pour faciliter le traitement des données spatialisés, ainsi que le téléchargement deux dépots de données:

### Code
* pyce: https://github.com/adguerou/pyce.git

### Données
* grille lidar HD: [https://zenodo.org/uploads/18790013](https://zenodo.org/records/18790013?preview=1&token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6IjRlNGJjMGIzLTNiMzMtNDEyMi1iZjQwLTFiNmQxODc4NDU4NiIsImRhdGEiOnt9LCJyYW5kb20iOiI5ZGNmYmNjZGZiMDkzNThmYjU1MzU2ZjVhOTkxMjA1YyJ9.eOJ33NP09cPBJ83OyBPXAkqT9EDCpvsP4CNyTEddsF7z7CGRvW4PaK8hu2wSGyKla65xRF_rOPgvlpiHiq6Qxg)
* MNTs procéssés: [https://zenodo.org/uploads/18790210](https://zenodo.org/records/18790210?preview=1&token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6IjM3ZmZiZTg2LTljOWEtNDZlZS1hZjljLWJhMjc4YTU4MjBlNyIsImRhdGEiOnt9LCJyYW5kb20iOiIyMDlmNmIwMTZkOGZhYWQ0NTQ3YjlmNzQ4YmQzNzYyZCJ9.IG-FC5kuOY2OrbHHfGMAbZsURajLFJuQTdwW6otJo4j0wO9i6WSq560bD5-foLv1Ka9xEg2VSDr6GJ1wJeyv4Q)

Une fois ces téléchargement réalisé, les dossiers <mark>dem_main_lakes/</mark> et <mark>"dem_extra_lakes/"</mark> sont à copiés dans les dossiers respectifs <mark>"main_lakes"</mark> et <mark>"extra_lakes"</mark> en local (obtenu à partir du repo GIT). Ces dossiers doivent être ensuite à renomer <mark>"dem/"</mark> tous les deux afin d'avoir la structure nécessaire des sous dossiers qui fonctionnent pour le processing. 
