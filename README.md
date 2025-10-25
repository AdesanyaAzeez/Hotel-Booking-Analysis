# 🏨 HOTEL BOOKING ANALYSIS

## 📘 Project Overview
This project explores and analyzes the **Hotel Booking Dataset**, which contains booking information for a **City Hotel** and a **Resort Hotel** between 2013 and 2017.    

Through exploratory data analysis (EDA), visualization, and feature-based insights, this project aims to uncover patterns in **booking behavior, arrivals and stays, cancellations, seasonality, guest profiles, revenue performance**,  answer key business questions and help the hotels get insights to make data-driven decisions.

## 🛠️ Tools & Libraries Used

| Category | Tools |
|:--|:--|
| General Language | `Python` |
| Data Processing | `Pandas`, `NumPy` |
| Visualization | `Matplotlib`, `Seaborn`, `Plotly` |
| Development and Reporting | `VSCode`, `Markdown` |
| Version Control and Sharing| `Git`, `GitHub` |


## 📂 Dataset Information

**Data File:** [Hotel Booking Dataset](<Hotel Bookings.csv>)  
**Size:** 119390 rows × 33 columns  
**Scope:** Covers both City and Resort hotels, including details about reservations, arrival dates, lead times, stays, cancellation behavior, revenue, and guest demographics.



## 🧾 Data Dictionary (Key Columns)

| Column | Description |
|:--|:--|
| `hotel` | Type of hotel (`City Hotel` or `Resort Hotel`) |
| `is_canceled` | Whether the booking was canceled (1 = Yes, 0 = No) |
| `lead_time` | Number of days between booking and arrival date |
| `arrival_date_year`, `arrival_date_month`, `arrival_date_day_of_month` | Booking arrival details |
| `stays_in_weekend_nights` | Nights spent during weekends |
| `stays_in_week_nights` | Nights spent during weekdays |
| `adults`, `children`, `babies` | Number of guests per booking |
| `meal` | Type of meal booked (e.g., BB = Bed & Breakfast) |
| `country` | Country of guest origin |
| `market_segment` | How booking was made (e.g., Online TA, Direct) |
| `distribution_channel` | Booking distribution method |
| `is_repeated_guest` | Whether the guest has booked before (1 = Yes, 0 = No) |
| `previous_cancellations` | Number of previous cancellations |
| `reserved_room_type`, `assigned_room_type` | Room types booked and assigned |
| `deposit_type` | Type of deposit required (`No Deposit`, `Non Refund`, etc.) |
| `agent`, `company` | IDs of travel agents or companies |
| `adr` | Average Daily Rate (total booking cost / total nights) |
| `reservation_status` | Final booking status (`Check-Out`, `Canceled`, `No-Show`) |
| `total_of_special_requests` | Number of special requests made |
| `customer_type` | Type of customer (`Transient`, `Contract`, `Group`, `Transient-Party`) |



## 🧹 Data Cleaning & Preparations

1. **Handled Missing Values and Abbrevated Entries**

   * Replaced nulls in key columns based on context:
     * `Agent` -> *"No agent"*
     * `Company` -> *"Not provided"*
     * `Country` -> *"Not provided"*
     * `Children` -> *0*
   * Replaced abbrevations in key columns for clarity:
     * `BB`: Bed & Breakfast
     * `FB`: Full Board
     * `HB`: Half Board
     * `SC`: Self Catering
     * `TA/TO`: Travel Agent/Tour Operator
     * `GDS`: Global Distribution System

2. **Converted and Adjusted Data Types**

   * Combined arrival columns into a single `arrival_date`.
   * Changed column data types as needed for analysis.

3. **Filtered Unreasonable or Incorrect Records:**

   * Removed bookings with zero guests or negative ADR values.

4. **Created and Derived Columns:**

   * **`Booking Date`** derived using *‘Arrival Date’ - ‘Lead Time’*
   * `total_stay_nights` = `stays_in_weekend_nights + stays_in_week_nights`
   * `total_guests` = `adults + children + babies`
   * `amount` = `adr * total_stay_nights`
   * `revenue` = actualized revenue for valid stays or non-refundable cancellations

5. **Final Data Refinements:**

   * Dropped unnecessary columns.
   * Renamed columns and standardized value names for readability.
   * Checked for and removed duplicates.

All data cleaning steps can be found in the [Data Cleaning & Preparation Notebook](<0_Data_Cleaning_andPreparation.ipynb>). However, some of the transformations were done during the analysis process as needed and are found in other notebooks.
Here are some key code snippets used during data cleaning:

### 🗓️ Creating Arrival Date
```python
htb['arrival_date'] = pd.to_datetime(
    htb['arrival_date_year'].astype(str) + '-' + 
    htb['arrival_date_month'].astype(str) + '-' + 
    htb['arrival_date_day_of_month'].astype(str), 
    format="%Y-%B-%d"
    )
```

### Removing Duplicated Record
```python
# Print no of duplicates before deleting them
print(f'Number of duplicates: {htb.duplicated().sum():,}')

# Remove duplicates from dataframe 'htb'
htb = htb.drop_duplicates()

# Print no of duplicates after deleting them
print(f'Number of duplicates after removal: {htb.duplicated().sum()}')
```
---
## 🎯 Key Analysis Areas

This analysis explored five key areas:

📅 Bookings & Arrivals: Reviews booking volumes, hotel type distribution, cancellations, lead times, and guest origins.

⏰ Time-Based Analysis: Examines monthly and yearly trends, seasonality, and variations in ADR and cancellations over time.

👥 Guest Profile Analysis: Highlights guest composition, customer types, and booking preferences across hotels.

🔗 Booking Channels & Market Segments: Analyzes distribution channels, market segments, and their impact on ADR, lead time, and cancellations.

💰 Revenue & Performance Analysis: Evaluates revenue drivers, ADR behavior, and performance trends across hotels and time periods.

All questions as regards these areas can be found in the [Hotel Booking Questions Notebook](<questions.txt>)

---
## 📊 The Analysis

### 📝 Exploratory Data Analysis - Bookings, Arrivals, Stays

Notebook Link: [EDA - Bookings & Arrivals](<1_EDA-Bookings_Arrivals.ipynb>)

A total of valid 87,299 bookings were recorded, with the City Hotel receiving about ~61% of all reservations. The Resort Hotel accounted for 33,955 bookings. From all bookings, 24,009 were canceled, resulting in an overall cancellation rate of approximately 27.5%.

The Average Lead Time across all bookings was 80 days, with canceled bookings having a significantly higher lead time (106 days) compared to non-canceled ones (70 days), suggesting that bookings with lead time approaching 100 days increases cancellation likelihood.

On an average, each booking has a length of 3 stay nights, with Resort Hotel bookings tending to be longer (4 nights) compared to City Hotel (2 nights).

Most bookings came from Portugal (PRT), far exceeding other countries, suggesting a strong domestic or regional market presence. Additionally, Europe (Portugal, United Kingdom, France, Spain, Germany, Italy, Ireland, Belgium, Netherlands) accounted for the majority of bookings, indicating a strong European customer base.



---

## ✍️ Author

**AbdulAzeez Adesanya**  
Data Analyst<br> 
>📧 [adesanya240@gmail.com](mailto:adesanya240@gmail.com)  
>🌐 [LinkedIn](https://www.linkedin.com/in/abdulazeezadesanya)

---


