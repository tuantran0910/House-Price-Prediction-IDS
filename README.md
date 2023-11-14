# House Price Prediction

## Introduction

### Project Description
 > This practical final project is part of the Introduction to Data Science course in the field of Data Science at VNUHCM - University of Science.

House Price Prediction Problem is a task of estimating the value of real estate based on various factors. It involves building and developing a model or algorithm that can predict prices based on property attributes.

The goal of house price prediction is to provide a reliable estimate of the buying or selling price for buyers, sellers, real estate agents, or financial institutions to make informed decisions in transactions. By analyzing past and current buying and selling transactions in the market, considering factors such as location, size, number of rooms in the property, amenities in the neighborhood, and market trends, prediction models are built and trained to accurately estimate the price of a house.

House price prediction is a regression problem because the target variable (house price) is a continuous variable. Regression models such as linear regression, decision trees, random forest, support vector machines, or gradient boosting algorithms are commonly used for this task.

### Team members

| Name                | Student ID | Contribution % | Note           |
|---------------------|------------|----------------|----------------|
| Võ Thị Khánh Linh   | 21280070   | 100%           | Group leader   |
| Nguyễn Nhật Minh Thư | 21280112   | 100%           |                |
| Nguyễn Đặng Anh Thư  | 21280111   | 100%           |                |
| Trần Ngọc Tuấn      | 21280058   | 100%           |                |
| Phạm Duy Sơn        | 21280107   | 100%           |                |

### Project Workflow

![image](https://github.com/TuanTran0910/House-Price-Prediction-IDS/assets/94174684/45cf125b-7b0a-40aa-8f25-c16b6445bd0f)

## Data Collection

To efficiently and automatically gather data, we will utilize the technique of web scraping. Our objective is to extract information related to real estate transactions from this [website](https://batdongsan.vn/ban-nha/). Specifically, we aim to collect data on various property attributes such as the number of floors, bedrooms, bathrooms, the area in square meters, location, road frontage, legal status, as well as the selling prices of the properties.

To crawl information from real estate website, in this project we will function ```scrape_this```:

```python
vn = scrape_this(province, num_page, district_list, province_wards)
```

The final dataset after being collected:

![image](https://github.com/TuanTran0910/House-Price-Prediction-IDS/assets/94174684/e18d71da-8875-4034-b0df-47147574c7d3)

