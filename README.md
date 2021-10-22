# LFA-Rossmann_Store_sales_prediction
This repository contains scripts that sales prediction machine learnin for Rossmann Drug Stores

Rossmann operates over 3,000 drug stores in 7 European countries. Currently, Rossmann store managers are tasked with predicting their daily sales for up to six weeks in advance. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality, and locality. With thousands of individual managers predicting sales based on their unique circumstances, the accuracy of results can be quite varied.

![image](https://user-images.githubusercontent.com/88016259/138372302-d5e1f615-00f5-4ffa-9e82-4b096c3e6fbe.png)

# Business problem
The CFO of Rossmann Drug Stores requested a sales predction for each store for the next six weeks in order to define a budget for stores renovation. The current prediction was not satisfactory as there were several inconsistencies. In this context, I developed a machine learning model in order to provide more accurately forecast store sales.
# Business Assumptions
- The days when stores were closed were removed from the analysis.
- Only stores with sales values bigger than 0 were considered.
- For stores which did not have Competition Distance information, it was considered that the distance should be the longest distance observed in the data set.
# Data Description
You are provided with historical sales data for 1,115 Rossmann stores. The task is to forecast the "Sales" column for the test set. Note that some stores in the dataset were temporarily closed for refurbishment.
# Files
- train.csv - historical data including Sales
- test.csv - historical data excluding Sales
- sample_submission.csv - a sample submission file in the correct format
- store.csv - supplemental information about the stores
# Attribute List
- Id - an Id that represents a (Store, Date) duple within the test set
- Store - a unique Id for each store
- Sales - the turnover for any given day (this is what you are predicting)
- Customers - the number of customers on a given day
- Open - an indicator for whether the store was open: 0 = closed, 1 = open
- StateHoliday - indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None
- SchoolHoliday - indicates if the (Store, Date) was affected by the closure of public schools
- StoreType - differentiates between 4 different store models: a, b, c, d
- Assortment - describes an assortment level: a = basic, b = extra, c = extended
- CompetitionDistance - distance in meters to the nearest competitor store
- CompetitionOpenSince[Month/Year] - gives the approximate year and month of the time the nearest competitor was opened
- Promo - indicates whether a store is running a promo on that day
- Promo2 - Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating
- Promo2Since[Year/Week] - describes the year and calendar week when the store started participating in Promo2
- PromoInterval - describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store
# Solution Strategy
The method used for the project was CRISP-DM, apply as the steps below:

**Step 01**. **Data Description:** The goal is to use statistical metrics to identify outliers in the business scope and also analyze basic statistical metrics such as: mean, median, maximum, minimum, range, skew, curtosis and standard deviation.

**Step 02**. **Feature Engineering**: The goal of this step is to obtain new attributes based on the original variables, in order to better describe the phenomenon to be modeled.

**Step 03**. **Data Filtering**: The goal of this step it to filter rows and delete columns that are not relevant for the model or are not part of the business scope.

**Step 04**. **Exploratory Data Analysis**: The goal of this step is to explore the data to find insights and better understand the impact of variables on model learning.

**Step 05**. **Data Preparation**: The goal of this step is to prepare the data prepare data for application of the machine learning model.  

**Step 06**. **Feature Selection**: The goal of this step is to select the better attributes to train the model. It was used Boruta Algorithm to make the selection.

**Step 07**. **Machine Learning Modeling**: The goal of this step is to do the machine learning model training.

**Step 08**. **Hyperparameter Fine Tunning**: The goal of this step is to choose the best values for each of the parameters of the model selected in the previous step.

**Step 09**. **Convert model performance to business values**:  The goal of this step is to convert model performance to a business result.

**Step 10**. **Deploy Model to Production**: The goal of this step is to publish the model in a cloud environment so that other people or services can use the results to improve the business decision. The cloud application platform choosed was Heroku.

**Step 11**. **Telegram Bot**: The goal of this step is to create a bot on the telegram app, that make possible to consult the forecast at any time.

# Data Insigths
**H1**: Stores with larger assortments should sell more.

**FALSE**: Stores with a larger assortment sell LESS.
![image](https://user-images.githubusercontent.com/88016259/138381065-868977a4-6d16-4db6-a479-896545c29635.png)

**H2**: Stores with closer competitors should sell less.

**FALSE**: Stores with CLOSER COMPETITORS sell MORE.
![image](https://user-images.githubusercontent.com/88016259/138381733-bb96acbb-c481-43d6-9761-28fea97368a9.png)

**H3**: Stores with long time competitors should sell more.

**FALSE**: Stores with COMPETITORS LONG TIME sell LESS.
![image](https://user-images.githubusercontent.com/88016259/138382328-92396ed0-a9ce-4589-8d94-6c0ea36076cd.png)

**H4**: Stores with promotions active for long time should sell more.

**FALSE**: Stores with promotions active for long time sell less after a certain period of promotion.
![image](https://user-images.githubusercontent.com/88016259/138382828-e06b8a84-def4-412c-9487-af7d450b321c.png)

**H6**: Stores with more consecutive promotions should sell MORE.

**FALSE**: Stores with more consecutive promotions sell LESS.
![image](https://user-images.githubusercontent.com/88016259/138383185-75bed694-386f-43b1-9be5-8d8540c00d6b.png)

**H7**: Stores open during the Christmas holiday should sell more.

**FALSE**: Stores open during the Christmas holiday sell less.
![image](https://user-images.githubusercontent.com/88016259/138383538-a6d256a2-cfb5-4e76-b30a-0bb38e0a5fe3.png)

**H8**: Stores should sell more over the years.

**FALSE**: Stores sell less over the years.
![image](https://user-images.githubusercontent.com/88016259/138383833-4ca81ed3-8c28-4f0f-ad91-361dc8118bed.png)

**H9**: Stores should sell more in the second half of the year.

**FALSE**: Stores sell less in the second half of the year.
![image](https://user-images.githubusercontent.com/88016259/138384211-264c75e2-1531-4b85-96a5-5616bcb043b7.png)

**H10**: Stores should sell more after the 10th of each month.

**TRUE**: Stores sell more after the 10th of each month.
![image](https://user-images.githubusercontent.com/88016259/138384664-e67cfd5d-4e9e-44af-bd56-e671c5f820cb.png)

**H11**: Stores should sell less on weekends.

**TRUE**: Stores sell less on the weekend.
![image](https://user-images.githubusercontent.com/88016259/138384844-eeb23dc1-08f3-4d4c-962e-38e0a548d6ad.png)

**H12**: Stores should sell less during school holidays

**TRUE**: Stores sell less during school holidays, except July and August.
![image](https://user-images.githubusercontent.com/88016259/138385046-fb09a01e-9d08-4b47-a383-af9862dcd6ff.png)


