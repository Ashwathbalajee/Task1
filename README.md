# LetsGrowMore Internship: Data Science
# Intermediate level - Task 2: Exploratory Data Analysis on Dataset Terrorism
*submitted by* **Ashwath B**


---
Description

As a security/defense analyst, try to find out the hot zone of terrorism.

# Import all Libraries

import io
import numpy as np
import pandas as pd
import seaborn as sns
from sklearn import tree
from google.colab import files
import matplotlib.pyplot as plt

%matplotlib inline

# Read the Dataset 


data = pd.read_csv("globalterrorismdb_0718dist.csv" ,encoding='iso-8859-1')
data.head()

data.shape

data.rename(columns={'eventid':'Event_ID','iyear':'Year','imonth':'Month','iday':'Day','country_txt':'Country','provstate':'state'
                             ,'region_txt':'Region','attacktype1_txt':'AttackType','target1':'Target','nkill':'Killed',
                             'nwound':'Wounded','summary':'Summary','gname':'Group','targtype1_txt':'Target_type','weaptype1_txt':'Weapon_type',
                             'motive':'Motive','success':'Success'},inplace=True)
data

data.isnull().sum()

dup = data[data.duplicated()]
print(dup)

data = data[['Event_ID','Year','Month','Day','Country','Region','region','state','latitude','longitude','Success','AttackType','attacktype1'
               ,'Target_type','targtype1','Target','natlty1_txt','Killed','Wounded','Motive','city','Weapon_type','Group']]
data

data.describe()

# Summary of the Dataset

data.info()

data['Year'].value_counts()

data['Year'].unique()

data['Country'].value_counts()

data['Country'].unique()

data['Region'].value_counts()

data['city'].value_counts()

data.corr()

# Data visualization

fig,axes = plt.subplots(1,1,figsize=(15,15))
sns.heatmap(data.corr(), annot =True)
plt.show()

plt.figure(figsize=(15,8))
sns.countplot(data = data, x = 'Year',palette='Set1')
plt.xticks(rotation=90)
plt.xlabel("Year",size=20)
plt.ylabel("Count",size=20)
plt.show()

sns.countplot(data = data, x='Region')
plt.xticks(size = 16,rotation=90)
plt.xlabel("REGION",size=20)
plt.ylabel("COUNT",size=20)
plt.show()

plt.figure(figsize=(15,9))
x = data['Country'].value_counts().index[:5]
y = data['Country'].value_counts().values[:5]
sns.barplot(x,y,palette='deep')
plt.title(' Top 5 Countries Affected By Terrorism',size=20)
plt.xlabel('Countries',size=15)
plt.ylabel('Count',size=15)
plt.xticks(size=13,rotation= 90)
plt.show()

plt.figure(figsize=(15,9))
x =data['city'].value_counts().index[1:10]
y =data['city'].value_counts().values[1:10]
sns.barplot(x,y,palette='Blues_r')
plt.title('Top 10 Cities Affected By Terrorism',size=20)
plt.xlabel('Cities',size=15)
plt.ylabel('Count',size=15)
plt.xticks(size=13,rotation= 90)
plt.show()

plt.figure(figsize=(10,10))
data['AttackType'].value_counts().plot.pie(autopct ="%1.1f%%")
plt.show()

data['Group'].value_counts().to_frame().drop('Unknown').head(10).plot(kind='bar',color='brown',figsize=(20,10))
plt.title("Top 10 terrorist group attack",fontsize=20)
plt.xlabel("terrorist group name",fontsize=15)
plt.ylabel("Attack number",fontsize=15)
plt.show()

# Target type

Target = data['Target_type'].value_counts().nlargest(n=15)
Target

plt.figure(figsize= (18,10))
sns.barplot(x = Target.index , y = Target.values)
plt.title('Most Frequent Target Type')
plt.xlabel('Target Type')
plt.ylabel('Attacks count')
plt.xticks(rotation = 90)
plt.show()

# Thank you


---


