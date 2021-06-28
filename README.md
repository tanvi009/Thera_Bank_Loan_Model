**Thera Bank - Loan Purchase Modeling**

This case is about a bank (Thera Bank) which has a growing customer base. Majority of these customers are liability customers (depositors) with varying size of deposits. The number of customers who are also borrowers (asset customers) is quite small, and the bank is interested in expanding this base rapidly to bring in more loan business and in the process, earn more through the interest on loans. In particular, the management wants to explore ways of converting its liability customers to personal loan customers (while retaining them as depositors). A campaign that the bank ran last year for liability customers showed a healthy conversion rate of over 9% success. This has encouraged the retail marketing department to devise campaigns with better target marketing to increase the success ratio with a minimal budget. The department wants to build a model that will help them identify the potential customers who have a higher probability of purchasing the loan. This will increase the success ratio while at the same time reduce the cost of the campaign. The dataset has data on 5000 customers. The data include customer demographic information (age, income, etc.), the customer's relationship with the bank (mortgage, securities account, etc.), and the customer response to the last personal loan campaign (Personal Loan). Among these 5000 customers, only 480 (= 9.6%) accepted the personal loan that was offered to them in the earlier campaign.

Job is to build the best model which can classify the right customers who have a higher probability of purchasing the loan. 

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Few concepts which might help you with Problem:

**What is Data Mining?**
Data mining, also known as knowledge discovery in data (KDD), is a process of extracting information to identify patterns, trends, and useful data that would allow the business to take the data-driven decision from huge sets of data. Given the evolution of data warehousing technology and the growth of big data, adoption of data mining techniques has rapidly accelerated over the last couple of decades, assisting companies by transforming their raw data into useful knowledge. Data mining has improved organizational decision-making through insightful data analyses.

Decision Trees are commonly used in data mining with the objective of creating a model that predicts the value of a target (or dependent variable) based on the values of several input (or independent variables).  Let's discuss about CART decision tree methodology. 
 
 **CART:** CART (Classification and Regression Trees) can be used for both classification and regression problems. The difference lies in the target variable:
1. With classification, we attempt to predict a class label. In other words, classification is used for problems where the output (target variable) takes a finite set of values, e.g., whether it will rain tomorrow or not.
2. Meanwhile, regression is used to predict a numerical label. This means your output can take an infinite set of values, e.g., a house price.

The pseudocode for constructing a CART decision tree is:
1. Chose a feature that has the optimal index. The index is calculated using the cost function.
2. Split the dataset based on the chosen feature
3. Repeats the process until it reaches to the leaves (Or meet the stopping criteria)

Creating a CART model involves selecting input variables and split points on those variables until a suitable tree is constructed. To build the CART decision trees in an efficient way we use the concept of Entropy and Gini Impurity.

**1. Gini Impurity:** 
Gini impurity is the lost function being used in the CART method which measures how much noise a category has. In other words, it is a measure of how often a randomly chosen element from the set would be incorrectly labelled if it was randomly labelled according to distribution of labels in the subset. For example, the weather feature can have categories: rain, sunny, or snowy; a numerical feature such as grade can be divide into 2 blocks: <70 or ≥70. Gini impurity can be calculated by the following formula:

