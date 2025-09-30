## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
df=pd.read_csv("Encoding Data.csv")
df
```


## Output:
<img width="653" height="558" alt="image" src="https://github.com/user-attachments/assets/b36c6cb6-e27e-4d79-9696-63693a5c9002" />



```
 from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
 pm=['Hot','Warm','Cold']
 e1=OrdinalEncoder(categories=[pm])
 e1.fit_transform(df[["ord_2"]])

```


# Output:
<img width="741" height="354" alt="image" src="https://github.com/user-attachments/assets/fa51c9dc-e850-4bbe-9161-807ce8fec3c2" />



```
 df['bo2']=e1.fit_transform(df[["ord_2"]])
 df

```

# Output:
<img width="617" height="517" alt="image" src="https://github.com/user-attachments/assets/7d725117-41e4-452c-b831-c42ceaa013e3" />


```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc

```

# Output:
<img width="578" height="568" alt="image" src="https://github.com/user-attachments/assets/38d16d0b-9cd0-41dc-af4d-b3b59a6f4308" />


```
from sklearn.preprocessing import OneHotEncoder
import pandas as pd

ohe = OneHotEncoder(sparse_output=False)   # use sparse_output instead of sparse
df2 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
df2=pd.concat([df2,enc],axis=1)
df2

```


# Output:
<img width="834" height="648" alt="image" src="https://github.com/user-attachments/assets/69e068a4-b9cc-4163-82b5-548c105b46e3" />


```
pd.get_dummies(df2,columns=["nom_0"])

```

# Output:
<img width="956" height="522" alt="image" src="https://github.com/user-attachments/assets/70f7e054-fd05-441b-84fd-858a696fc143" />


```
!pip install --upgrade category_encoders

```

# Output:
<img width="1275" height="419" alt="image" src="https://github.com/user-attachments/assets/0da225c7-889b-4a49-971e-756d25c6aac8" />


```
from category_encoders import BinaryEncoder
df=pd.read_csv("data.csv")
df

```

# Output:
<img width="772" height="534" alt="image" src="https://github.com/user-attachments/assets/f4404b89-41d7-4817-9fcc-82bdbd81bc45" />



```
be=BinaryEncoder()
 nd=be.fit_transform(df['Ord_2'])
 df

```

# Output:
<img width="866" height="535" alt="image" src="https://github.com/user-attachments/assets/958792d0-5c6f-4cbd-b063-0d757d1a66d9" />



```
 dfb=pd.concat([df,nd],axis=1)
 dfb

```


# Output:
<img width="976" height="538" alt="image" src="https://github.com/user-attachments/assets/c4fe8f76-3211-4426-8f94-3f6a3210bb9b" />



```

from category_encoders import TargetEncoder
te=TargetEncoder()
CC=df.copy()
new=te.fit_transform(X=CC["City"],y=CC["Target"])
CC=pd.concat([CC,new],axis=1)
CC
```


# Output:
<img width="909" height="643" alt="image" src="https://github.com/user-attachments/assets/6aec1076-9910-4213-89b7-f4ea120421af" />




```
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("Data_to_Transform.csv")
df


```


# Output:
<img width="1044" height="650" alt="image" src="https://github.com/user-attachments/assets/d7282ca6-beb1-421c-bf51-d100473db28e" />




```

df.skew()

```


# Output:
<img width="514" height="314" alt="image" src="https://github.com/user-attachments/assets/52ec15b4-f168-46bb-8998-6f9d937ad151" />



```
np.log(df["Highly Positive Skew"])

```


# Output:



```
np.reciprocal(df["Moderate Positive Skew"])

```


# Output:
<img width="700" height="612" alt="image" src="https://github.com/user-attachments/assets/931acd15-12af-40af-9210-d619889d57eb" />



```

np.sqrt(df["Highly Positive Skew"])
```


# Output:
<img width="562" height="628" alt="image" src="https://github.com/user-attachments/assets/fbde6ec6-55cb-456f-a80c-cfd90c4df487" />


```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
df

```


# Output:
<img width="1301" height="631" alt="image" src="https://github.com/user-attachments/assets/8cc305ca-3acb-4b2c-b0ab-9abdbc46dc05" />


```
from scipy import stats

df["Highly Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Highly Negative Skew"])
df.skew()

```


# Output:
<img width="1091" height="451" alt="image" src="https://github.com/user-attachments/assets/6ae91429-0f0b-4fed-9683-e225ab52f40a" />


```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df


```


# Output:
<img width="1128" height="673" alt="image" src="https://github.com/user-attachments/assets/9c290726-79e8-41a6-840f-9bd24e977f4e" />


```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()


```


# Output:
<img width="881" height="654" alt="image" src="https://github.com/user-attachments/assets/ece52944-36cb-4d44-8ab1-2e81a7396aae" />



```
 sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
 plt.show()

```


# Output:
<img width="886" height="626" alt="image" src="https://github.com/user-attachments/assets/6fd973c3-d254-4aae-86a1-19d23b674c2d" />



```

 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
 df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
 sm.qqplot(df["Moderate Negative Skew"],line='45')
 plt.show()


```


# Output:
<img width="829" height="651" alt="image" src="https://github.com/user-attachments/assets/c01684d3-9511-4a35-ab64-09d4a723df8b" />



```
 df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
 sm.qqplot(df["Highly Negative Skew"],line='45')
 plt.show()


```


# Output:
<img width="891" height="641" alt="image" src="https://github.com/user-attachments/assets/c86326d1-5632-47e0-a8a5-59679c290e8e" />



```
 dt=pd.read_csv("titanic_dataset.csv")
 dt


```


# Output:

<img width="1127" height="665" alt="image" src="https://github.com/user-attachments/assets/eaa85224-b21b-4fd9-8444-c45efcfd5e08" />



```
 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
 dt["Age_1"]=qt.fit_transform(dt[["Age"]])
 sm.qqplot(dt['Age'],line='45') 
 plt.show()

```


# Output:

<img width="869" height="664" alt="image" src="https://github.com/user-attachments/assets/a7afa900-7da5-4098-b336-fd6744398d5f" />



```

sm.qqplot(df["Highly Negative Skew_1"],line='45')
plt.show()

```


# Output:

<img width="819" height="608" alt="image" src="https://github.com/user-attachments/assets/c77f26d2-16fc-4782-a2b0-7849d82e4dec" />



# RESULT:
 Thus the given data, Feature Encoding, Transformation process and save the data to a file
 was performed successfully. 

       
