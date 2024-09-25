# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df

![image](https://github.com/user-attachments/assets/8072c16b-7745-43ce-bb82-38d877518778)

df.shape

![image](https://github.com/user-attachments/assets/17c87218-971c-460c-a5d5-d466a2beaf31)

df.describe()

![image](https://github.com/user-attachments/assets/af28ee11-1e54-4380-b02d-fb5035d841b4)

df.info()

![image](https://github.com/user-attachments/assets/19320d44-f339-44b0-8635-dd4d644e480e)

df.head(4)
df.tail(4)

![image](https://github.com/user-attachments/assets/2eb31c8b-a01f-4657-8881-7170c82c97c0)

df.isnull().sum()

![image](https://github.com/user-attachments/assets/d143bc6a-7b35-4180-a96a-9989cef93588)

df.dropna(how='any').shape
df.shape

![image](https://github.com/user-attachments/assets/a4641760-7c25-46de-8345-91f8fa9b1b36)

x=df.dropna(how='any')
x

![image](https://github.com/user-attachments/assets/b70c185d-da54-4359-9d5b-8ec75102bcbb)

x2=df.dropna(how='all').shape
mn=df.TOTAL.mean()
mn
df.isnull().sum()

![image](https://github.com/user-attachments/assets/b7a63aaa-4fa7-479c-8ad2-3ee03cd5ee72)

df.TOTAL.fillna(mn,inplace=True)
df

![image](https://github.com/user-attachments/assets/3d05c190-ad74-41af-b689-73aa80bfc20e)

df['M1']

![image](https://github.com/user-attachments/assets/15c5410e-0248-4935-934d-2ddac965dcdc)

df['M1'].fillna(method='ffill',inplace=True)

![image](https://github.com/user-attachments/assets/1bdb3021-72b7-4c00-9ce6-664c4b97d043)


df.duplicated()


![image](https://github.com/user-attachments/assets/6b28cb41-f497-4be0-ab4c-a0723f224c47)


l=df.M1.interpolate()
l

![image](https://github.com/user-attachments/assets/4070d22f-c08e-47e4-b777-f808318b3813)

df['DOB']

![image](https://github.com/user-attachments/assets/16f712d9-8053-4886-ba7d-23bfdf7f6d7e)

x

![image](https://github.com/user-attachments/assets/78d56365-921f-4026-99d2-bc93f60c1ee3)

import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)

![image](https://github.com/user-attachments/assets/987d5006-3dca-4c08-97fe-5591cd5b0cae)


df.dropna(inplace=True)
sns.heatmap(df.isnull(),yticklabels=False,annot=True)

![image](https://github.com/user-attachments/assets/9e0856f3-18b7-4cd4-84bc-3c3646f716b8)

import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af

![image](https://github.com/user-attachments/assets/ccefdfbb-09dd-41c9-b259-7ecf9590dabe)

sns.boxplot(data=af)

![image](https://github.com/user-attachments/assets/ef240f8c-26cd-43ce-b742-73f685728b97)

sns.scatterplot(data=af)

![image](https://github.com/user-attachments/assets/3011d38c-e44b-4063-82f0-f2716b1f3295)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr

![image](https://github.com/user-attachments/assets/67eaebf9-5b0e-4bb3-b7e0-46fdcd122b69)

Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR

![image](https://github.com/user-attachments/assets/e6438868-3fee-474f-8a19-a0dd39adfc8d)

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR



lower_bound
upper_bound

![image](https://github.com/user-attachments/assets/8941786d-b6ef-425a-be8a-8d2c87fd673d)

outliers=[x for x in age if x<lower_bound or x>upper_bound]
print("Q1:", Q1)
print("Q3:", Q3)
print("IQR:", IQR)
print("Lower bound:", lower_bound)
print("Upper bound:", upper_bound)
print("Outliers:", outliers)

![image](https://github.com/user-attachments/assets/921d0cd9-7a03-4dd1-84b4-10d1499bd6e4)

af=af[((af>=lower_bound)&(af<=upper_bound))]
af

![image](https://github.com/user-attachments/assets/2fbbe296-655b-4b1d-aec6-59fc3fced68a)

af.dropna()


![image](https://github.com/user-attachments/assets/9d0013da-c191-4ccd-8eed-f537b0934b0e)

sns.boxplot(data=af)

![image](https://github.com/user-attachments/assets/f82f718f-4c85-4843-9e0f-1f7f952c0793)

data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print("Mean of the Dataset is", mean)
print("Std. Deviation is", std)


threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
print('outlier in dataset is',outlier)

![image](https://github.com/user-attachments/assets/c66faa35-61ac-4a25-957e-285059636fa9)

from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df

![image](https://github.com/user-attachments/assets/74ba1f07-f479-47ca-b808-dd5704b67626)

z=np.abs(stats.zscore(df))
print(df[z['weight']>3])

![image](https://github.com/user-attachments/assets/ec7dd224-c54f-4d9c-a72e-1e120246321b)


val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]

out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out

op=d_o(val)

op


![image](https://github.com/user-attachments/assets/c85006d3-e0dc-40e7-8116-2d59eb138b6f)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
