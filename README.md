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

## CODING AND OUTPUT
        
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from google.colab import files

# Read dataset
data = pd.read_csv('titanic_dataset.csv')

print("First 5 Rows:")
print(data.head())

print("\nDataset Information:")
data.info()

print("\nMissing Values:")
print(data.isnull().sum())

# Handle missing values
data['Age'] = data['Age'].fillna(data['Age'].median())
data['Embarked'] = data['Embarked'].fillna(data['Embarked'].mode()[0])
data['Cabin'] = data['Cabin'].fillna('Unknown')

print("\nMissing values handled.")

# Boxplot before removing outliers
sns.boxplot(x=data['Fare'])
plt.title("Boxplot - Fare")
plt.show()

# Remove outliers using IQR
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, 'Fare')

print("\nOutliers removed using IQR method.")

# Countplot
sns.countplot(x='Sex', data=data)
plt.title("Countplot - Gender Distribution")
plt.show()

# Age distribution
sns.displot(data['Age'], kde=True)
plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()

# Cross tabulation
crosstab_result = pd.crosstab(data['Sex'], data['Survived'])
print("\nCross Tabulation Result:")
print(crosstab_result)

# Correlation heatmap
correlation_matrix = data.select_dtypes(include=np.number).drop(
    columns=['PassengerId'], errors='ignore'
).corr()

sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()

# Final cleaned dataset
print("\nFinal Dataset:")
print(data.head())

print("\nFinal Dataset Shape:", data.shape)

print("\nRemaining Missing Values:")
print(data.isnull().sum())

# Save cleaned dataset
data.to_csv('Titanic_Cleaned_Dataset.csv', index=False)

# Download cleaned dataset
files.download('Titanic_Cleaned_Dataset.csv')

<img width="520" height="455" alt="image" src="https://github.com/user-attachments/assets/075f9454-c804-44fc-9996-7ef0dad38e9f" />
<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/cffad442-08cf-4941-a888-e20697e5c816" />
<img width="489" height="512" alt="image" src="https://github.com/user-attachments/assets/9b907e4a-e897-4898-b0d0-e9ede7bd3bb4" />
<img width="635" height="552" alt="image" src="https://github.com/user-attachments/assets/7b4807dc-2d45-4793-b054-a80860e5830a" />
<img width="437" height="420" alt="image" src="https://github.com/user-attachments/assets/b1aae3a6-0bd1-46e4-a001-2df24a90b5cc" />





# RESULT
        Thus, Exploratory Data Analysis (EDA) was successfully performed on the Titanic dataset using Python. Missing values were handled using mean, median and mode methods. Outliers were detected using a boxplot and removed using the Interquartile Range (IQR) method. Countplot, displot, cross-tabulation and heatmap were used to analyze and visualize the dataset. Finally, the cleaned dataset was saved as a CSV file and downloaded successfully.

# SUMMARY
          - Successfully performed data cleaning.
          - Handled missing values in Age, Embarked and Cabin columns.
          - Detected and removed Fare outliers using the IQR method.
          - Visualized categorical data using Countplot.
          - Analyzed Age distribution using Displot.
          - Examined relationships using Cross Tabulation.
          - Visualized numerical correlations using Heatmap.
          - Saved and downloaded the cleaned Titanic dataset.
          Conclusion: The experiment helped us understand the dataset, identify patterns, handle missing values, remove outliers and perform Exploratory Data       Analysis successfully.
