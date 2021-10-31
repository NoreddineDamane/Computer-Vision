# Image classification using ensemble algorithms and zernike moments 
## Zernike moments
Zernike moments are features extracted by mapping the input image onto a complex set of Zernike polynomials.
Computing Zernike moments from an input image involves three steps. 
1.	The computation of the radial polynomials
2.	The computation of the Zernike basis functions
3.	The computation of the Zernike moments by mapping the image onto the Zernike basis functions [[1]](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Feature%20Extraction%20Using%20Zernike%20Moments/images%2Bdoc/1-s2.0-S0031320306001166-main.pdf).

## Dataset
To illustrate the use of zernike moments in shape recognition, we will use the Four Shapes dataset. This dataset contains 14970 samples of four classes: circles, squares, stars, triangles and the rotated version of each.. 
[link to the data](https://www.kaggle.com/smeschke/four-shapes)

![](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/four%20shapes.PNG)

## Feature extraction
we computed the Zernike moments for the order and repetition (n, m) (n, m): ["(0, 0)", "(1, 1)", "(2, 0)", "(2, 2)", "(3, 1)", "(3, 3)", "(4, 0)", "(4, 2)", "(4, 4)", "(5, 1)", "(5, 3)", "(5, 5)", "(6, 0)", "(6, 2)", "(6, 4)", "(6, 6)" ,"(7, 1)", "(7, 3)", "(7, 5)", "(7, 7)"]

```python
m = []
n = []
N = np.arange(0 , 8)
M = np.arange(0 , 8)
for i in range (0,8):
    for j in range (0,8):
        if(((N[i] - abs(M[j])) % 2 == 0 ) and (abs(M[j]) <= N[i])): # n - |m| = pair et |m| <= n
            n.append(N[i])
            m.append(M[j])
}
zer_m = []
for c, idx in classes.items():
    class_folder = img_path + "{}/".format(c)
    for f in os.listdir(class_folder):
        fpath = class_folder + f
        sample = int(f.replace(".png", ""))
        img = cv.imread(fpath, cv.IMREAD_GRAYSCALE)
        img_ = np.logical_not(img)
        img_ = ~img_
        A_Z_m = []
        for i in range (0,20):
            [A, Phi] = Zernikmoment(img_,n[i],m[i])    # Call Zernikemoment fuction
            A_Z_m.append(round(A,4))
        A_Z_m = np.array(A_Z_m)
        A_Z_m = [idx] + A_Z_m.reshape((1, 20)).tolist()[0]
        zer_m.append(A_Z_m)
```

![](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/Feature.PNG)


## Classification using ensemble algorithms

```python
classifiers = {
	"Decision Tree" : DT(),
	"Bagging"       : BG(),
	"Random Forest" : RDF()
	}
for i in range(rounds):
	X_train, X_test, y_train, y_test = data_split(X, y, test_size=0.3)
	for name, classifier in classifiers.items():
		scaler = StandardScaler()
		scaler.fit(X_train)
		X_train = scaler.transform(X_train)
		X_test = scaler.transform(X_test)
		classifier.fit(X_train, y_train)
		score = classifier.score(X_test, y_test)
		result[name]["score"].append(score)
```
### Decision tree
The decision tree algorithm is known by its modern name CART "Classification and Regression Trees", and it is used for classification and regression problems. A decision tree is a simple structure where non-terminal nodes represent tests on one or more attributes and terminal nodes reflect the results of the decision. The ordinary tree consists of a root, branches, nodes (places where branches are split) and leaves. The first node is a root. The end of the chain "root - branch - node - ... - node" is called a "leaf".


<p align="center">
  <img src="https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/cap/1.png" width="350" title="decision treet">
</p> 


decision treet [2](https://www.packtpub.com/product/mastering-machine-learning-for-penetration-testing/9781788997409)

### Bagging
### Random forest
