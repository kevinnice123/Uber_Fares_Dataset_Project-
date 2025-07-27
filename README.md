# 🚕 Uber_Fares_Dataset_Project-

## 👤 Project By

*Name:* Niyomugabo Nice kevin
*Student ID:* 26708 
*Course:* Introduction to Big Data

---

## 📘 About This Project

In this project, I worked with a real-world dataset from *Uber rides* to understand how prices change based on distance, time, and location. I used *Python* to clean and prepare the data, and then used *Power BI* to build a visual dashboard to help people see the patterns and trends in Uber fares.

---

## 📂 Dataset & Tools Used

 *Dataset Source:* [Uber Fares Dataset on Kaggle](https://www.kaggle.com/datasets/yasserh/uber-fares-dataset)
- *Data Cleaning & Processing:* Python (Pandas)
- *Visualization Tool:* Power BI Desktop
- *My Kaggle Notebook:* [View my work on Kaggle](https://www.kaggle.com/code/niyomugabonicekevin/kevin-nice/edit)

---

## 🔍 Project Steps
 Understanding the Data
⿢ Data Transformation
⿣ Building the Dashboard

Using Power BI, I created the following visualizations:

- Fare distribution chart
- Distance vs Fare chart
- Time of day analysis
- Rides per weekday
- Monthly ride count
- Pickup map of NYC

---

## 🧽 For Cleaning Process

```python

# Check for missing values
print(df.isnull().sum())

# Drop rows with missing key values
df.dropna(subset=['pickup_datetime', 'pickup_latitude', 'pickup_longitude',
                  'dropoff_latitude', 'dropoff_longitude', 'fare_amount'], inplace=True)

# Remove rows with invalid fare amounts
df = df[(df['fare_amount'] > 0) & (df['fare_amount'] < 1000)]
# Filter latitude and longitude (NYC bounds as rough check)
df = df[(df['pickup_latitude'].between(40, 42)) & 
        (df['pickup_longitude'].between(-75, -72)) &
        (df['dropoff_latitude'].between(40, 42)) &
        (df['dropoff_longitude'].between(-75, -72))]

print("Shape after cleaning:", df.shape)

```

<img width="533" height="162" alt="output2" src="https://github.com/user-attachments/assets/1f3e46f1-388d-4fa7-a689-96cd7358d198" />

## 🧽 For Analysis Process

```python
from geopy.distance import geodesic

# Convert pickup_datetime to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])

# Extract temporal features
df['hour'] = df['pickup_datetime'].dt.hour
df['day'] = df['pickup_datetime'].dt.day
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.day_name()
df['year'] = df['pickup_datetime'].dt.year

# Peak hours (7-9 AM or 5-7 PM)
df['is_peak'] = df['hour'].apply(lambda x: 1 if 7 <= x <= 9 or 17 <= x <= 19 else 0)

# Calculate distance (in km)
def calculate_distance(row):
    pickup = (row['pickup_latitude'], row['pickup_longitude'])
    dropoff = (row['dropoff_latitude'], row['dropoff_longitude'])
    return geodesic(pickup, dropoff).km

df['distance_km'] = df.apply(calculate_distance, axis=1)
print(df[['fare_amount', 'hour', 'weekday', 'is_peak', 'distance_km']].head())
```

<img width="563" height="125" alt="output3" src="https://github.com/user-attachments/assets/198f63d7-5693-469c-90e6-702603d3a564" />

---

## 📸 Dashboard & Results

### 📷 All Result Images

> Screenshots of key steps and results:

<img width="959" height="503" alt="Dashboard PBI" src="https://github.com/user-attachments/assets/7db76367-3c35-4cdc-b5cd-19482f9752ea" />

---

## 🙋 Contact Me
If you have any suggestions, questions, or feedback:

Email: nicekevinniyomugabo@gmail.com
Phone:+250791369434

---

Thank you for visiting my project! 😊
