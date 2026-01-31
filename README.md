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

# Coding and Output:
```
import pandas as pd
from scipy import stats
df = pd.read_csv("Data_set.csv")
df
```
<img width="1337" height="667" alt="image" src="https://github.com/user-attachments/assets/db9e3bb3-d51e-4491-8cf7-5e7b56c2967b" />

```
df.head()
```
<img width="1335" height="339" alt="image" src="https://github.com/user-attachments/assets/26db231e-b6de-42ac-b6c4-e126868d8558" />

```
df.isnull().sum()
```
<img width="677" height="413" alt="image" src="https://github.com/user-attachments/assets/5d1701c6-c3d0-40d6-ae3c-e8c31e2fc196" />
```
df_clean = df.dropna()
df_clean.isnull().sum()
```
<img width="468" height="420" alt="image" src="https://github.com/user-attachments/assets/eafce950-0edf-4115-bcad-938ef1af2ebc" />

```
df_clean.to_csv("Data_set_clean.csv", index=False)
num_cols = df_clean.select_dtypes(include='number')
Q1 = num_cols.quantile(0.25)
Q3 = num_cols.quantile(0.75)
IQR = Q3 - Q1
df_iqr = df_clean[
    ~((num_cols < (Q1 - 1.5 * IQR)) |
      (num_cols > (Q3 + 1.5 * IQR))).any(axis=1)
]
df_iqr
```
<img width="1342" height="675" alt="image" src="https://github.com/user-attachments/assets/53b8399a-a19d-4e8b-a584-6dc16a7f7f95" />

```
df_iqr.to_csv("Data_set_iqr.csv", index=False)
z_scores = stats.zscore(num_cols)
z_scores
```
<img width="602" height="605" alt="image" src="https://github.com/user-attachments/assets/d3c0c59a-32c9-4dba-96a1-ca1c0c6fcef4" />

<img width="617" height="615" alt="image" src="https://github.com/user-attachments/assets/56f9586e-22d2-4e4a-bbe2-f6bbde1e76c6" />

```
df_zscore = df_clean[(abs(z_scores) < 3).all(axis=1)]
df_zscore.to_csv("Data_set_zscore.csv", index=False)
df_zscore
```
<img width="1344" height="664" alt="image" src="https://github.com/user-attachments/assets/e75baae6-b06c-469d-867c-85e2db3190ca" />

ir = pd.read_csv('iris.csv')
ir
```
<img width="665" height="517" alt="image" src="https://github.com/user-attachments/assets/961691bb-50a3-4662-84ec-6b70055964e7" />

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
<img width="716" height="575" alt="image" src="https://github.com/user-attachments/assets/310bebb4-99ff-483b-906a-97deff9f86ef" />

```
q1 = ir.sepal_width.quantile(0.25)
q3 = ir.sepal_width.quantile(0.75)
iqr = q3 - q1
print(iqr)
```
<img width="117" height="42" alt="image" src="https://github.com/user-attachments/assets/20b2308c-233a-4343-8b45-56a851cc8bfb" />

```
rid = ir[((ir.sepal_width<(q1-1.5*iqr)) |(ir.sepal_width>(q3+1.5*iqr)))]
rid['sepal_width']
```
<img width="258" height="268" alt="image" src="https://github.com/user-attachments/assets/02a9a853-a7c0-469a-b4a4-46938d6cb35d" />

```
delid = ir[~((ir.sepal_width<(q1-1.5*iqr)) |(ir.sepal_width>(q3+1.5*iqr)))]
delid
```
<img width="727" height="527" alt="image" src="https://github.com/user-attachments/assets/974f0ed1-a01c-48af-8a16-e93de5684349" />

```
sns.boxplot(x='sepal_width',data=delid)
```
<img width="717" height="575" alt="image" src="https://github.com/user-attachments/assets/385d6d00-add6-4f8b-b9a1-b8cb5fdcb0d5" />

```
import numpy as np
import scipy.stats as stats
z = np.abs(stats.zscore(ir['sepal_width']))
z
```
<img width="757" height="660" alt="image" src="https://github.com/user-attachments/assets/eaf09dc4-f56b-40e5-bf4b-3b770f5db8fd" />

```
df1 = ir[z<3]
df1
```
<img width="727" height="507" alt="image" src="https://github.com/user-attachments/assets/cf5c311d-f11c-40e1-9192-13194cf26af4" />


# Result
          <<include your Result here>>
