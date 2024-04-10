
 #Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings 
warnings.filterwarnings('ignore')
df=pd.read_csv(r"C:\Users\vinit\Downloads\hotel_bookings 2.csv")
df
df.head()
df.tail()
df.columns
df.shape()
df.info()
df.describe(include = "object")
for col in df.describe(include = 'object').columns:
    print(col)
    print(df[col].unique())
    print('-'*50)
df.isnull().sum()
df.drop(['company' , 'agent'] ,axis = 1 , inplace = True)
df.dropna(inplace = True)
df.describe()
df = df[df['adr']<5000]


#data analysis and visualization
cancelled_perc = df['is_canceled'].value_counts(normalize = True)
print(cancelled_perc)
plt.figure(figsize = (5,4))
plt.title('Reservation status count')
plt.bar(['Not canceled','canceled'], df['is_canceled'].value_counts(), edgecolor = 'k', width = 0.7)
plt.show()
resort_hotel = df[df['hotel'] == 'Resort Hotel']
resort_hotel['is_canceled'].value_counts(normalize = True)
city_hotel = df[df['hotel'] == 'City Hotel']
city_hotel['is_canceled'].value_counts(normalize = True)
resort_hotel = resort_hotel.groupby('reservation_status_date')[['adr']].mean()
city_hotel = city_hotel.groupby('reservation_status_date')[['adr']].mean()
plt.figure(figsize = (20,8))
plt.title('Average Daily Rate in City and Resort Hotel', fontsize = 30)
plt.plot(resort_hotel.index, resort_hotel['adr'], label = 'Resort Hotel')
plt.plot(city_hotel.index, city_hotel['adr'], label = 'City Hotel')
plt.show()
df['month'] = df['reservation_status_date'].dt.month
plt.figure(figsize = (16,8))
ax1 = sns.countplot(x = 'month' , hue = 'is_canceled' , data = df)
plt.figure(figsize = (15,8))
plt.title('ADR per month' , fontsize = 30)
sns.barplot('month' , 'adr' , data = df[df['is_canceled'] == 1].groupby('month')[['adr']].sum().reset_index())
plt.show()
cancelled_data = df[df['is_canceled'] == 1]
top_10_country = cancelled_data['country'].value_counts()[:10]
plt.figure(figsize = (8,8))
plt.title('Top 10 countries with reservation canceled')
plt.pie(top_10_country,autopct = '%2f', labels = top_10_country.index)
plt.show()
df['market_segment'].value_counts()
df['market_segment'].value_counts(normalized = True)
cancelled_data['market_segment'].value_counts(normalize = True)


1. ![h1](https://github.com/Vini28122001/Data-Analysis-Hotel-Booking-/assets/149174627/8ef389c2-935e-4828-850f-a5b0d1cffce6)
2. 
3. ![h2](https://github.com/Vini28122001/Data-Analysis-Hotel-Booking-/assets/149174627/404ff009-dfb1-4589-8bc4-acfe5b3a0ca6)
4. 
5. ![h3](https://github.com/Vini28122001/Data-Analysis-Hotel-Booking-/assets/149174627/b4ee97a7-bda0-47e9-945c-2faef782cc6c)
