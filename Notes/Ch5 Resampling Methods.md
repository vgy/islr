# Chapter 5 - Resampling methods

--
## Cross-Validation

+ We're going to sample from a data set in order to learn about the quantity of interest. 

+ The cross validation and the bootstrap are both ways of resampling from the data.

+ The main thing we use the cross validation for is to get an idea of the test set error of our model. We review the concept of training error which is too optimistic. The more we fit to the data, the lower the training error. But the test error can get higher if we overfit. So, we use cv to get the idea of the test set error of the model.

+ Bootstrap is the most useful to get an idea of the variability or standard deviation of an estimate and its bias.

+ Distinction btw test error and training error:

	+ The test error is the average error that results from using a statistical learning method to predict the response on a new observation, one that was not used in training the method.
	
	+ In contrast, the training error can be easily calculated by applying the statistical learning method to the observations used in its training.
	
	+ But the training error rate often is quite different from the test error rate, and in particular the former can dramatically underestimate the latter.

**Quiz**

	1/ When we fit a model to data, which is typically larger?
		[x] Test Error 
		[] Training Error
		
		Explanation: Training error almost always underestimates test error, sometimes dramatically

 	2/ What are reasons why test error could be LESS than training error?
		[x] By chance, the test set has easier cases than the training set.
		[] The model is highly complex, so training error systematically overestimates test error
		[] The model is not very complex, so training error systematically overestimates test error
		
		Explanation: 
			Training error usually underestimates test error when the model is very complex (compared to the training set size), 
				and is a pretty good estimate when the model is not very complex. 
			However, it's always possible we just get too few hard-to-predict points in the test set, or too many in the training set.


## K-fold Cross-Valdiation

	
	**Quiz**
	
	- 5.2.R1: Suppose we want to use cross-validation to estimate the error of the following procedure:
		Step 1: Find the k variables most correlated with y
		Step 2: Fit a linear regression using those variables as predictors
		We will estimate the error for each k from 1 to p, and then choose the best k.

		True or False: a correct cross-validation procedure will possibly choose a different set of k variables for every fold.
		Answer: [True]
			
		Explanation: 
			True: we need to replicate our entire procedure for each training/validation split.
			That means the decision about which k variables are the best must be made on the basis of the training set alone.
			In general, different training sets will disagree on which are the best k variables.

## 5.3 Cross-Validation: the wrong and right way

	**Quiz**
	- 5.3.R1
		Suppose that we perform forward stepwise regression and use cross-validation to choose the best model size.

		Using the full data set to choose the sequence of models is the WRONG way to do cross-validation (we need to redo the model selection step within each training fold). If we do cross-validation the WRONG way, which of the following is true?

			[x] The selected model will probably be too complex
			[] The selected model will probably be too simple

		Explanation
			Using the full data set to choose the best variables means that we do not pay as much price as we should for overfitting 
			(since we are fitting to the test and training set simultaneously). 
			This will lead us to underestimate test error for every model size, but the bias is worst for the most complex models. 
			Therefore, we are likely to choose a model that is more complex than the optimal model.

## Bootstrap

	**Quiz**
	- 5.4.R1
		One way of carrying out the bootstrap is to average equally over all possible bootstrap samples from the original data set (where two bootstrap data sets are different if they have the same data points but in different order). 
		Unlike the usual implementation of the bootstrap, this method has the advantage of not introducing extra noise due to resampling randomly.
		To carry out this implementation on a data set with n data points, how many bootstrap data sets would we need to average over?

		Answer: n^n

		Explanation
			Completely removing the bootstrap resampling noise is usually not worth incurring the extreme computational cost. 
			If B is large, but still less than n^n, random resampling gives a good Monte Carlo estimate of the idealized bootstrap estimate for all n^n data sets.

## More on the Bootstrap

	**Quiz**
	- 5.5.R1
		If we have n data points, what is the probability that a given data point does not appear in a bootstrap sample?

		Answer: (1-1/n)^n
		
		Explanation
			To construct a bootstrap sample, we repeatedly draw a single data point from a sample of size n, n times.
			Any given data point has a 1 -1/n chance of not being selected in each draw. Hence, the chance of not being selected in any of the n draws is (1 - 1/n)^n
		
