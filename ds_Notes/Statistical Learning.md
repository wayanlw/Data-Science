# Statistical Learning

## 1 Introduction

- Statistical learning refers to a vast set of tools for understanding data.
- These tools can be classified as
	- supervised
		- supervised statistical learning involves building a statistical model for predicting, or estimating, an output based on one or more inputs. Problems of this nature occur in felds as diverse as business, medicine, astrophysics, and public policy.
		- Types
			- Regression
			- Classification
		- Involves training
	- unsupervised.
		- unsupervised statistical learning, there are inputs but no supervising output; nevertheless we can learn relationships and structure from such data
- The input variables are typically denoted using the output variable symbol X, with a subscript to distinguish them
- The inputs go by diferent names, such as predictors, independent variables, features, predictor independent variable feature or sometimes just variables.
- The output variable—in this case, sales—is variable often called the response or dependent variable, and is typically denoted using the symbol Y .  

## 2 Statistical Learning

### 2.1 Statistical Learning

#### 2.1.1 Why Estimate F

- There are two main reasons that we may wish to estimate f: prediction and inference.
	- **Prediction**: objective is just predict Y using X, not to understand the relationship them
		- Eg. Identify individuals who will respond positively for a marketing campaign. Here it is not important to understand the function but to understand the set of people who will respond positively.
		- accuracy of prediction for Y depends on two quantities
			- reducible error
				- This error is reducible by improving the accuracy of ˆf by using the most appropriate statistical learning technique to estimate f.
			- irreducible error.
				- Y is also a function of e.
				- irreducible error will always provide an upper bound on the accuracy of prediction for Y . This bound is almost always unknown in practice, which, by defnition cannot be predicted using X
	- **Inference**: objective is to understand the relationship between Y and variables X.  
			- Eg. relationship between advertising spend and sales. Need to understand Which media are associated with sales? – Which media generate the biggest boost in sales? or – How large of an increase in sales is associated with a given increase in TV advertising?  
			- Eg. Elasticity of demand  
			- Questions to answer  
				- ==Which predictors== are associated with the response?  
				- What is the ==relationship== between the response and each predictor?  
				- Can the relationship between Y and each predictor be adequately summarized using a ==linear equation, or is it complicated==
	- Inference + Prediction
		- In certain examples you will need both
		- For example, in a real estate setting,
			- one may seek to relate values of homes to inputs such as crime rate, zoning, distance from a river, air quality, schools, income level of community, size of houses, and so forth.
			- In this case one might be interested in the association between each individual input variable and housing price—for instance, how much extra will a house be worth if it has a view of the river? This is an inference problem.
			- Alternatively, one may simply be interested in predicting the value of a home given its characteristics: is this house underor over-valued? This is a prediction problem

#### 2.1.2 How to Estimate F

- Parametric
	- Parametric methods involve a two-step model-based approach.
		1. First, we make an assumption about the functional form, or shape,of f. For example, one very simple assumption is that f is linear in
		2. After a model has been selected, we need a procedure that uses the training data to fit or train the model
	- Pro: simplifies the problem of estimating f because it is generally much easier to estimate a set of parameters, such as β 0 , β 1 , … , β p in the linear model (2.4), than it is to fitan entirely arbitrary function
	- Con: Might not be the true function. Trying to solve for thes may lead to [[overfitting]]
	- Less flexible. More interpretable. >> Suitable for infernece, when there is a need to understnad the function
- Non-parametric methods
	- do not make explicit assumptions about the func-tional form of f . Instead they seek an estimate of f that gets as close to the data points as possible without being too rough or wiggly.
	- Less intepretable. More flexible. Suitablef for prediction, when the prediction is more important than the understanding

#### 2.1.3 Tradeoff Between Prediction Accuracy and Model Interpretability

![](_attachments/image/Statistical%20Learning-1709363977567.jpeg)

- Prediction problems --> Flexibility is more important. Non-Parametric models are suitable.
- Inference problems --> Interpretation/understanding of the model is more important. Parametric models are suitable.

#### 2.1.4 Supervised Vs Un-supervised Learning

- Supervised
	- Fore each observation of predictor there is a response
	- Models used : Regresson, GAM, Boosting
- Un supervised
	- There are only observation. There is no y, predicted variable
	- Models used: [[Clustering]]
	- Eg. market segmentation
- Semi Supervised
	- ???

#### 2.1.5 Regression Vs Classification

- Variable
	- Quantitivative/numerical
	- qualitative/categorical

### 2.2 Assessing Model Accuracy

