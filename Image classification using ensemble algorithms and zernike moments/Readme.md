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


## Classification

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
</p>    decision treet [2](https://www.packtpub.com/product/mastering-machine-learning-for-penetration-testing/9781788997409)


The principal challenge in implementing the decision tree is to identify the attributes that we consider to be the root node at each level. This process is known as attribute selection. Information Gain is one method of attribute selection.

#### Information gain
The ID3 (Iterative Dichotomizer) decision tree algorithm uses entropy to calculate the information gain. We calculate the information gain to estimate the information that each attribute contains.  Using the information gain as a criterion, we try to estimate the information that each attribute contains. The information gain is the entropy reduction, it calculates the difference between the entropy before the division and the average entropy after the division of the data set based on the values of the attributes. The attribute with the highest information gain is chosen as the splitting attribute at the node level.

### Ensemble methods
Ensemble learning is a technique used to aggregate individual learning algorithms, known as baseline predictors, to produce a potentially superior predictor. Basically, ensemble learning can be classified into two groups based on their learning concept: parallel ensemble and sequential ensemble.
### Parallel methods
The parallel set trains the base predictors in parallel to utilize the independence features between them. The base predictors can be different learning algorithms (i.e., a heterogeneous set) or a single learning algorithm (i.e., a homogeneous set). Parallel methods primarily use decision trees, which are small decision trees in general. Among the most robust algorithms of parallel methods is Bagging.


#### Bagging
Bagging, or bootstrap aggregating, is a classical technique for creating an ensemble proposed by Breiman, however, it can be used in regression and classification problems. It is characterized by the creation of multiple samples, with readjustment using the bootstrap technique, i.e., randomly sampling on the training set to produce several training subsets, then training each training subset to give rise to an aggregated model. The final prediction result is obtained by averaging in the case of regression or voting in the case of classification.
Bagging has the advantage of allowing many weak learners to combine their efforts to outperform a single strong learner. It also reduces variance for algorithms that have high variance such as decision trees, eliminating model overfitting in the procedure.
When using the bagging technique, the trees constructed may have similar characteristics, implying a lack of diversity. One way to circumvent this problem is to use Random-Forest, which can be understood as modeling using bagging with a random selection of attributes to compose each decision tree. This method, combined with the selection of the best set of features explaining the data.
<p align="center">
  <img src="https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/cap/2.png" width="350" title="bagging">
</p> Graph illustrating how parallel ensemble learning works [2](https://www.packtpub.com/product/mastering-machine-learning-for-penetration-testing/9781788997409)


#### Random Forest

Random Forest proposed by Breiman is considered one of the most popular ensemble methods.
The RF model uses an ensemble of decision trees and two processes, bagging and random selection of attributes (variables) for each decision tree, to provide more accurate results and make the model more resistant to overfitting. This machine learning algorithm has become popular due to the simplicity of the learning and tuning parameters, the ability to fit nonlinear models, and the production of excellent classification results. It has been widely used in classification research, prediction, feature selection and outlier detection. In general, the main objective of this approach is to improve the performance of classification trees by reducing their variance.

### Sequential methods
Sequential ensemble, also known as boosting, trains the base predictors sequentially, with each newly added predictor attempting to correct its predecessor. The predictor focuses more on errors to improve prediction accuracy.
<p align="center">
  <img src="https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/cap/3.png" width="350" title="bagging">
</p> Flowchart of the sequential set where each model corrects the errors of its predecessor [2](https://www.packtpub.com/product/mastering-machine-learning-for-penetration-testing/9781788997409)

#### Boosting
Boosting is a technique used to solve classification and regression problems, which combines a set of models (decision trees), whose individual performances can be considered as poor, while when the individual predictions are aggregated, a high accuracy model is obtained. The focus of this approach is on bias reduction, i.e. improving the ability of the model to fit the data. Several machine learning models have been proposed with this idea in mind, using decision trees with individual learners. We highlight Adaptive Boost (AB) and gradient boosting (GB).

#### Adaptive Boost
The Adaptive Boost algorithm is one of the best known algorithms for creating an ensemble classifier. The algorithm generates a strong classifier from several weak classifiers, in which a new predictor attempts to correct its predecessor by adding more weight to the errors. One of the reasons why the Adaptive Boost algorithm performs well is the diversity among the weak classifiers.

#### Gradient boosting
Gradient boosting is the combination of Adaptive Boost and weighted minimization, in which the residual errors made by the previous predictor are passed on to the new predictor. The objective of Gradient boosting is to minimize the loss of a model by sequentially adding new baseline predictors using a gradient descent type procedure. The three main components of Gradient boosting are the loss function, the weak learner and the additive model.
