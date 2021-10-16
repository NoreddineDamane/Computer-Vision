# Feature Extraction Using Hu Moments
## Introduction
Hu a proposé les moments de Hu en 1962 \cite{hu1962visual}, qui sont principalement utilisés pour la reconnaissance des formes. En statistique mathématique, les moments sont utilisés pour décrire la distribution d'une variable aléatoire. Les moments de Hu sont un ensemble de 7 nombres calculés à l'aide de moments centraux invariants aux transformations d'image. Les 6 premiers moments se sont avérés être invariants à la translation, à l’échelle, à la rotation et à la réflexion. Alors que le signe du 7ème moment change pour la réflexion de l'image. De plus, ils présentent l'avantage d'une faible complexité de calcul. Les moments de hu sont obtenus comme suit .\\
\\


Moment brut d’ordre [1](https://latex.codecogs.com/gif.latex?%5C%28%28p%20&plus;%20q%29%5C%29) est défini comme :

\[m_{p q} =\sum_{x} \sum_{y} x^p y^q I(x,y)\]

Où, \(I (x, y)\) est la valeur de gris de l'image, \(x\) et \(y\) sont la coordonnée horizontale et la coordonnée verticale.

Et les moments centraux peuvent être décrits comme :

\[\mu_{p q} = \sum_{x} \sum_{y} (x-\bar x)^p (y-\bar y)^q I(x,y) \]

Avec:\[\bar x = \frac {m_{10}}{m_{00}} \text{et } \bar y = \frac {m_{01}}{m_{00}}\]
Les moments centraux ci-dessus sont invariants par translation.\\

Afin de rendre les moments invariants à l'échelle nous avons besoin de moments centraux normalisés comme indiqué ci-dessous.\\

\[\eta(t)_{pq} = \frac {\mu_{p q}}{\mu_{00}^\gamma} \]
 
Où \[\gamma =\frac {(p+q)}{2}+1 \text{ et  } p+q \geq {2}\]\\
À partir de la définition ci-dessus, Les 7 moments de hu sont calculés à l'aide des formules suivantes :

\[h_0 = \eta_{20} + \eta_{02}\]
\[h_1 = (\eta_{20} - \eta_{02})^2 + 4\eta_{11}^2 \]
\[h_2 = (\eta_{30} - 3\eta_{12})^2 + (3\eta_{21} -\eta_{03} )^2 \]
\[h_3 = (\eta_{30} + \eta_{12})^2 + (\eta_{21} +\eta_{03} )^2 \]
\[h_4 = (\eta_{30} - 3\eta_{12})(\eta_{30} +\eta_{12} )[(\eta_{30} + \eta_{12})^2 - 3(\eta_{21} + \eta_{03})^2 ] + (3\eta_{21} - \eta_{03}) [3(\eta_{30} + \eta_{12})^2 - (\eta_{21} + \eta_{03})^2 ] \]

\[h_5 = (\eta_{20} - 3\eta_{02}) [(\eta_{30} + \eta_{12})^2 - (\eta_{21} + \eta_{03})^2 + 4\eta_{11}(\eta_{30} - \eta_{12}) (\eta_{21} + \eta_{03}) ] \]

\[h_6 = (3\eta_{21} - \eta_{03}) (\eta_{30} +\eta_{12}) [(\eta_{30} + \eta_{12})^2 - 3(\eta_{21} + \eta_{03})^2 ] + (\eta_{30} - 3\eta_{12}) (\eta_{21} - \eta_{03}) [3(\eta_{30} + \eta_{12})^2 - (\eta_{21} + \eta_{03})^2 ] \]
