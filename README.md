# phase_one_prj
Explorative_Data _Analysis_Superstore_data_2014-18

# Explorative Data Analysis (EDA)

The project aim at evaluating the value of discounting furniture prices towards the superstore sales and profit. The Superstore dataset contains information about sales, orders, customers, and furniture products. The projec will analyze the data to estabish relatiships, trends and patterns to help in making optimal data driven business decisions.

<Background -->

The prospects for growth in demand of furniture products has been on an upward trajectory informed by increased disposable income and changing lifestyle preferences towards stylish products. In the United States, this positive outlook of the market has attracted not only further investment in the market from the big firms in the sector, but also seen entrant of small and medium enterprises. Additionally, the rapidly changing E-commerce is forcing firm to rethink their strategies to maintain an edge in the midst of cut throat competition. Superstores that deals in furniture products across all the States in the USA introduced discount to guarantee price leadership, maintain market share and increase revenue and profits.

<Business case  -->
The project aim at evaluating the value of discounting furniture prices towards the superstore sales and profit.

<Objectives  -->
Time Series Analysis to evaluate the trends in superstore sales, profit, or discount between 2014 and 2017 -To analyze trend in total sales per state -To anlyze market segments -To determine the relationship between discount and profit.

<Data sources  -->
the project will be based on super store data of 2014 to 2018 downloaded from kaggle

Codes
# loading the required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import csv
import seaborn as sns

# authorization module to access files from from my laptop operating system
import os     

# establish the current working directory location
os.getcwd()

# loading excel file into panda dataframe without the first column
df = pd.read_excel("Sample - Superstore.xls", index_col=0)

# to check if the loading was successful
# get the first five rows of the file
df.head()

# prints out the column names
df.columns

# checking for the number of rows and columns 
df.shape

#interrogate data edges
df.tail ()

# checking for the overview of the data
df.info()
# key observations from data overview
# the data set has no missing values
# most data type is in form of object

# count to see the number and frequency of product categories
product_count_per_category = df.groupby('Category').size().reset_index(name='Product_Count')

# Displaying the result
print(product_count_per_category)

# runng descriptive statistics of the dataset
df.describe()
# Observations from the descriptive statistics
# the data generated decriptives for float and integer data
# postal code statistics are not necessary since they dont make sense!
# Average sales was 229.858 with the minimum being 0.444 and max 22638 dollars
# Average quantity was 3.79 units ragnging from a low of 1 and maximum of 14 products
# Average disount offered was 0.156 percent ranging between a min of 0.0 and max of 0.8 percent
# Average profit was 28.657 ranging from a low of -6599(loss) and maximum of 8399.976 dollars

# Visualizing trends in sales over the years
# first is to tranform 'Order Date' to datetime format
df['Order Date'] = pd.to_datetime(df['Order Date'])

# grouping 'Order Date' and calculate the total sales for each date
sales_trend = df.groupby('Order Date')['Sales'].sum()

# generating sales trend plot
plt.figure(figsize=(10, 8))
plt.plot(sales_trend.index, sales_trend.values, marker='o', linestyle='-', color='r')
plt.xlabel('Order Date')
plt.ylabel('Total Sales')
plt.title('Sales Trend Over Time')
plt.xticks(rotation=90)
plt.grid(True)
plt.show()


# observation from trends in sales
# the data is split into segments of seven months
# sales has bee oscillating between 0 and slightly less than 15,000
# execption of two periods when sales overshort to over 25,000 and slighlt under 20,000
# around April of 2014 and May of 2016

# Plot the sales trend
plt.figure(figsize=(8, 6))
plt.plot(sales_trend.index, sales_trend.values, marker='o', linestyle='-', color='g')
plt.xlabel('Order Date')
plt.ylabel('Profit')
plt.title('Profit Trend Over Time')
plt.xticks(rotation=90)
plt.grid(True)
plt.show()

# observation from trends in sales
# the data is split into segments of seven months
# profit has been oscillating between 7000 and 0 with most concentrated below 5,000
# execption of two periods when sales overshort to over 25,000 and slighlt under 20,000
# around April of 2014 and May of 2016

# Segment customer categories for further analysis
segment_data = df.groupby('Segment').agg({
    'Sales': 'mean',
    'Profit': 'sum',
    'Quantity': 'sum'
}).reset_index()

# plotting segmented data 
plt.figure(figsize=(8, 6))
plt.bar(segment_data['Segment'], segment_data['Sales'])
plt.xlabel('Segment')
plt.ylabel('National Average Sales')
plt.title('National Average Sales by Segment')
plt.xticks(rotation=90)
plt.grid(True)
plt.show()

# observations from the segmented data
# there are three segment of superstores customers 
# all the segments have sales of over 200 aggregate 
# with consumer segment having the lowest share
# and home office having the highest average

# grouping segment and state by county to combined analysis
# Geographic analysis
state_data = df.groupby('State').agg({
    'Sales': 'mean',
    'Profit': 'sum',
    'Quantity': 'sum'
}).reset_index()

# estimate the distribution of sales per state to see the one with the highest market 
# average sales across the States
# creating a plot of average sales per state
plt.figure(figsize=(10, 20))
plt.barh(state_data['State'], state_data['Sales'])
plt.xlabel('State')
plt.ylabel('Average Sales')
plt.title('Total Average Sales by State')
plt.xticks(rotation=45)
plt.grid(True)
plt.show()

# key observations from the sales by state
# Wyoming command the largest market share followed by Vermont and Nevada states 
# with average sale of over 400 and 1,600
# 14 states had sales below less that 200 and below aggregate mean of 229
# South Darkota and Kansas has the least market share 

# assessing the way these variables are related and strength of relationship
# correlation between the quantity of products sold, discount offered and profit
correlation_matrix = df[['Profit', 'Discount', 'Sales']].corr()
print("Correlation Matrix:")
print(correlation_matrix)

# observation from the correlation data
# profit has a weak and negative correlation with discout;
# this implies that disount eats on profit as 
# increase in discount relates to a drop in profit
# Profit has a moderately stronger correlation (0.479064) with sales
# this implies that increased sales relate to moderate increa in profits
# discount has a weak negative relation with sales;
# this implies that increase in discount relates to marginal decrease in sales

# Plotting a correlation heatmap for Sales, Discount and profit for better visualization
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)

# Display the plot
plt.title('Correlation Heatmap')
plt.show()
https://github.com/Consmuhia




![Logo](https://aidalabpsu.com/wp-content/uploads/2022/03/logo-300x151.png)



## API Reference

#### Get all items

```http
  GET /api/items
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. Your API key |

#### Get item

```http
  GET /api/items/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of item to fetch |

#### add(num1, num2)

Takes two numbers and returns the sum.


## Acknowledgements

 - The Superstore dataset used in this project is sourced from [https://community.tableau.com/s/question/0D54T00000CWeX8SAL/sample-superstore-sales-excelxls]

## 🚀 About Me
I'm a data science student at Moringa School Kenya. 

## Screenshots

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)


## Roadmap

- Additional browser support

- Add more integrations


## Environment Variables

To run this project, you will need to add the following environment variables to your .env file

`API_KEY`

`ANOTHER_API_KEY
