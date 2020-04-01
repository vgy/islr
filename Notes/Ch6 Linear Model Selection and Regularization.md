# Chapter 6 Linear Model Selection and regulization

## 6.1 Introduction and Best-Subset Selection 

+ Quiz
	
	+ Which of the following modeling techniques performs Feature Selection?

		[] Linear Discriminant Analysis
		[] Least Squares		
		[x] Linear Regression with Forward Selection		
		[] Support Vector Machines
		
		Explanation: Forward Selection chooses a subset of the predictor variables for the final model. The other three methods end up using all of the predictor variables.
 
## 6.2 Stepwise selection

+ Quiz

	+ 6.2.R1
		We perform best subset and forward stepwise selection on a single dataset. For both approaches, we obtain p+1 models, containing 0,1,2,…,p predictors.
		Which of the two models with k predictors is guaranteed to have training RSS no larger than the other model?

		[x] Best Subset		
		[] Forward Stepwise		
		[] They always have the same training RSS		
		[] Not enough information is given to know

	+ 6.2.R2
		Which of the two models with k predictors has the smallest test RSS?

		[] Best Subset
		[] Forward Stepwise		
		[] They always have the same test RSS		
		[x] Not enough information is given to know correct
		
		Explanation
			We know that Best Subset selection will always have the lowest training RSS (that is how it is defined).
			That said, we don't know which model will perform better on a test set.

## 6.3 Backward stepwise selection

+ Quiz
	
	+ 6.3.R1
		You are trying to fit a model and are given p=30 predictor variables to choose from. 
		Ultimately, you want your model to be interpretable, so you decide to use Best Subset Selection.
		How many different models will you end up considering?:
		
		Answer: 2^p = 2^30

		Explanation
			Each predictor can either be included or not included in the model. 
			That means that for each of the 30 variables there are two options. 
			Thus, there are 2^30 potential models.
			Note: 
				Don’t ever try to fit that many models!
				It is too many and that is why Best Subset Selection is rarely used in practice for say p=10 or larger.

	+ 6.3.R2
		How many would you fit using Forward Selection?:

		Answer: 466
		
		Explanation
			For Forward Selection, you fit (p-k) models for each k=0,...p-1. The expression for the total number of models fit is on pg 15 of the notes: 1 + p(p+1)/2.


## 6.4 Estimating test error

+ Quiz

	+ 6.4.R1
		You are fitting a linear model to data assumed to have Gaussian errors. The model has up to p=5 predictors and n=100 observations. 
		Which of the following is most likely true of the relationship between Cp and AIC in terms of using the statistic to select a number of predictors to include?

		[] Cp will select a model with more predictors AIC
		[] Cp will select a model with fewer predictors AIC		
		[x] Cp will select the same model as AIC		
		[] Not enough information is given to decide
		
		Explanation: For linear models with Gaussian errors, Cp and AIC are equivalent.
		

## 6.5 Validation and cross validation

+ Quiz
	
	+ 6.5.R1
		You are doing a simulation in order to compare the effect of using Cross-Validation or a Validation set. For each iteration of the simulation, you generate new data and then use both Cross-Validation and a Validation set in order to determine the optimal number of predictors. Which of the following is most likely?

		[] The Cross-Validation method will result in a higher variance of optimal number of predictors		
		[x] The Validation set method will result in a higher variance of optimal number of predictors
		[] Both methods will produce results with the same variance of optimal number of predictors
		[] Not enough information is given to decide
		
		Explanation
			Cross-Validation is similar to doing a Validation set multiple times and then averaging the answers. 
			As such, we expect it to have lower variance than the Validation set method. This is why Cross-Validation is appealing (especially for small n).

## 6.6 Shrinkage methods and ridge regression

+ Quiz

	+ 6.6.R1
		√ (j=1Σp (βj)^2) is equivalent to:

		[] X ^β
		[] (^β)^R		
		[] Cp statistic		
		[x] ‖β‖2 correct

		Explanation: The expression is the L2 norm of β.
		
	+ 6.6.R2
		You perform ridge regression on a problem where your third predictor, x3, is measured in dollars. You decide to refit the model after changing x3 to be measured in cents. Which of the following is true?:

		[] ^β3 and ^y will remain the same.		
		[] ^β3 will change but ^y will remain the same.		
		[] ^β3 will remain the same but ^y will change.		
		[x] ^β3 and ^y will both change. correct

		Explanation: The units of the predictors affects the L2 penalty in ridge regression, and hence ^β3 and ^y will both change