## Resamplin in R

	**Quiz**
	- 5.R.R1
		Download the file 5.R.RData and load it into R using load("5.R.RData"). Consider the linear regression model of y on X1 and X2. What is the standard error for β1? 

		Answer: β1 = 0.02593
		Explanation: use summary(lm(y~., data=Xy))
			Output:
				Call:
				lm(formula = y ~ ., data = Xy)

				Residuals:
				     Min       1Q   Median       3Q 
				-1.44171 -0.25468 -0.01736  0.33081 
				     Max 
				 1.45860 

				Coefficients:
				            Estimate Std. Error t value
				(Intercept)  0.26583    0.01988  13.372
				X1           0.14533    0.02593   5.604
				X2           0.31337    0.02923  10.722
				            Pr(>|t|)    
				(Intercept)  < 2e-16 ***
				X1          2.71e-08 ***
				X2           < 2e-16 ***
				---
				Signif. codes:  
				  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’
				  0.1 ‘ ’ 1

				Residual standard error: 0.5451 on 997 degrees of freedom
				Multiple R-squared:  0.1171,	Adjusted R-squared:  0.1154 
				F-statistic: 66.14 on 2 and 997 DF,  p-value: < 2.2e-16


		5.R.R2
			Next, plot the data using matplot(Xy,type="l"). Which of the following do you think is most likely given what you see?


			[] Our estimate of s.e.(^β1) is too high.
			[x] Our estimate of s.e.(^β1) is too low. 
			[] Our estimate of s.e.(^β1) is about right.

			Explanation
				There is very strong autocorrelation between consecutive rows of the data matrix. 
				Roughly speaking, we have about 10-20 repeats of every data point, so the sample size is in effect much smaller than the number of rows (1000 in this case).
			
		5.R.R3
			Now, use the (standard) bootstrap to estimate s.e.(β^1). To within 10%, what do you get?

			Answer: 0.02844209
			
			Explanation
				When we do the i.i.d. bootstrap, we are relying on the original sampling having been i.i.d. That is the same assumption that screwed us up when we used lm.
				reference: https://github.com/kjy/StatisticalLearning_classstuff/blob/master/HW_TheBootstrap.R

		5.R.R4
			Finally, use the block bootstrap to estimate s.e.(^β1). Use blocks of 100 contiguous observations, and resample ten whole blocks with replacement then paste them together to construct each bootstrap time series. For example, one of your bootstrap resamples could be:

			new.rows = c(101:200, 401:500, 101:200, 901:1000, 301:400, 1:100, 1:100, 801:900, 201:300, 701:800)

			new.Xy = Xy[new.rows, ]

			To within 10%, what do you get?

			Answer: 0.2;
			
			Explanation: The block bootstrap does a better job of mimicking the original sampling procedure, because it preserves the autocorrelation.

## Quiz

	5.Q.1
		If we use ten-fold cross-validation as a means of model selection, the cross-validation estimate of test error is:

		[] biased upward
		[] biased downward
		[] unbiased
		[x] potentially any of the above

		Explanation
			There are competing biases: on one hand, the cross-validated estimate is based on models trained on smaller training sets than the full model, which means we will tend to overestimate test error for the full model.
			On the other hand, cross-validation gives a noisy estimate of test error for each candidate model, and we select the model with the best estimate. 
			This means we are more likely to choose a model whose estimate is smaller than its true test error rate, hence, we may underestimate test error. 
			In any given case, either source of bias may dominate the other.
			
	5.Q.2
		Why can't we use the standard bootstrap for some time series data?

		[x] The data points in most time series aren't i.i.d.
		[] Some points will be used twice in the same sample
		[x] The standard bootstrap doesn't accurately mimic the real-world data-generating mechanism
		
		Explanation
			The bootstrap always involves using some points more than once in each resample, but that doesn't inherently make it incorrect(unless we are trying to gauge prediction error). 
			The real problem in this case is that the usual bootstrap algorithm samples i.i.d., so there is no serial autocorrelation (unlike what is observed in most time series). 
			This makes the set of resampled time series very very different from the sorts of time series we actually get in the real world.