Different methods may provide different accuracy levels. Hence in selection of the model measurement of accuracy is important to understand the quality of fit of different models

#### 2.2.1 Training MSE Vs Test MSE and Overfitting

- Mean square Error
	- $\mathrm{MSE}=\frac{1}{n}\sum_{i=1}^{n}(y_{i}-\hat{f}(x_{i}))^{2}$
	- Use train data - Training MSE
	- Use Test data thereafter - Test MSE
	- What we are more intersted in is Test MSE
	- Sometimes training MSE can be very low but the test MSE is very high. This is overfitting test data
	- ![](_attachments/image/Statistical%20Learning-1709365952297.jpeg)
- As model flexibility increases, the training MSE will decrease, but the test MSE may not. When a given method yields a small training MSE but a large test MSE, we are said to be overfitting the data. This is a fundamental property of statistical learning that holds regardless of the particular data set at hand and regardless of the statistical method being used. ![](_attachments/image/Statistical%20Learning-1709366203100.jpeg)![](_attachments/image/Statistical%20Learning-1709366850462.jpeg)

#### 2.2.2 Variance Vs Bias Tradeoff - Regression Settings

it is possible to show that the expected test MSE, for a given value x 0 , can always be decomposed into the sum of three fundamental quantities: the variance of ˆ f(x 0 ) , the squared bias of ˆf(x 0 ) and the variance of the errorterms " .$E\left(y_0-\hat{f}(x_0)\right)^2=\mathrm{Var}(\hat{f}(x_0))+[\mathrm{Bias}(\hat{f}(x_0))]^2+\mathrm{Var}(\epsilon).$

Here the notation $E\left(y_0-\hat{f}(x_0)\right)^2$ defines the expected test MSE at x0 and refers to the average test MSE that we would obtain if we repeatedly estimated f using a large number of training sets, and tested each at x 0 . The overall expected test MSE can be computed by averaging $E\left(y_0-\hat{f}(x_0)\right)^2$ over all possible values of x 0 in the test set.

- ==**Variance**== refers to the amount by which ˆf would change if we estimated it using a different training data set. Ideally the variance should not be too much. In general more *flexible* methods have higher variance due to the higher fit. This is the error that is introduced by fitting. As we increase flexibility initially the variance will slowly increase and after a certain degree of freedom, it drastically increases
- ==**bias**== is the error introduced by approximating a real life problem. Eg. when using linear regression we assume that there is a linear relationship between the variables. However actually there could be not. As you increase the flexibility, initially the bias will reduce drastically and stabilize.
- In Figure 2.11, the true f is substantially non-linear, so no matter how many training observations we are given, it will not be possible to produce an accurate estimate using linear regression. In other words, linear regression results in high bias in this example. However, in Figure 2.10 the true f is very close to linear, and so given enough data, it should be possible for linear regression to produce an accurate estimate. Generally, more flexible methods result in less bias.![](_attachments/image/Statistical%20Learning-1709366860306.jpeg)
- As a general rule, as we use more flexible methods, the variance will increase and the bias will decrease. The relative rate of change of these two quantities determines whether the test MSE increases or decreases.
- As we increase the flexibility of a class of methods, the bias tends to initially decrease faster than the variance increases. Consequently, the expected test MSE declines. However, at some point increasing flexibility has little impact on the bias but starts to significantly increase the variance. When this happens the test MSE increases.
- In a real-life situation in which f is unobserved, it is generally not possible to explicitly compute the test MSE, bias, or variance for a statistical learning method.

#### 2.2.2 Variance Vs Bias Tradeoff - Classification Settings

- Most common method is error rate
- Training error rate is $\begin{aligned}\frac{1}{n}\sum_{i=1}^nI(y_i\neq\hat{y}_i).\end{aligned}$ "I" is and indicator variable that equals 1 if $y_i\neq\hat{y}_i$. If this is 0, then the observation is classified correct
- testing error rate $\operatorname{Ave}\left(I(y_0\neq\hat{y}_0)\right)$ where y 0 is the predicted class label that results from applying the classifier to the test observation with predictor x 0 .
- Good classifer is one with the smallest *test error*

Bayes decission boundary - Gold standard. produces the lowest possible test error rate, called the Bayes error rate. Shows the line where the condition probability is 50%. However, cannot do for real data. The Bayes error rate is analogous to the irreducible error, discussed earlier. So it is used as a comparator

##### KNN (K nearest Neighbours)

![](_attachments/image/Statistical%20Learning-1709368721080.jpeg)
