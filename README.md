# Predictive Churn Analysis in Credit Card Banking

## 1. Introduction

### 1.1. Background

A consumer credit card bank is facing the problem of customer attrition. They want to analyse the data to find out the reason behind this and leverage the same to predict customers who are likely to drop off. They also want to predict customer churn from the existing data, thereby gaining some insights on how the bank can reduce the customers who have churned.

### 1.2. Objectives

* Find out reasons behind customer churns
* Predict which customer will cancel their service in the future

### 1.3. Methodology & Tools

* Python: data cleaning, data extraction
* Power BI: data visualisation
* Excel: statistics
* Python: model selection & data fitting

## 2. Analysis

### 2.1. Data Cleaning

In this step, I used SQL to delete the last 2 columns due to being irrelevant to this study, and update the Attrition_Flag in the way that is more efficient to conduct further analysis.

### 2.2. Statistics

Here, I’m going to conduct statistical tests to see whether the variables are sufficiently qualified for the analysis. For categorical variables, I’m using the Information Value (IV) test, whereas the z-test is conducted for continuous variables.

#### 2.2.1. Information Value - Categorical Variables

Information Value (IV) is a commonly used measure in credit modelling to assess the predictive power of a given variable. It measures the strength of the relationship between a predictor variable and the response variable. Here, the IV test will be used to answer two questions: if the categorical variables demonstrate the difference between two types of customers, and if these variables are suitable for the prediction model.

IV interpretation:
| Information Value | Variable Predictiveness     |
|-------------------|-----------------------------|
| Less than 0.02    | Not useful for prediction   |
| 0.02 to 0.1       | Weak predictive Power       |
| 0.1 to 0.3        | Medium predictive Power     |
| 0.3 to 0.5        | Strong predictive Power     |
| > 0.5             | Suspicious Predictive Power |

Variables to be tested: Gender, Education_Level, Marital_Status, Income_Category, Card_Category

##### Result

* Gender: 0.01
* Education_Level: 0.009
* Marital_Status: 0.004
* Income_Category: 0.01
* Card_Category: 0.001

The test result of all categorical variables falls under "Not useful for prediction". This is to be considered, even though these variables are in fact needed to be further analysed, for they are the key features of the customer. These variables will be included in the data analysis, then will be further tested prior to building the prediction model.

#### 2.2.2. Z-test - Continuous Variables

A two-tailed z-test is a typical statistical hypothesis test, commonly used for determining whether there is a significant difference between two population means. Here, it is used for continuous variables, verifying if there are significant differences between 2 customer types or not.

Prior to conduct the Z-test, I used SQL to extract the necessary data of 2 types of customers.

##### Hypothesis:

* H0: there is no difference between two types of customer
* Ha: there is difference between two types of customer

Variables to be tested: Customer_Age, Dependent_count, Months_on_book, Total_Relationship_Count, Months_Inactive_12_mon, Contacts_Count_12_mon, Credit_Limit	Total_Revolving_Bal, Avg_Open_To_Buy, Total_Amt_Chng_Q4_Q1, Total_Trans_Amt, Total_Trans_Ct, Total_Ct_Chng_Q4_Q1, Avg_Utilization_Ratio

##### Result:

* The null hypothesis cannot be rejected in 4 variables: Customer_Age, Dependent_count, Months_on_book, Avg_Open_To_Buy. This means that they do not appear to have statistical differences. Thus, these variables will not be used in either data analysis or the prediction model.
* The null hypothesis is rejected in all other variables, which means they are statistically different. They will be used in data analysis and the predicting model.

### 2.3. Data Visualisation

#### 2.3.1. Customer Overview

![Customer Overview](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/1.%20Customer%20Overview.png)

Regarding customer income, less than $40,000 is the majority income of those who cancelled their card (42.5%). It is also applied to existing customers; however, the percentage of this income category is compared to attrited customers (38.93%). Attrited customers, in general, may earn less than existing customers, and they may find other alternatives for their needs, based on their salary.

Regarding marriage, less than half of attrited customers are married (47.33%), whereas half of existing customers are married (50.48%). Perhaps the attrited customer does not seem to seek settlement at the moment. On the other hand, those who seek this credit card service tend to desire financial stability, and are settled/want to settle.

