# house_data-prediction-in-tensorflow
the house data predict the tensorflow package

!pip uninstall tensorflow

!pip install tensorflow==2.10.0

import tensorflow as tf
import numpy as np
import pandas as pd
from pylab import rcParams
import matplotlib.pyplot as plt
import warnings

# Commented out IPython magic to ensure Python compatibility.
# %matplotlib inline
warnings.filterwarnings('ignore')
pd.set_option('display.expand_frame_repr',False)
rcParams['figure.figsize']=16,8

#using the data set
df = pd.read_csv('/content/drive/MyDrive/train/house1.csv')
df.head()

plt.scatter(df['price'],df['sqft_living'])
plt.show()

model=tf.keras.Sequential()
model.add(tf.keras.layers.Dense(1,input_shape=[1]))
model.compile(loss='mean_squared_error',optimizer=tf.keras.optimizers.Adam(0.001))

model.summary()

history=model.fit(df['price'],df['bedrooms'],epochs =300)
plt.plot(history.history['loss'])
plt.show()

df["prediction"]=model.predict(df['price'])

plt.scatter(df['bathrooms'],df['price'])
plt.show

#clean the data
df.isna().sum()

df.info

df.tail()

!pip uninstall tensorflowy

!pip install tensorflow==2.10.0

import tensorflow as tf
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from tensorflow import keras
from tensorflow.keras import layers
import seaborn as sns

df = pd.read_csv('/content/drive/MyDrive/train/house1.csv')
df

df.isna().sum()

df.drop(['waterfront','view','sqft_basement','date'],axis=1,inplace=True)

df

print('training and test datasets:')
train_df=df.sample(frac=0.8,random_state=0)
test_df=df.drop(train_df.index)
print('training data:')
display(train_df.head(10))
print('training data:')
display(test_df.head(2))

print('Pair plot of a train_df:')
sns.pairplot(train_df[['price','bathrooms','bedrooms','yr_built']],diag_kind='kde')
plt.title('pair plot of df_train attributes')

train_stat=train_df.describe()
print('\n')
print('Description about price attribute of a train_df:')
display(train_stat.pop('price'))
train_lables=train_df.pop('price')
test_labels=test_df.pop('price')
print('\n')
print('View test labels:')
display(test_labels)

model=tf.keras.Sequential()
model.add(tf.keras.layers.Dense(1,input_shape=[1]))
model.compile(loss='mse',optimizer=tf.keras.optimizers.Adam(0.01))
print('Summary of a model:')
display(model.summary())

history=model.fit(df['sqft_above'],df['price'],epochs=100)

print('Error and epoch:')
plt.plot(history.history['loss'])
plt.xlabel('epoch')
plt.ylabel('error')
plt.title('error with respect to epochs:')

print('epoch:676/676')
df['Prediction']=model.predict(df['bedrooms'])
plt.scatter(df['bedrooms'],df['price'])
plt.plot(df['bedrooms'], df['Prediction'], color="yellow")
plt.xlabel('bedrooms')
plt.ylabel('price')
plt.show()

plt.plot(df['sqft_above'],df['Prediction'])

from sklearn.metrics import r2_score
v=r2_score(df['yr_built'],df['Prediction'])
print('r2score is',v)
from sklearn.metrics import mean_squared_error
sde=mean_squared_error(df['yr_built'],df['Prediction'])
print('mean sqarued error=',sde)
