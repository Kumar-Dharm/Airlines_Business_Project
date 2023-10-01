# Airlines_Business_Project  
![Airline_project_logo](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/d19f7bcc-6008-45f5-b4cd-fb2c8aad4ad1)  

"ElevateAir: Enhancing Aviation Profitability via Data-Driven Occupancy Optimization"

ElevateAir addresses modern aviation challenges by analyzing our diverse aircraft fleet's occupancy rates. 
Strict regulations, rising costs and market competition compel us to boost profitability. 
Through as an insightful data analysys, we aim to optimize seat occupancy, elevating both passenger experiences and per-seat profits. 
Join us in shaping aviation's future through innovation and data excellence.

## Table of Contents
- [Introduction](#introduction)
- [Installation and Steps Involved](#installation-and-steps-involved)
- [Objectives](#objectives)
- [Schema of Database](#schema-of-database)
- [Preprocessing and Exploration](#preprocessing-and-exploration)
- [Analysis and Insights](#analysis-and-insights)
- [Limitation and Challenges](#limitation-and-challenges)
- [Conclusion](#conclusion)

## Introduction
- Navigating Aviation Challenges: Our aviation fleet thrives on passenger satisfaction. Yet, factors like regulations, costs, and competition challenge profitability.
- Data-Powered Solution: Through precise data analysis, we're optimizing seat occupancy to counter financial pressures and offer exceptional travel.
- Revitalizing Industry: This project not only boosts per-seat profits but also revolutionizes aviation economics, inviting you to shape a sustainable future with us.  

## Installation and Steps Involved
<pre><code>
1. Google Colab Setup:
  Open Google Colab.
  Create a new notebook or import your existing notebook.
  
2. Google Drive Integration:
  Mount Google Drive to access project files: from google.colab import drive and drive.mount('/content/drive').

3. Library Imports:
  ```python
  import sqlite3
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  import seaborn as sns'''

4. Data Loading:
	Load data into Colab environment.
	If using SQLite: conn = sqlite3.connect('your_database.db').

5. Data Exploration:
	Use Pandas for data analysis: df = pd.read_sql_query("SELECT * FROM your_table", conn).

6. Data Visualization:
	Create visualizations using Matplotlib and Seaborn: plt.plot(...), sns.barplot(...), etc.

7. Analysis and Insights:
	Analyze data patterns, trends, and correlations.
	Extract insights from your data exploration.

8. Project Completion:
	To save and download the modified notebook to our local drive.
</code></pre>

## Objectives
*Increase Occupancy Rate:*  
- The primary objective is to raise the occupancy rate. Achieving this will directly enhance the average profit per seat, countering the current challenges.

*Optimize Pricing Strategy:*  
- Develop a dynamic pricing strategy that adapts to market fluctuations and aligns with customer preferences. This will attract and retain customers effectively.

*Elevate Customer Experience:*  
- Prioritize a seamless end-to-end experience for passengers, from booking to arrival. This distinctiveness in a competitive industry will foster customer loyalty.

* The ultimate aim of these objectives is to pinpoint avenues for boosting the occupancy rate on flights with lower performance. 
This targeted effort has the potential to significantly amplify the airline's profitability.

## Schema of Database  
![Schema](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/ac20f5c8-5d6a-497c-9d96-f89b38204c3e)  

## Preprocessing and Exploration

**Null and Noise Handling:** Conducted a thorough assessment to identify and address null values in the dataset. Also, implemented noise reduction techniques to ensure data accuracy.

**Data Type Consistency:** Ensured uniform data types across the dataset. This consistency aids in smooth processing and analysis.

**Table Size and Shape Evaluation:** Assessed the size and shape of each table to comprehend its structure. This step is crucial for understanding the data's composition.
 <pre><code>
import pandas as pd
table_names = ["aircrafts_data", "airports_data", "boarding_passes","bookings", "flights", "seats","ticket_flights","tickets"]

# Loop through the table names and print the head of each table
for table_name in table_names:
    query = f"SELECT * FROM {table_name}"
    df = pd.read_sql_query(query, conn)
    print(f"Table: {table_name}")
    print(df.shape)
    print(df.head())
    print("\n")
</code></pre>
* By executing these preprocessing steps, the dataset was refined, cleaned, and made ready for further analysis, establishing a solid foundation for accurate insights.

## Analysis and Insights
 <pre><code>
**Basic Analysis**
Q1.How many planes have more than 100 seats?
Q2. What are the ranges of different airplane models?
Q3.How the number of tickets booked and total amount earned changes with the time?
Q4.Calculate the average charges for each aircraft with different fare conditions?

**Analysing Occupancy Rate**
Q5. For each aircraft, calculate the total revenue per year and the average revenue per ticket.
Q6. Calculate the average occupancy per aircraft. (occupanct_rate = booked_seat/available_seat)
Q7. Calculate by how much the total annual turnover could increase by giving all aircraft a 10% higher occupancy rate.
</code> </pre>

**Number of Tickets Booked with Time**  
`plt.figure(figsize=(18,6))`  
`x = df3.groupby('date')[['date']].count()`  
`plt.plot(x.index, x['date'], marker='^')`  
`plt.title('Number of tickets booked with time')`  
`plt.xlabel('Date')`  
`plt.ylabel('No of tickets')`  
`plt.grid('b')`  
`plt.show()`

![No_of_ticket_booked_with_time](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/7b3d841b-bd3d-472e-804e-e398b136c61e)
- Ticket bookings exhibited a gradual increase from June 22nd to July 7th, followed by a stable period in July and a notable peak in bookings on a specific day.

**Total Amount Earned with Time**  
`plt.figure(figsize=(18,6))`  
`y = df3.groupby('date')[['total_amount']].sum()`  
`plt.plot(y.index, y['total_amount'], marker='^')`  
`plt.title('Total amount earned with Time')`  
`plt.xlabel('Date')`  
`plt.ylabel('Total amount')`  
`plt.grid('b')`  
`plt.show()`

![Total_amount_earned_with_time](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/11f5beba-2a08-43bc-99c6-53aa26718153)
- Total revenue earned by the company closely mirrors the trend in ticket bookings, indicating a strong correlation between bookings and revenue. 
- Further investigation into the factors behind the peak in bookings is recommended for revenue optimization.

**Airplane Model with Ranges**  
`plt.figure(figsize=(10,5))`  
`ax = sns.barplot(x='model',y='range', data=aircrafts_data, palette = 'Paired')`  
`for i in ax.containers:`  
`    ax.bar_label(i)`  
`plt.title('Airplane Models with their Ranges')`  
`plt.xticks(rotation=45)`  
`plt.show()`

![Airplane_Model_with_Ranges](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/16699b54-d87e-400c-9f63-ef7a6c0d8e0c)
- Created a bar chart to visualize and compare the ranges of different airplanes.
- The "Boeing 777-300" boasts the longest range, covering an impressive distance of 11,100KM, while the "Cessna 208 Caravan" offers the shortest range, with a distance limit of only 1,200KM.

**Aircraft Code vs Average Charges**  
`sns.barplot(data=df4, x=df4['aircraft_code'], y=df4['average'], hue=df4['fare_conditions'])`  
`plt.title('Aircraft code vs Average charges with different Fare conditions')`  

![Aircraft_code_vs_avg_charges](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/ced50ef1-ff60-467e-966a-108f948fcbc7)  
**Fare Types:**
- Business class fares consistently have higher costs compared to economy class fares across all aircraft types.
- Comfort class is only available on the 773 aircraft, while CN1 and CR2 planes offer only economy class fares.
**Price Comparison:**
- Noted a consistent pattern where business class charges consistently exceeded economy class charges across all aircraft.

**Final Results**
![Final_results](https://github.com/Kumar-Dharm/Image_Gallery/assets/132021299/cce11541-b2fa-43cc-8a79-9a8691b00edc)

**Revenue Analysis for Profit Maximization:**
- Examining overall yearly income and average revenue per ticket is crucial for airlines to optimize profitability.
- Insights from these metrics guide decisions on aircraft types, itineraries, pricing optimization, and resource allocation.

**Revenue and Occupancy Impact:**
- Total revenue, average revenue per ticket, and average occupancy per aircraft are critical indicators.
- SU9 aircraft leads in total revenue with lower business and economy class prices.
- CN1 has lower revenue due to offering only economy class at a minimal price.

**Occupancy's Role in Revenue:**
- Average occupancy per aircraft reflects how effectively seats are filled.
- Higher occupancy rates improve revenue, profitability, and operational efficiency.
- Calculated by dividing booked seats by total seats.

## Limitation and Challenges  
- Working with static data poses a limitation for future relevance unless automated with real-time or updated datasets.
- Explored the integration of Google Colab with Google Drive, SQLite, and Pandas, which added a layer of complexity to the project.
- Dealing with extensive datasets requires efficient techniques for extraction and analysis to draw meaningful conclusions.

## Conclusion  
**Revenue Data Analysis for Profitability:**
- Analyzing total yearly revenue, average ticket revenue, and aircraft occupancy is vital for maximizing airline profitability.
- Insights from these metrics guide pricing, route adjustments, and operational improvements.

**Occupancy's Role in Profitability:**
- Greater occupancy rates enhance profitability by maximizing revenue and minimizing vacant seat costs.
- Pricing adjustment based on aircraft condition and facility is crucial for attracting passengers without compromising on quality.

**Balancing Profit and Quality:**
- While boosting occupancy is crucial, maintaining customer satisfaction and safety is equally important.
- Airlines should adopt a data-driven approach to revenue analysis and optimization for sustainable success in a competitive industry.

* These summary points underscore the importance of revenue analysis, the role of occupancy in profitability, and the need to balance profit goals with delivering quality service and safety.

|---------------------------------------------------------------------------------------------------------------------------|