Regarding education, the percentage of “College”, “Post-Graduate”, “Doctorate” level is higher in attrited customers. About existing customers, the percentage of “Graduate”, “High School”, and “Uneducated” is higher. This implies that those who do not put as much emphasis on studying as those willing to reach a higher level tend to be the target customer of this credit card. As they have basic and sufficient education, they tend to seek stability, which corresponds to their marital status. For those who seek further study, their priority is on the academic path, and as suggested from the data, this credit card service may not suit them.

#### 2.3.2. Card Information

![Card Information](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/2.%20Card%20Information.png)

The number of types of cards has revealed possible issues. The majority of card types chosen by the customer is Blue card, that is the most basic one. In the premium ones, problems arise as the attrited/existing ratio comes down to 1:4 in Gold, or even 1:3 at Platinum card. The more luxurious the card becomes, the more customers cancel the card compared to overall figures. The bank should find out the functions of the advanced card, whether the customer feels that the upgrade purchase is worthy enough, or the services these cards offer may cause more issues than the basic card.

Regarding total products that customers own, the majority of attrited customers held only less than 3 products, while most of existing customers hold more than 3 products. This may originate from their need, existing customers have more demands so this service is necessary for them.

The number of inactive months raises a severe issue. When the customer always use the card, whether for transaction, contact, or any purposes, there is a 50% chance they may cancel their card. With high frequency of usage, there might be problems regarding their personal needs, or the fact that they are not satisfied with the provided service. More investigation should be conducted about the service.

The service issues lead to another problem, that is the number of contacts made from the customer to the bank. The more contacts the bank receives from the customer, the more chance that customer will cancel their service. Especially, after 6 times contacted, if there is another problem, the customer will definitely cancel their cards and there will not be a 7th contact.

#### 2.3.3. Credit Usage

![Credit Usage](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/3.%20Credit%20Usage.png)

Overall, attrited customers have less credit limit, and especially much less total revolving balance, than existing customers. This may imply that they either do not need to use the service, or do not want to. This corresponds to card utilisation ratio, where most of attrited customers have 0% of the ratio, compared to fluctuated ratio among existing customers.

#### 2.3.4. Transaction Analysis

![Transaction Analysis](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/4.%20Transaction%20Analysis.png)

Finally, a look into transactions reveals the same pattern as credit usage. In total number of transactions, and changes in transaction counts, it is clear that the figures of attrited customers are much less than those of existing customers. As existing customers have much more transactions and more changes, it may be true that their need for the credit card is much higher than attrited customers.

In addition, regarding the total amount and changes in the amount of credit, again, the figures in existing customers are higher than attrited customers. Not only do the existing customer need this credit card more than attrited customers, they may have higher income, and this matches very well with the previous income analysis.

#### 2.3.5 Conclusion

After the analysis, the most general pattern of the potential customers are:

* People with middle to high income;
* People who seek family stability, who do not seek advanced education but just want to settle down.
The satisfaction of credit card services must be further investigated.

## 3. Suggestions

* Use targeted advertising that speaks directly to the desires of the demographic (family and stability) and highlighting the ease of use and convenience of a credit card for everyday expenses.
* Showcase the benefits that are relevant to the target demographic, such as travel rewards or cashback on everyday expenses like groceries and gas.
* Conduct further investigation for:
    * Credit card functions: focus the investigation on the premium cards to find out if those functions have errors or if they are satisfying for the ranking of the card
    * Frequent users: they have 50% of cancelling their service
    * Find out the nature of customer service, whether there are technical issues or personnel issues

## 4. Prediction model


To investigate the likelihood of other customers to leave the service or not in the future, ML models are to be selected to perform binary classification. After evaluating the possible models using PyCaret library, I decided to pick out 3 models for further fine-tuning (Logistic Rrgression, Support Vector Machine, and XGBoost. After the best parameters are found and the models are built, of of all models, XGBoost seems to perform the best in both PyCaret evaluation and the comparision with 2 other model. However, with these scores, XGBoost could be prone to overfitting. Further fine-tuning is needed.

![Confusion Matrix of XGBoost Model](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/5.%20Confusion%20Matrix%20of%20XGBoost%20Model.png)

![ROC of XGBoost Model](https://github.com/nam-anh-21/Credit-Card-Customer-Churns/blob/main/Images/6.%20ROC%20of%20XGBoost%20Model.png)