![image](https://user-images.githubusercontent.com/63853707/123602135-13eb4d00-d816-11eb-850a-fef052beacd5.png)

**2. Gini Index:**
Gini Index combines the category noises together to get the feature noise. Gini Index is the weighted sum of Gini Impurity based on the corresponding fraction of the category in the feature. The formula is:

![image](https://user-images.githubusercontent.com/63853707/123602637-96740c80-d816-11eb-89dc-5531c43f62ad.png)

**3. Entropy:**
Entropy can be defined as a measure of the purity of the sub split. Entropy always lies between 0 to 1. Entropy is a measure of the randomness of a system. In physics, entropy represents the unpredictability of a random variable. The chance of having Head or Tail from a fair coin is 50/50, and so its entropy value is 1, which is the highest value for randomness. On the other hand, having a value 0 indicates the corresponding event is destined.The entropy of any split can be calculated by this formula:

![image](https://user-images.githubusercontent.com/63853707/123602893-e2bf4c80-d816-11eb-976e-baf5df977361.png)

**4. Information Gain:**
The information gain is the amount by which the Entropy of the system reduces due to the split that we have done. The more information we gain, the better. The formula is:

![image](https://user-images.githubusercontent.com/63853707/123603058-169a7200-d817-11eb-9507-c70b42d48f37.png)

Decision Trees are very useful and don't require standardising or normalising the data since it works on rules. Decision trees being so powerful also have a tendency to overfit. We keep on dividing the dataset till we get perfect split. This might capture last point of noise. To avoid overfitting we can prune our tree. 

The fastest and simplest pruning method is to work through each leaf node in the tree and evaluate the effect of removing it using a hold-out test set. Leaf nodes are removed only if it results in a drop in the overall cost function on the entire test set. You stop removing nodes when no further improvements can be made. In Pruning we use complexity parameter, which says everytime you add a branch, the error should decrease more than a specifically given threshold, usually called alpha. If decrease in error is not less than alpha than branch is not worth making.

Problem with Decision trees are that if we change data little bit, whole tree will give different output. Decision Trees are very sensitive to small changes in the data. Also, we discussed that they might overfit. So, instead of using one decision tree what if we use bunch of decision trees for our prediction. This concept is called Random Forest. Random forests are more stable and reliable than just a decision tree.

**Random forests** (RF) are basically a bag containing n Decision Trees (DT) having a different set of hyper-parameters and trained on different subsets of data. Let’s consider that I have somehow trained 100 trees with their respective subset of data. Now I will ask all the hundred trees in my bag that what is their prediction on my test data. Now we need to take only one decision on one example or one test data, we do it by taking a simple vote. We go with what the majority of the trees have predicted for that example.

![image](https://user-images.githubusercontent.com/63853707/123617770-39cc1e00-d825-11eb-86a7-1f97a05b7a7d.png)

While building subsets of data for trees, the word “random” comes into the picture. A subset of data is made by randomly selecting x number of features (columns) and y number of examples (rows) from the original dataset of n features and m examples. This is called Bootstrap Aggregation or Bagging which is used while creating our Decision Trees. This is done because if we use same dataset then results will be same, which will defeat our purpose of Random Forest. Sampling in Bagging is done by replacements, i.e. observations might repeat. While growing a decision tree during the bagging process, random forests perform split-variable randomization where each time a split is to be performed, the search for the split variable is limited to a random subset of mtry of the original p features. This forces even more variation amongst the trees in the model and ultimately results in lower correlation across trees and more diversification.

But what should be ideal value for mtry?

When mtry=p - the algorithm is equivalent to bagging decision trees. In this case correlation might be high
When mtry is very small than p- At various level of split the chance of actually catching one of the important variables become small. The trees have weal ability to predict.

Typical default values are mtry=p/3  (regression) and mtry=√p (classification) but this should be considered a tuning parameter. 

What do we need in order for our random forest to make accurate class predictions?

1. We need features that have at least some predictive power. After all, if we put garbage in then we will get garbage out.
2. The trees of the forest and more importantly their predictions need to be uncorrelated (or at least have low correlations with each other). While the algorithm itself via feature randomness tries to engineer these low correlations for us, the features we select and the hyper-parameters we choose will impact the ultimate correlations as well.



**Model Evaluation:**

Building accurate models will be futile if we don't have any measure to evaluate it. Hence Model Evaluation metrics are extremely important. Evaluating model performance with the data used for training is not acceptable in data science because it can easily generate overoptimistic and overfitted models. To avoid overfitting, methods use a test set (not seen by the model) to evaluate model performance. Few Model Evaluation metrics are:

**1. Confusion Matrix:**

A Confusion matrix is an N x N matrix used for evaluating the performance of a classification model, where N is the number of target classes. The matrix compares the actual target values with those predicted by the machine learning model.

![image](https://user-images.githubusercontent.com/63853707/123622564-fde78780-d829-11eb-97bb-ef50f64dcb93.png)

Few definitions you must be aware of:

1. Accuracy : the proportion of the total number of predictions that were correct.
2. Positive Predictive Value or Precision : the proportion of positive cases that were correctly identified.
3. Negative Predictive Value : the proportion of negative cases that were correctly identified.
4. Sensitivity or Recall : the proportion of actual positive cases which are correctly identified.
5. Specificity : the proportion of actual negative cases which are correctly identified.

**2. Gain and Lift Chart:**

Lift is a measure of the effectiveness of a predictive model calculated as the ratio between the results obtained with and without the predictive model.

![image](https://user-images.githubusercontent.com/63853707/123632285-6425d780-d835-11eb-8bbe-1cf8f4898746.png)

Gain chart tells us which segment to target for our business problem.

![image](https://user-images.githubusercontent.com/63853707/123632269-5e2ff680-d835-11eb-8e0c-4749892724bc.png)

Gain and Lift chart are mainly concerned to check the rank ordering of the probabilities. Here are the steps to build a Lift/Gain chart:

Step 1 : Calculate probability for each observation
Step 2 : Rank these probabilities in decreasing order.
Step 3 : Build deciles with each group having almost 10% of the observations.
Step 4 : Calculate the response rate at each deciles for Good (Responders) ,Bad (Non-responders) and total.

The Greater the area between the Lift / Gain and Baseline, the Better the model.

**3. Kolomogorov Smirnov chart:**

K-S or Kolmogorov-Smirnov chart measures performance of classification models. More accurately, K-S is a measure of the degree of separation between the positive and negative distributions. The K-S is 100, if the scores partition the population into two separate groups in which one group contains all the positives and the other all the negatives.
On the other hand, If the model cannot differentiate between positives and negatives, then it is as if the model selects cases randomly from the population. The K-S would be 0. In most classification models the K-S will fall between 0 and 100, and that the higher the value the better the model is at separating the positive from negative cases.

**4. ROC curve (ROC) and Area Under Curve (AUC):**

The ROC (Receiver operating characteristic) curve is the plot between sensitivity and (1- specificity). (1- specificity) is also known as false positive rate and sensitivity is also known as True Positive rate.

For each sensitivity, we get a different specificity.The two vary as follows:

![image](https://user-images.githubusercontent.com/63853707/123633161-7c4a2680-d836-11eb-8a77-8297e9499a84.png)

To bring this curve down to a single number, we find the area under this curve (AUC).Hence AUC itself is the ratio under the curve and the total area.

**NOTE:**
Why should you use ROC and not metrics like lift curve?

Lift is dependent on total response rate of the population. Hence, if the response rate of the population changes, the same model will give a different lift chart. A solution to this concern can be true lift chart (finding the ratio of lift and perfect model lift at each decile). But such ratio rarely makes sense for the business.

ROC curve on the other hand is almost independent of the response rate. This is because it has the two axis coming out from columnar calculations of confusion matrix. The numerator and denominator of both x and y axis will change on similar scale in case of response rate shift.

**5. Gini Coefficient:**

Gini coefficient is sometimes used in classification problems. It is ratio between area between the ROC curve and the diagnol line & the area of the above triangle. Following is the formulae used :

Gini = 2*AUC – 1

**6. Concordant – Discordant ratio:**

Concordant – Discordant ratio is also used in Classification Problem. We take pair of all features. We choose all the pairs where we will find one responder and other non-responder.The concordant pair is where the probability of responder was higher than non-responder. Whereas discordant pair is where the vice-versa holds true. In case both the probabilities were equal, we say its a tie. We calculate number of concordant and discordant pair.

**7. Root Mean Squared Error (RMSE):**

RMSE is used in regression problems. 

![image](https://user-images.githubusercontent.com/63853707/123638679-10b78780-d83d-11eb-8a90-f1b178d25aa7.png)

where, N is Total Number of Observations

**8. R-Squared:**

R-squared or R2 explains the degree to which your input variables explain the variation of your output / predicted variable. So, if R-square is 0.8, it means 80% of the variation in the output variable is explained by the input variables. So, in simple terms, higher the R squared, the more variation is explained by your input variables and hence better is your model.

However, the problem with R-squared is that it will either stay the same or increase with addition of more variables, even if they do not have any relationship with the output variables. This is where “Adjusted R square” comes to help. Adjusted R-square penalizes you for adding variables which do not improve your existing model. The Adjusted R-squared takes into account the number of independent variables used for predicting the target variable. In doing so, we can determine whether adding new variables to the model actually increases the model fit.

R-squared formula:

![image](https://user-images.githubusercontent.com/63853707/123639267-a3582680-d83d-11eb-97b3-23f96b72a37b.png)


Adjusted R square formula:

![image](https://user-images.githubusercontent.com/63853707/123639163-8b80a280-d83d-11eb-81b0-c6a32a289e9c.png)

Here,

n represents the number of data points in our dataset
k represents the number of independent variables, and
R represents the R-squared values determined by the model.
