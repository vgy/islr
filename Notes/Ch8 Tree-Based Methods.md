# Chapter 8 Tree Based Methods

## 8.1 Tree-based methods

* Quiz 

	8.1.R1 
		Using the decision tree on page 5 of the notes, what would you predict for the log salary of a player who has played for 4 years and has 150 hits?:

		[x] 5.11
		[] 5.55		
		[] 6.0		
		[] 6.74
		
		Explanation: The player has played less than 4.5 years, so at the first split we follow the left branch. There are no further splits, so we predict 5.11.


## 8.2 More details on Trees

* Pruning a tree: To choose the best subtree.
	The tuning parameter alpha controls a trade-off btw subtree's complexity and its fit to the training data.
	Select an optimal value alpha_hat using cross validation, the return to the full dataset and obtain the subtree corresponding to alpha_hat.

* Quiz

		|T|
		sum  sum     (yi−yˆRm)2+α|T|
		m=1 i: xi∈Rm

	8.2.R1
		Imagine that you are doing cost complexity pruning as defined on page 18 of the notes. 
		You fit two trees to the same data: T1 is fit at α=1 and T2 is fit at α=2. Which of the following is true?

		[x] T1 will have at least as many nodes as T2
		[] T1 will have at most as many nodes as T2
		[] Not enough information is given in the problem to decide
	
		Explanation. A higher value of alpha corresponds to a higher penalty on the complexity of the tree. This means that T1 will have at least as many nodes as T2.


## 8.3 Classification trees

* Quiz:
	+ Gini:
				 K
			G = sum  pˆmk (1 − pˆmk)
				 k=1

		K classes. The Gini index takes on a small value if all of the pˆmk’s are close to zero or one.

	+ 8.3.R1
		You have a bag of marbles with 64 red marbles and 36 blue marbles.
		What is the value of the Gini Index for that bag? Give your answer to the nearest hundredth:

		Answer: 0.4608
		Explanation: Gini Index = .64*(1-.64) + .36*(1-.36) = .4608

	+ 8.3.R2
		What is the value of the Cross-Entropy? Give your answer to the nearest hundredth (using log base e, as in R):

		Answer: 0.65

		Explanation: Cross Entropy = -.64*ln(.64) - .36*ln(.36) = .6534

## 8.4 Bagging and Random Forests

* Bagging (or bootstrap aggregation): is a general purpose procedure for reducing the variance of a stat learning method; useful for decision trees use.

	+ Bootstrap: by taking repeated samples from the (single) training data set.

	+ We then train our method on the bth bootstrapped training set in order to get fˆ∗b(x), the prediction at a point x. We then average all the predictions to obtain:
		
						 B
		fˆbag (x) = 1/B sum fˆ *b (x)
						b=1
		
	+ This is called bagging.

		** Bagging involves creating multiple copies of the original training data set using the bootstrap, fitting a separate decision tree to each copy, and then combining all of the trees in order to create a single predictive model. Each tree is built on a bootstrap data set, independent of the other trees.


* Random Forests:

	+ Provide an improvement over bagged trees by way of a small tweak that decorrelates the trees. This reduces the variance when we average the trees.

	+ As in bagging, we build num of decision trees on bootstrapped training samples, so each time a split in a tree is considered, a random selection of m predictors is chosen as split candidates from the full set of p predictors. The split is allowed to use only one of those m predictors.

	+ A fresh selection of m predictors is taken at each split, and we choose m=sqrt(p) : num of predictors considered at each split is approx. equal to the sqrt of total. 


* Quiz

	Suppose we produce ten bootstrap samples from a data set containing red and green classes.
	We then apply a classification tree to each bootstrap sample and, for a specific value of X, produce 10 estimates of P(Class is Red|X):

		0.1,0.15,0.2,0.2,0.55,0.6,0.6,0.65,0.7, and 0.75
	
	There are two common ways to combine these results together into a single class prediction.
	One is the majority vote approach discussed in the notes. The second approach is to classify based on the average probability.

		+ 8.4.R1: What is the final classification under the majority vote method?:
		
			Answer: Red
			
			Explanation: 6 of the 10 probabilities are greater than 1/2, so the majority vote method will select red.

		+ 8.4.R2: What is the final classification under the average probability method?:
			
			Answer: Green
			
			Explanation: The average of the probabilities is 0.45, so the average probability method will select green.

## 8.5 Boosting

* Like bagging, boosting is a general approach that can be applied to many statistical learning methods for regression or classification

* Bagging involves creating multiple copies of the original training data set using the bootstrap, fitting a separate decision tree to each copy, and then combining all of the trees in order to create a single predictive model. Each tree is built on a bootstrap data set, independent of the other trees.

* Boosting works in a similar way, except that the trees are grown sequentially: each tree is grown using information from previously grown trees.

* Quiz

	+ 8.5.R1
		In order to perform Boosting, we need to select 3 parameters: number of samples B, tree depth d, and step size λ.

		How many parameters do we need to select in order to perform Random Forests?:

		Answer: 2  
		
		Explanation: To perform Random Forests we need to select 2 parameters: number of samples B and m = number of variables sampled at each split.

## 8.R Tree-based methods in R

	+ 8.R.R1
		You are trying to reproduce the results of the R labs, so you run the following command in R: > library(tree)
		As a response, you see the following error message: Error in library(tree) : there is no package called ‘tree’
		What went wrong?

			- N : You meant to use 'require(tree)'
			- N : You meant to use 'library("tree")'
			- Y : The tree package is not installed on your computer
			- N : Nothing is wrong, that error message could not be produced by R

			Explanation: In order to install the package, run install.packages() or use the package installer through the R menu bar.

## Quiz

+ 8.Q1
	The tree building algorithm given on pg 13 is described as a Greedy Algorithm. Which of the following is also an example of a Greedy Algorithm?:

		[] The Lasso
		[] Support Vector Machines	
		[] The Bootstrap	
		[x] Forward Stepwise Selection
		
		Explanation: 
			Forward Stepwise Selection is a Greedy Algorithm because at each step it selects the variable that improves the current model the most.
			There is no guarantee that the final result will be optimal.

+ 8.Q2
	Examine the plot on pg 23. Assume that we wanted to select a model using the one-standard-error rule on the Cross-Validated error. What tree size would end up being selected?:

		[]	1
		[x] 2	
		[] 3	
		[] 10
		
		Explanation: 
			Cross-Validated error is minimized at tree size 3. 
			The error for Tree size 2 is within one standard error of the minimum, but the error for tree size 1 is not. 
			Thus, the one-standard-error rule selects tree size 2.

+ 8.Q3
	Suppose I have two qualitative predictor variables, each with three levels, and a quantitative response. I am considering fitting either a tree or an additive model. For the additive model, I will use a piecewise-constant function for each variable, with a separate constant for each level. Which model is capable of fitting a richer class of functions:

		[x] Tree
		[] Additive Model	
		[] They are equivalent
		
		Explanation: 
			Although each split of the tree makes two partitions, it can fit interactions, while the additive model cannot.
			With enough splits the tree can fit a full 3x3 regression surface.