## 6.7 The Lasso

+ performs variable selection.

+ Quiz
	
	+ 6.7 R1
		Which of the following is NOT a benefit of the sparsity imposed by the Lasso?

		[] Sparse models are generally more easy to interperet		
		[] The Lasso does variable selection by default		
		[x] Using the Lasso penalty helps to decrease the bias of the fits		
		[] Using the Lasso penalty helps to decrease the variance of the fits
		
		Explanation: 
			Restricting ourselves to simpler models by including a Lasso penalty will generally decrease the variance of the fits at the cost of higher bias.

## 6.8 Tuning parameter selection

+ Quiz

	+ 6.8.R1
		Which of the following would be the worst metric to use to select λ in the Lasso?

		[] Cross-Validated error		
		[] Validation set error		
		[x] RSS
		
		Explanation: 
			RSS would be the worst metric to use because it will cause us to always select the most complicated model.
			Any of the other metrics could be used, although Cross-Validated error is probably most common.

## 6.9 Dimension reduction methods

+ Quiz

	+ 6.9.R1
		We compute the principal components of our p predictor variables.
		The RSS in a simple linear regression of Y onto the largest principal component will always be no larger than the RSS in a simple regression of Y onto the second largest principal component. 
		True or False? (You may want to watch 6.10 as well before answering - sorry!)

		[] True
		[x] False

		Explanation: Principal components are found independently of Y, so we can't know the relationship with Y a priori.


## 6.10 Principal Components Regression and Partial Least Squares

+ Quiz

	+ 6.10.R1
		You are working on a regression problem with many variables, 
			so you decide to do Principal Components Analysis first and then fit the regression to the first 2 principal components. 
		Which of the following would you expect to happen?:

		[] A subset of the features will be selected
		[] Model Bias will decrease relative to the full least squares model	
		[x] Variance of fitted values will decrease relative to the full least squares model	
		[] Model interpretability will improve relative to the full least squares model
	
		Explanation
			While some forms of dimensional reduction will cause the first or fourth to occur, that is not the case with PCA.
			When using dimensional reduction we restrict ourselves to simpler models. Thus, we expect bias to increase and variance to decrease.

	 
## 6.R Model Selection in R

	+ 6.R.R1
		One of the functions in the glmnet package is cv.glmnet().
		This function, like many functions in R, will return a list object that contains various outputs of interest.
		What is the name of the component that contains a vector of the mean cross-validated errors?

	Answer:cvm
	
	Explanation: To check the return value of a function, use ?functionname and then scroll down to the Value heading.


## Quiz

	+ 6.Q.1
		Suppose we estimate the regression coefficients in a linear regression model by minimizing
			i=1∑n (yi − β0 − j=1∑p β(j) x(ij))^2 + λ j=1∑p (βj)^2
		for a particular value of λ. For each of the following, select the correct answer:
		As we increase λ from 0, the training RSS will:
		Answer: Steadily increase

		Explanation: Increasing λ will force us to fit simpler models. This means that training RSS will steadily increase because we are less able to fit the training data exactly.


	+ 6.Q.2 
		As we increase λ from 0, the test RSS will:

		Answer: Decrease initially, and then eventually start increasing in a U shape

		Explanation: 
			At first, we expect test RSS to improve because we are not overfitting our training data anymore.
			Eventually, we will start fitting models that are too simple to capture the true effects and test RSS will go up.

	+ 6.Q.3
		As we increase λ from 0, the variance will:

		Answer: Steadily decrease

		Explanation: Increasing λ will cause us to fit simpler models, which reduces the variance of the fits.

	+ 6.Q.4
		As we increase λ from 0, the (squared) bias will:

		Answer: Steadily increase

		Explanation: Increasing λ will cause us to fit simpler models, which have larger squared bias.

	+ 6.Q.5
		As we increase λ from 0, the irreducible error will:

		Answer: Remain constant

		Explanation: 
			Increasing λ will have no effect on irreducible error.
			By definition, irreducible error is an aspect of the problem and has nothing to do with a particular model being fit.



