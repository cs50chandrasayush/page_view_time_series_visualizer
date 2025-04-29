# page_view_time_series_visualizer

This project is part of the **freeCodeCamp Data Analysis with Python Certification**. It involves cleaning and visualizing time series data from the freeCodeCamp forum to better understand website traffic over time.

## 🧾 Project Objective

- Clean the data by removing outliers.
- Create three types of visualizations:
  - Line Plot (to observe trends over time)
  - Bar Plot (to compare average monthly page views year-wise)
  - Box Plot (to analyze distributions by year and month)

## 🧰 Technologies Used

- Python 🐍
- Pandas 📊
- Matplotlib 📉
- Seaborn 🎨
- NumPy 🔢

## ⚙️ How It Works

### 1. Data Cleaning

```python
df = pd.read_csv("fcc-forum-pageviews.csv")
df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)

# Remove outliers (values outside 2.5th and 97.5th percentiles)
lower_limit = df['value'].quantile(0.025)
upper_limit = df['value'].quantile(0.975)
df = df[(df['value'] > lower_limit) & (df['value'] < upper_limit)]
2. Line Plot (draw_line_plot())
Shows page views from May 2016 to December 2019.

python
Copy
Edit
ax.plot(df.index, df['value'], color='blue')
📌 X-axis: Date

📌 Y-axis: Page views

📌 File: line_plot.png

3. Bar Plot (draw_bar_plot())
Displays average page views for each month, grouped by year.

python
Copy
Edit
df_grouped = df.groupby(['year', 'month'])['value'].mean().unstack()
df_grouped.plot(kind='bar')
🟦 Bars grouped by year

🌕 Each bar represents a month's average

📌 File: bar_plot.png

4. Box Plot (draw_box_plot())
Used to analyze:

📈 Year-wise trends

🍂 Month-wise seasonality

python
Copy
Edit
sns.boxplot(x='year', y='value', data=df_box)   # Year-wise
sns.boxplot(x='month', y='value', data=df_box)  # Month-wise
📌 File: box_plot.png

📂 Dataset
File: fcc-forum-pageviews.csv

Contains: date, value (daily page views)
