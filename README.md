# House Price Prediction

## Introduction

### Project Description
 > This practical final project is part of the Introduction to Data Science course in the field of Data Science at VNUHCM - University of Science.

House Price Prediction Problem is a task of estimating the value of real estate based on various features. It involves building and developing a model or algorithm that can predict prices based on property attributes.

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

After collecting the data, the final dataset will consist of 7 features.

![image](https://github.com/TuanTran0910/House-Price-Prediction-IDS/assets/94174684/e18d71da-8875-4034-b0df-47147574c7d3)

## Data Preprocessing

At this phrase, we will handle various problem in raw collected data.

### Drop duplicates

During the data collection process, we have noticed that some houses have been listed for sale multiple times. Therefore, the initial step in your data processing is to drop the duplicate data points in the dataset.

```python
data_VN = data_VN.drop_duplicates().reset_index(drop = True)
```

### Handle Irrational Input Values

In the data collection process, you have observed that some sellers did not pay attention to the unit of currency when listing their properties for sale. Specifically, some may have mistakenly used units such as million, thousand, or even Vietnamese Dong (VND) instead of billion (Vietnamese currency). Instead of discarding data points with such errors, you can perform simple division or multiplication operations to convert them to the correct values. However, please note that the following steps are based on the assumption that no property is listed for a price exceeding 1,000 billion or less than 100 million.

```python
data_VN = handling_price(data_VN, 'Price')
```

### Encode Categorical Variables

To convert the "Roadfrontage" and "Legal" features to numeric values, where they only accept two distinct values, you can map them to "1" and "0" in a meaningful way.

```python
# Binary Variables
data_VN["Roadfrontage"] = list(map(int, data_VN["Roadfrontage"]))

data_VN.loc[data_VN['Legal'] == 'Good', 'Legal'] = int(1)
data_VN.loc[data_VN['Legal'].isna(), 'Legal'] = int(0)
data_VN['Legal'] = pd.to_numeric(data_VN['Legal'])
```

For the "Address" feature, our team has chosen to "geocode" it by converting it into coordinates, including two new features: Lat (Latitude) and Long (Longitude).

```python
data_VN_encoding = createLatLong(data_VN)
```

### More and more

You can see more details inside the notebook

## Modeling

We build a model and train it based on data collected using various algorithms. Afterward, we will compare their performance.

Machine learning algorithms that are used to train the model: 
- eXtreme Gradient Boosting (XGBoost)
- Histogram-based Gradient Boosting
- CatBoost
- ...

```python
# Initialize models
model1 = xgb.XGBRegressor(max_depth=9,
                          learning_rate=0.1216060123693681,
                          n_estimators=632,
                          min_child_weight=52,
                          gamma=0.5109582511543662,
                          subsample=0.9976570598100385,
                          colsample_bytree=0.9719365038898948,
                          reg_alpha=0.911025347022059,
                          reg_lambda=0.8850435124855656)

model2 = HistGradientBoostingRegressor(l2_regularization = 5.390165270582185,
                                       learning_rate = 0.1518554287972511,
                                       max_iter = 201,
                                       max_depth = 17,
                                       max_bins = 251,
                                       max_leaf_nodes = 37,
                                       min_samples_leaf = 5)

model3 = CatBoostRegressor(l2_leaf_reg = 4.3173827907470885,
                           max_bin = 91,
                           subsample = 0.9085139050093797,
                           learning_rate = 0.14374193354140258,
                           n_estimators = 423,
                           max_depth = 7,
                           min_data_in_leaf = 46,
                           verbose = False)

# Training
model1.fit(X_train_scaled, y_train)
y_pred1 = model1.predict(X_test_scaled)

model2.fit(X_train_scaled, y_train)
y_pred2 = model2.predict(X_test_scaled)

model3.fit(X_train_scaled, y_train)
y_pred3 = model3.predict(X_test_scaled)
```

### Basic ensemble

The idea behind ensemble learning is that by combining the predictions of multiple models, the overall performance and accuracy can be improved compared to using a single model.

```python
# Weighted Average
y_pred = y_pred1*0.25 + y_pred2*0.54 + y_pred3*0.21
```

We can see that the results of applying the Weighted Average technique have improved the R2 and RMSE compared to using any of the three models individually. The final results are as follows: In the best case,
- R2 Score: 0.711
- RMSE: 1.60

## Conclusion

Overall, this study demonstrates the successful application of machine learning techniques to the house price prediction problem, providing insights into the factors influencing house prices and enabling more informed decision-making in the real estate market.

## Contribution

This project is a collaborative effort, and we would like to acknowledge the contributions of the following individuals:

- Vo Thi Khanh Linh
- Nguyen Nhat Minh Thu
- Nguyen Dang Anh Thu
- Pham Duy Son

We would like to express our gratitude to all the contributors for their hard work and dedication to this project. Without their efforts, this project would not have been possible.
