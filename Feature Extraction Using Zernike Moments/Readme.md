
# Feature Extraction Using Zernike Moments

## Introduction :
L’utilisation des moments de Zernike dans l’analyse d’images a été lancée par Teague [[1]](https://www.osapublishing.org/josa/viewmedia.cfm?uri=josa-70-8-920&seq=0) . Les moments de Zernike sont des entités extraites en projetant l’image d’entrée sur un ensemble complexe de polynômes de Zernike.
Le calcul des moments de Zernike à partir d’une image d’entrée comprend trois étapes :
1.	Le calcul des polynômes radiaux
2.	Le calcul des fonctions de base de Zernike 
3.	Le calcul des moments de Zernike en projetant l’image sur les fonctions de base de Zernike [[2]](https://www.sciencedirect.com/science/article/abs/pii/S0888327009001228).

## Méthode et résultats :
Les moments de Zernike ont fait l’objet de larges investigations et sont aussi toujours largement utilisés. Cette approche consiste à projeter l’image dans un espace vectoriel en utilisant un ensemble de polynômes orthogonaux (les polynômes de Zernike).


Pour calculer les moments de Zernike nous avons implémenté un algorithme sous python en s’appuyant sur un article [[3]](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Feature%20Extraction%20Using%20Zernike%20Moments/images%2Bdoc/1-s2.0-S0031320306001166-main.pdf).


Afin de tester le code, nous avons utilisé des images typiques présentant des formes (ovale, rectangle, nuage) et des versions pivotées de ces formes. La figure ci-dessous montre les résultats de l’application de l’algorithme sur ces images (Amplitude et phase pour ordre n=5 et répétition m=1).


![alt text](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Feature%20Extraction%20Using%20Zernike%20Moments/output.png?raw=true)

Les dernières images ne sont que des versions tournées d'un seul objet (nuage), les amplitudes des moments de Zernike pour ces deux images sont les mêmes (invariance de rotation). De plus, les différences entre les phases des moments sont proportionnelles aux angles de rotation des images. Comme prévu, les moments de Zernike de deux formes différentes (par exemple ovale et rectangle) sont complètement différents. Cela signifie que l'algorithme fonctionne bien.
