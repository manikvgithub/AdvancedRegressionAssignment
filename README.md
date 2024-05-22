# Advanced Linear Regression Assignment
A US based housing company called Surprise Housing wants to enter Australian Market.  The company uses data analytics to purchase houses at a price below their actual values and flip them on at a higher price. For the same purpose, the company has collected a data set from the sale of houses in Australia. 

The Company is looking for buying prospective properties and enter the market. 

This assignment aims to come up with  a regression model using regularisation technique in order to predict what variables are important and worth considering to help the company decide whether to invest in them or not.


## Table of Contents
* [Project Details and Approach](#project-details-and-approach)
* [Technologies Used](#technologies-used)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)


## Project Details and Approach
The primary objective of the project is to come up with a best fit linear regression model using regularization techniques by applying Ridge and Lasso methods. It aims to find the top predictive variables (features) that will help the company in identifying parameters for prospective investments in future.   

The data set provided consisted of 81 columns and 1460 rows in an excel sheet. This data is about past sales over the years in Australia and included details such as Living Area, Street where the house is located, whether the house has got garage and if so how many cars could be accomodated, how many floors the house has, whether the house is fenced or not, whether it had swimming pool or not, when it was built and when it was remodeled and when it was sold etc.

From the given data set, the following approach was taken to build the model:

  Step 1: Reading and Understanding  data 
       -  There were 1460 rows and 81 columns provided in the data set.  Out of these there were several variables with null values.
       -  Evidently, the SalePrice was the target variable and the remaining were Predictive ones. It also had one index column.
       

  Step 2: Cleaning Data
       - The index column "Id" was removed as it would not be useful for the analysis
       - There were columns with more than 45% null values - Alley, MasVnrType, FirePlaceQu, PoolQC, Fence, MiscFeature - which were dropped from the analysis
       - There were 33 categorical variables.  Out of these, the variables Utilities was removed as it contained only 2 distinct values and 1459 out of 1460 were AllPub and a single different value is NoSeWa.  Evidently, there is no variation in this feature and wont help in regression line modeling and hence was dropped.
        - Imputaion was done on the following variables based on certain logic:
             - LotFrontage - applied mean() value for the missing values
             - MasVnrArea - applied mean() value for the missing values
             - From the data dictionary, found that absence of values for certain variables are valid.  It just that they are not available.   For instance, BsmtQual which stores the height of the basement could have a Null value indicating that there is no Basement in the house.  The variables that were imputed with None for Null values are: BsmtQual,  BsmtCond, BsmtExposure, BsmtFinType1,BsmtFinType2, GarageType, GarageFinish, GarageQual and GarageCond
             - For Electrical variable, there was only 1 missing value.  This value was replaced with the value that was occuring most for this column.
             - Also dropped GarageYrBlt column as there were missing values it could not be imputed with any specific value.

  Step 3: Label Encoding categorical Variables
        - Applied Label Encoding techinques for the following categorical variable so as to have a better readability as well as to maintain the same number of columns. These columns after encoding as 0,1,2 etc for their respective values were stored as <Original Variable Name_encoded> column. For example, a new columns called MSSubCLass_encoding was created and it contained the actual encoded values of the original MSSubCLass column.  Post encoding exercise, the original columns were removed from the data set.

        MSSubClass, MSZoning,Street,LotShape,LandContour,LotConfig,LandSlope,Neighborhood,Condition1,Condition2,
        BldgType,HouseStyle,RoofStyle,RoofMatl,Exterior1st,Exterior2nd,ExterQual,ExterCond,Foundation,BsmtQual,
        BsmtCond,BsmtExposure,BsmtFinType1,BsmtFinType2,Heating,HeatingQC,CentralAir,Electrical,KitchenQual,
        Functional,GarageType,GarageFinish,GarageQual,GarageCond,PavedDrive,SaleType,SaleCondition

    Step 4:  Splitting the Data into Training and Testing Sets
          - The data was split into training and test data sets with a 70:30 ratio
          - Applied the min-max scalar approach to bring the following independent variables with continous values 
             LotFrontage, LotArea, MasVnrArea, BsmtFinSF1, BsmtFinSF2,BsmtUnfSF,TotalBsmtSF 
             ,1stFlrSF,2ndFlrSF,LowQualFinSF,GrLivArea,GarageArea, WoodDeckSF, OpenPorchSF, 
              EnclosedPorch, 3SsnPorch, ScreenPorch, PoolArea,MiscVal

    Step 5: Building Ridge and Lasso Models using Regulaization techniques
           - The model building was applied on the training dataset after all the above mentioned cleanups and imputations.
           - For fitting these models, 5 folds were considered for cross validation.
           - Different alpha values were used to find the best fit.
           - The best fit model for Ridge yielded an alpha value of 0.3 while that for Lasso was 0.0001.
           - The R2 values for Ridge on training and test sets were 0.840 and 0.827
           - The R2 values for Lasso on training and test sets were 0.837 and 0.835
    
     Step 6: Model Interpretation
           - The best alpha value using Ridge method is 0.3
           - The best alpha value using Lasso method is 0.0001
            - The R2 scores for Train and Test with this alpha values for Ridge is 0.84 and 0.827 respectively 
            - The R2 scores for Train and Test with this alpha values for Lasso is 0.837 and 0.835 respectively 
            - Since train and test R2 scores for both Ride and Lasso are close to each other, it can be concluded that there is no overfitting or underfitting.
            - Based on what was fitted, for Ridge regression method, the top 5 predictive variables are: 
                     GrLivArea, 1stFlrSF, 2ndFlrSF, LotArea, MasVnrArea
            - Similarly, based on what was fitted, for Lasso regression method, the top 5 predictive variables are: 
                    GrLivArea, MasVnrArea, OverallQual, LandSlope_encoded, BsmtFullBath
            - It can be safely concluded from the above results that people prefer the GrLivArea feature which stands for "Above grade (groud) Living Area (in square feet)" to be the primary consideration for purchasing house.  This also make sense practically as most of us prefer the same primarily before anything else while purchasing properties.   

## Conclusions
   After completing the analysis, the following observations were interpreted:

a. The company could focus on the following five parameters the most while looking for prospective property purchases 
     GrLivArea, MasVnrArea, OverallQual, LandSlope_encoded, BsmtFullBath
b. Both Ridge and Lasso models resulted in GrLivArea - that is - Living Area in square feet to be most prominent of variables
c. Also, both models resulted in GrLivArea and MasVnrArea variables in the top 5.


## Technologies Used
- python 3.11.5
- numpy 1.24.3
- pandas 2.0.3
- matplotlib 3.7.2
- seaborn 0.12.2
- Jupyter Notebook 6.5.4
- scikit-learn 1.3.0
- statsmodels 0.14.0

## Acknowledgements
References 
- stackoverflow and geekforgeek websites for python examples
- Course materials from upGrad curriculam


## Contact
Manikandan Krishnamurthy Vembu (https://github.com/manikvgithub)
