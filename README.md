# **Black Friday Sales Data Analysis**

## **Overview**
This project analyzes **Black Friday sales data** to uncover purchasing trends based on demographic factors such as **age, gender, occupation, and city category**. The dataset is cleaned, processed, and visualized using **Pandas** and **Seaborn**.

## **Dataset**
The dataset (`BlackFriday.csv`) includes various attributes such as:
- **Gender, Age, Marital Status**
- **Occupation, City Category, Stay Duration**
- **Product Categories and Purchase Amount**

## **Project Workflow**
### **1. Data Preprocessing**
- Load the dataset using `pandas`:
  ```python
  import pandas as pd
  df = pd.read_csv("BlackFriday.csv")
  ```
- Check for missing values:
  ```python
  df.isnull().sum()
  ```
- Remove columns with excessive missing values:
  ```python
  del df["Product_Category_2"]
  del df["Product_Category_3"]
  ```

### **2. Exploratory Data Analysis**
- Dataset shape: `df.shape`
- Unique values per column:
  ```python
  df.nunique()
  for column in df.columns:
      print(df[column].nunique(), "\t: ", column)
  ```

### **3. Data Visualization**
#### **Gender-Based Analysis**
- Pie chart for gender distribution:
  ```python
  df.groupby("Gender").size().plot(kind='pie', autopct='%0.1f')
  ```
- Bar chart for total purchase amount by gender:
  ```python
  df.groupby("Gender").sum()['Purchase'].plot(kind='bar')
  ```

#### **Age-Based Insights**
- Age vs Purchase amount (bar plot):
  ```python
  import seaborn as sns
  sns.set(rc={'figure.figsize': (6,6)})
  sns.barplot(x='Age', y='Purchase', data=df, hue='Gender')
  ```
- Unique product distribution by age group:
  ```python
  lst = []
  for i in df['Age'].unique():
      lst.append([i, df[df['Age'] == i]['Product_ID'].nunique()])
  data = pd.DataFrame(lst, columns=['Age', 'Product_ID'])
  sns.barplot(x='Age', y='Product_ID', data=data)
  ```

#### **Marital Status & Occupation Trends**
- Purchase amount by marital status and gender:
  ```python
  sns.barplot(x='Marital_Status', y='Purchase', data=df, hue='Gender')
  ```
- Occupation-based purchase behavior:
  ```python
  df.groupby('Occupation').sum()['Purchase'].sort_values().plot(kind='bar')
  ```

#### **Product Category & City-Based Insights**
- Most purchased product categories:
  ```python
  df.groupby('Product_Category_1').sum()['Purchase'].sort_values().plot(kind='bar')
  ```
- Purchase trends based on city:
  ```python
  df.groupby('City_Category').sum()['Purchase'].sort_values().plot(kind='bar')
  ```

## **Key Learnings**
- **Gender-based trends**: Male consumers contribute a larger share of purchases.
- **Age-driven insights**: Certain age groups purchase specific types of products more frequently.
- **City impact**: Purchase behavior varies based on city category and stay duration.

