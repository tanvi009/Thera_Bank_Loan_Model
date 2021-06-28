**Thera Bank - Loan Purchase Modeling**

This case is about a bank (Thera Bank) which has a growing customer base. Majority of these customers are liability customers (depositors) with varying size of deposits. The number of customers who are also borrowers (asset customers) is quite small, and the bank is interested in expanding this base rapidly to bring in more loan business and in the process, earn more through the interest on loans. In particular, the management wants to explore ways of converting its liability customers to personal loan customers (while retaining them as depositors). A campaign that the bank ran last year for liability customers showed a healthy conversion rate of over 9% success. This has encouraged the retail marketing department to devise campaigns with better target marketing to increase the success ratio with a minimal budget. The department wants to build a model that will help them identify the potential customers who have a higher probability of purchasing the loan. This will increase the success ratio while at the same time reduce the cost of the campaign. The dataset has data on 5000 customers. The data include customer demographic information (age, income, etc.), the customer's relationship with the bank (mortgage, securities account, etc.), and the customer response to the last personal loan campaign (Personal Loan). Among these 5000 customers, only 480 (= 9.6%) accepted the personal loan that was offered to them in the earlier campaign.

Job is to build the best model which can classify the right customers who have a higher probability of purchasing the loan. 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
Entropy can be defined as a measure of the purity of the sub split. Entropy always lies between 0 to 1. In physics, entropy represents the unpredictability of a random variable. The chance of having Head or Tail from a fair coin is 50/50, and so its entropy value is 1, which is the highest value for randomness. On the other hand, having a value 0 indicates the corresponding event is destined.The entropy of any split can be calculated by this formula:

![image](https://user-images.githubusercontent.com/63853707/123602893-e2bf4c80-d816-11eb-976e-baf5df977361.png)

**4. Information Gain:**
After obtaining the entropy for each category, we can combine them to get the information gain values for the features. The more information we gain, the better. The formula is:

![image](https://user-images.githubusercontent.com/63853707/123603058-169a7200-d817-11eb-9507-c70b42d48f37.png)



