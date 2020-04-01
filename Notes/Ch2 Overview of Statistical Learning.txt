# Chap2: Overview of statistical learning

### Notes:

**2.1 Introduction to Regression Models**
	+ Quiz:
		2.1 R1: In the expression Sales ≈ f(TV, Radio, Newspaper), "Sales" is the:
			- Y : Response
			- N : Training Data
			- N : Independent Variable
			- N : Feature
		Explanation
			The variable which you are trying to model is called the response or outcome. 
			The other variables are called features, predictors, or independent variables. 
			Together, the collection of features and response values that you will use for fitting form your training data.

**2.2 Dimensionality and structured models**

	+ In the curse of dimensionality, it's hard to find near neighborhoods in high dimensions and stay local.
	+ A linear model f(x) = b0 + b1.x gives a reasonable fit, and a quadratic model fq(x) = b0 + b1.x + b2.x^2 fits slightly better (polynomial).

	+ Trade-offs:
		
		+ Prediction accuracy vs interpretability: linear models are easy to intepret; thin-plate splines (TPS) are not.
		
		+ Good fit vs over-fit or under-fit: how do we know when the fit is just right?

		+ Parsimony vs black-box: prefer a simpler model to a black-box.

		The interpretability vs flexibility.
		Subset selection (lasso) >> least squares >> generalized additive model (Trees) >> bagging,boost >> SVM.

		+ Quiz 3: 
			
			- 2.2 R1: A hypercube with side length 1 in d dimensions is defined to be the set of points (x1, x2, ..., xd) such that 0 <= xj <= 1 for all j = 1, 2, ..., d. 
			The boundary of the hypercube is defined to be the set of all points such that there exists a j for which 0 <= x(j) <= 0.05 or 0.95 <= x(j) <= 1 
				(namely, the boundary is the set of all points that have at least one dimension in the most extreme 10% of possible values). 
			What proportion of the points in a hypercube of dimension 50 are in the boundary? 
				(hint: you may want to calculate the volume of the non-boundary region)
			
			Please give your answer as a value between 0 and 1 with 3 significant digits. If you think the answer is 50.52%, you should say 0.505:

			Answer: 0.995
 
			Explanation
				We know that the volume of the whole hypercube is 150 = 1. The volume of the interior of the hypercube is 0.950 = 0.005. 
				Thus, the volume of the boundary is 1-0.005 = 0.995.

**2.3 Model Selection and Bias-Variance Tradeoff**

	+ Assessing model accuracy.
		
		MSE = Avg(y - f(x))^2


	+ bias variance tradeoff

		E(y0 - f(x0))^2 = Var(f(x0)) + [bias(f(x0))]^2 + Var(e)

		* E averages over the Var of y0 awa Var in Training. [bias(f(x0))] = E[\f(x0)] - f(x0)

		* Flexibility of /f increases, its variance increases (~ its bias decreases). 
		
		* Choosing the flexibility based on avg test error amounts to a bias-variance trade-off.

	+ Quiz:

		* False: A fitted model with more predictors will necessarily have a lower Training Set Error than a model with fewer predictors. 
			
			Explanation
				False. While we typically expect a model with more predictors to have lower Training Set Error, it is not necessarily the case. 
				An extreme counterexample would be a case where you have a model with one predictor 
					that is always equal to the response, compared to a model with many predictors that are random.
		
		* While doing a homework assignment, you fit a Linear Model to your data set. You are thinking about changing the Linear Model to a Quadratic one. Which of the following is most likely true:

			- N : Using the Quadratic Model will decrease your Irreducible Error.
			- Y : Using the Quadratic Model will decrease the Bias of your model.
			- N : Using the Quadratic Model will decrease the Variance of your model
			- N : Using the Quadratic Model will decrease your Reducible Error
			
			Explanation:
				Introducing the quadratic term will make your model more complicated. 
				More complicated models typically have lower bias at the cost of higher variance. 
				This has an unclear effect on Reducible Error (could go up or down) and no effect on Irreducible Error.

**2.4 Classification problems**

	+ The response variable Y is "qualitative" - e.g. email is one C = {spam, ham} where ham is a good email. Digit C is from {1-9}. The goal is to build a classifier C(x) that assigns a class label from C to a future unlabeled observation x. Assess the uncertainty in each classification. Understand the roles of the different predictors among x={x1, x2, .., xp}

	+ Quiz:
		- 2.4.R1: Look at the graph given on page 30 of the Chapter 2 lecture slides. 
			Which of the following is most likely true of what would happen to the Test Error curve as we move 1/K further above 1?

			- N : The Test Errors will increase
			- N : The Test Errors will decrease
			- N : Not enough information is given to decide
			- Y : It does not make sense to have 1/K > 1
			
			Explanation: Since K is the number of neighbors, the value of K must be a Natural Number. This means that 1/K <= 1.
	
**Quizzes**
	
	+ 2.Q.1: For each of the following parts, indicate whether we would generally expect the performance of a flexible statistical learning method to be better or worse than an inflexible model.

		- The sample size n is extremely large, and the number of predictors p is small:

			correct: Flexibility is better 
			
			Explanation: A flexible model will allow us to take full advantage of our large sample size.

	+ 2.Q.2: The number of predictors p is extremely large, and the sample size n is small:

		correct: Flexibility is worse   
		
		Explanation: The flexible model will cause overfitting due to our small sample size.
	
	+ 2.Q.3: The relationship between the predictors and response is highly non-linear:

		correct: Flexibility is better  
		
		Explanation: A flexible model will be necessary to find the nonlinear effect.

	+ 2.Q.4: The variance of the error terms, i.e. σ2=Var(ϵ), is extremely high:

		correct: Flexibility is worse
		
		Explanation: A flexible model will cause us to fit too much of the noise in the problem.






















