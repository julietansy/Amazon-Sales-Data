# Amazon-Sales-Data

## Introduction


## Data Source
The dataset originates from the [Amazon Sales Dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset/) on Kaggle. Within the dataset, it contains more than 1000 Amazon Products with details on it's ratings and reviews as listed on the official Amazon (India) webpage.

        # Load raw data
        data = pd.read_csv('/kaggle/input/amazon-sales-dataset/amazon.csv')

Containing 1465 rows and 16 fields detailing product information, this dataset offers comprehensive insights.

## Python Libraries

        import pandas as pd
        import numpy as np
        import matplotlib.pyplot as plt
        import seaborn as sns

## Data Cleaning

Upon initial assessment, no duplicate rows were identified. However, 2 rows, approximately 0.14%, of the data within the 'Rating Count' column contains null values. Due to their minimal presence, these two rows with null values were excluded from the dataset. Furthermore, though all columns initially possessed object data types, four fields featured symbols. These symbols were removed to convert the respective data types to float.

        # Replace symbols for relevant columns
        data['Discounted Price'] = data['Discounted Price'].str.replace("₹",'').str.replace(",",'')
        data['Actual Price'] = data['Actual Price'].str.replace("₹",'').str.replace(",",'')
        data['Discount Percentage'] = data['Discount Percentage'].str.replace("%",'')
        data['Rating Count'] = data['Rating Count'].str.replace(",",'')

        # Convert data type to float
        data = data.astype({'Discounted Price': 'float64', 'Actual Price': 'float64', 'Discount Percentage': 'float64', 'Rating': 'float64', 'Rating Count': 'float64'})

        # Check for null value in dataset and removed
        nullvalue = data.isna().sum()
        nullvalue = nullvalue[nullvalue>0] / len(data) * 100
        nullvalue = nullvalue.round(2).to_frame('%Null').sort_values('%Null', axis=0, ascending=False)
        data = data.loc[~data['Rating Count'].isnull()]
