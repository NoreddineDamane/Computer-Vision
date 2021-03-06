# Feature Extraction Using Hu Moments

## Introduction
Hu a proposé les moments de Hu en 1962 [[1]](https://ieeexplore.ieee.org/abstract/document/1057692), qui sont principalement utilisés pour la reconnaissance des formes. En statistique mathématique, les moments sont utilisés pour décrire la distribution d'une variable aléatoire.

# Méthode
Les moments de Hu sont un ensemble de 7 nombres calculés à l'aide de moments centraux invariants aux transformations d'image. Les 6 premiers moments se sont avérés être invariants à la translation, à l’échelle, à la rotation et à la réflexion. Alors que le signe du 7ème moment change pour la réflexion de l'image. De plus, ils présentent l'avantage d'une faible complexité de calcul. Les moments de hu sont obtenus comme suit .

Moment brut d’ordre ![1](https://latex.codecogs.com/gif.latex?%5C%28p%20&plus;%20q%29%5C) est défini comme :


![2](https://latex.codecogs.com/gif.latex?m_%7Bp%20q%7D%20%3D%5Csum_%7Bx%7D%20%5Csum_%7By%7D%20x%5Ep%20y%5Eq%20I%28x%2Cy%29)


Où, ![3](https://latex.codecogs.com/gif.latex?I%20%28x%2C%20y%29) est la valeur de gris de l'image, ![](https://latex.codecogs.com/gif.latex?x) et ![](https://latex.codecogs.com/gif.latex?y) sont la coordonnée horizontale et la coordonnée verticale.


Et les moments centraux peuvent être décrits comme :


![4](https://latex.codecogs.com/gif.latex?%5Cmu_%7Bp%20q%7D%20%3D%20%5Csum_%7Bx%7D%20%5Csum_%7By%7D%20%28x-%5Cbar%20x%29%5Ep%20%28y-%5Cbar%20y%29%5Eq%20I%28x%2Cy%29)


Avec:![5](https://latex.codecogs.com/gif.latex?%5Cbar%20x%20%3D%20%5Cfrac%20%7Bm_%7B10%7D%7D%7Bm_%7B00%7D%7D%20%5Ctext%7B%20et%20%7D%20%5Cbar%20y%20%3D%20%5Cfrac%20%7Bm_%7B01%7D%7D%7Bm_%7B00%7D%7D)
Les moments centraux ci-dessus sont invariants par translation.

Afin de rendre les moments invariants à l'échelle nous avons besoin de moments centraux normalisés comme indiqué ci-dessous.

![6](https://latex.codecogs.com/gif.latex?%5Ceta%28t%29_%7Bpq%7D%20%3D%20%5Cfrac%20%7B%5Cmu_%7Bp%20q%7D%7D%7B%5Cmu_%7B00%7D%5E%5Cgamma%7D)
Où     ![7](https://latex.codecogs.com/gif.latex?%5Cgamma%20%3D%5Cfrac%20%7B%28p&plus;q%29%7D%7B2%7D&plus;1%20%5Ctext%7B%20et%20%7D%20p&plus;q%20%5Cgeq%20%7B2%7D)



À partir de la définition ci-dessus, Les 7 moments de hu sont calculés à l'aide des formules suivantes :



![](https://latex.codecogs.com/gif.latex?h_0%20%3D%20%5Ceta_%7B20%7D%20&plus;%20%5Ceta_%7B02%7D)



![](https://latex.codecogs.com/gif.latex?h_1%20%3D%20%28%5Ceta_%7B20%7D%20-%20%5Ceta_%7B02%7D%29%5E2%20&plus;%204%5Ceta_%7B11%7D%5E2)



![](https://latex.codecogs.com/gif.latex?h_3%20%3D%20%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20&plus;%20%28%5Ceta_%7B21%7D%20&plus;%5Ceta_%7B03%7D%20%29%5E2)



![](https://latex.codecogs.com/gif.latex?h_4%20%3D%20%28%5Ceta_%7B30%7D%20-%203%5Ceta_%7B12%7D%29%28%5Ceta_%7B30%7D%20&plus;%5Ceta_%7B12%7D%20%29%5B%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20-%203%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5E2%20%5D%20&plus;%20%283%5Ceta_%7B21%7D%20-%20%5Ceta_%7B03%7D%29%20%5B3%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20-%20%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5E2%20%5D)



![](https://latex.codecogs.com/gif.latex?h_5%20%3D%20%28%5Ceta_%7B20%7D%20-%203%5Ceta_%7B02%7D%29%20%5B%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20-%20%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5E2%20&plus;%204%5Ceta_%7B11%7D%28%5Ceta_%7B30%7D%20-%20%5Ceta_%7B12%7D%29%20%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5D)



![](https://latex.codecogs.com/gif.latex?h_6%20%3D%20%283%5Ceta_%7B21%7D%20-%20%5Ceta_%7B03%7D%29%20%28%5Ceta_%7B30%7D%20&plus;%5Ceta_%7B12%7D%29%20%5B%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20-%203%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5E2%20%5D%20&plus;%20%28%5Ceta_%7B30%7D%20-%203%5Ceta_%7B12%7D%29%20%28%5Ceta_%7B21%7D%20-%20%5Ceta_%7B03%7D%29%20%5B3%28%5Ceta_%7B30%7D%20&plus;%20%5Ceta_%7B12%7D%29%5E2%20-%20%28%5Ceta_%7B21%7D%20&plus;%20%5Ceta_%7B03%7D%29%5E2%20%5D)

# Résultats
Afin de tester le code, nous avons utilisé des images présentant des formes (ovale, rectangle, nuage) et des versions pivotées de ces formes[[2]](https://github.com/NoreddineDamane/Computer-Vision/tree/master/Feature%20Extraction%20Using%20Zernike%20Moments/images%2Bdoc/Test%20images)


La figure ci-dessous montre les résultats de l’application de l’algorithme sur ces images.

![](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Feature%20Extraction%20Using%20Hu%20Moments/output.png)


Les images de la première rangée ne sont que des versions pivotées de la forme ovale. hu6 (6éme invariant de hu) pour ces images est les mêmes et comme prévu, les moments hu de deux formes différentes sont différents.
