# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING
```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

Reading the file and display first five data:

```python
df=pd.read_csv("titanic.csv.csv")
df.head()
```

```python
df.info()
df.describe()
```

Data Cleaning:

```python


for column in df.select_dtypes(include='object').columns:
    df[column] = df[column].fillna(df[column].mode()[0])

for column in df.select_dtypes(include='number').columns:
    df[column] = df[column].fillna(df[column].median())

print("Data cleaning is performed successfully")
```

Box Plot:


```python
plt.figure(figsize=(6,10))
sns.boxplot(x=df["Age"])
plt.title("Boxplot - Age")
plt.show()
```

```python
plt.figure(figsize=(10,10))
sns.boxplot(x=df["Fare"])
plt.title("Boxplot - Fare")
plt.show()
```

Remove Outliers Using IQR Method

```python
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(df, "Age")
data = remove_outliers_iqr(df, "Fare")
print("Outliers removed using IQR method.\n")
```

Countplot for Categorical Data

```python
plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=df)
plt.title("Countplot - Survival Distribution")
plt.show()
```

```python
plt.figure(figsize=(6,4))
sns.countplot(x="Sex", data=df)
plt.title("Countplot - Gender Distribution")
plt.show()
```

```python
plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=df)
plt.title("Countplot - Passenger Class Distribution")
plt.show()
```

Displot for Univariate Distribution

```python
sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()
```

```python
sns.displot(data["Fare"], kde=True, height=6, aspect=2.5)
plt.title("Displot - Fare Distribution")
plt.show()
```

Cross Tabulation

```python
print("Cross Tabulation")
print(pd.crosstab(df['Sex'],df['Survived']))
print(pd.crosstab(df["Pclass"],df["Survived"]))
```

Heatmap for Correlation Analysis

```python
plt.figure(figsize=(8,4))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()
```

# Output

<img width="1430" height="265" alt="Screenshot 2026-03-09 210041" src="https://github.com/user-attachments/assets/5699ded6-eb5f-4dcd-9907-ebba569dc89f" />


<img width="1212" height="813" alt="Screenshot 2026-03-09 210133" src="https://github.com/user-attachments/assets/11758926-0769-4bb4-85f0-fafecb96fe75" />



<img width="562" height="879" alt="Screenshot 2026-03-09 210323" src="https://github.com/user-attachments/assets/3ca74835-a72e-40d7-8f53-3cdaee7dcca4" />



<img width="669" height="684" alt="Screenshot 2026-03-09 210535" src="https://github.com/user-attachments/assets/efb8eed2-25d2-49b0-8b6a-4331964db5de" />



<img width="674" height="406" alt="Screenshot 2026-03-09 210616" src="https://github.com/user-attachments/assets/48a8f6f5-6ba9-41f9-8f8f-4c423feb1eab" />



<img width="708" height="433" alt="image" src="https://github.com/user-attachments/assets/97b6ecd2-7497-4a32-9c63-fd1278e59025" />



<img width="633" height="429" alt="image" src="https://github.com/user-attachments/assets/dd29e44b-a295-4ec8-9872-c2b4d7dc061a" />



<img width="647" height="467" alt="image" src="https://github.com/user-attachments/assets/00ee6123-fc17-4d01-8b6a-d0fbb4dbaf7a" />



<img width="666" height="285" alt="image" src="https://github.com/user-attachments/assets/b351ece3-94c6-40b1-9c6b-2631ac4ed6ac" />




<img width="690" height="590" alt="image" src="https://github.com/user-attachments/assets/2d644e7d-02f0-4c27-9da9-5180f8c66aed" />












# RESULT
        Thus the EDA analysis executed successfully.
