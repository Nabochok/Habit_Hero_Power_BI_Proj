# Habit Tracker Analytics Project

This project includes synthetic data generation, database setup, and Power BI analysis for a mobile habit-tracking app with a subscription model.

## Folder Structure

```
/ (root)
├── habit_hero_data/             # Folder containing raw or processed data files
├── BI_Report.pbix               # Power BI report file
├── Create_Insert_Tables.ipynb    # Jupyter notebook to create and insert tables into PostgreSQL
├── Generate_data.ipynb           # Jupyter notebook to generate synthetic data
├── BI_Sheet1_Overview.png        # Screenshot of the Overview page in Power BI
└── BI_Sheet2_FinancialPerfomance.png  # Screenshot of the Financial Performance page in Power BI
```

## Files Description

- **habit_hero_data/**  
  This folder contains any raw data files or processed CSVs used for loading into the database (if applicable).

- **BI_Report.pbix**  
  The Power BI Desktop file that holds the data model, relationships, DAX measures, and all visualizations. Open this file in Power BI to view the interactive dashboard.

- **Create_Insert_Tables.ipynb**  
  A Jupyter notebook that includes Python code for connecting to PostgreSQL, creating the required tables (dim_date, dim_channel, users, transactions, costs, engagement), and inserting the generated data.

- **Generate_data.ipynb**  
  A Jupyter notebook with Python code to generate synthetic data for:
  - Users (100,000 rows with signup dates and acquisition channels)
  - Transactions (subscription and in-app purchase events)
  - Costs (daily marketing costs per channel)
  - Engagement (daily habit logs per user)

- **BI_Sheet1_Overview.png**  
  Screenshot image of the "Overview" page in the Power BI report, showcasing key KPIs and line charts for new users and revenue.

- **BI_Sheet2_FinancialPerfomance.png**  
  Screenshot image of the "Financial Performance" page in the Power BI report, showing financial metrics, waterfall chart, and cumulative revenue vs. cost.

## Overview

1. **Data Generation**  
   - Use `Generate_data.ipynb` to produce synthetic CSVs or directly load data into PostgreSQL.

2. **Database Setup**  
   - Run `Create_Insert_Tables.ipynb` to create tables in PostgreSQL and insert the generated data.
   - The schema includes:
     - `dim_date` (date dimension)
     - `dim_channel` (marketing channel dimension)
     - `users` (user profiles)
     - `transactions` (subscription/in-app purchase records)
     - `costs` (daily marketing spend)
     - `engagement` (daily habit logs)

3. **Power BI Analysis**  
   - Open `BI_Report.pbix` in Power BI Desktop.
   - The data model is configured with relationships:
     - `dim_date[DateID]` → `users[SignupDateID]`
     - `dim_date[DateID]` → `transactions[TransactionDateID]`
     - `dim_date[DateID]` → `costs[DateID]`
     - `dim_date[DateID]` → `engagement[ActivityDateID]`
     - `dim_channel[ChannelID]` → `users[channelID]`
     - `dim_channel[ChannelID]` → `costs[channelID]`
   - Key DAX measures include:
     - **CAC** (Customer Acquisition Cost)
     - **LTV** (Lifetime Value)
     - **ROI** (Return on Investment)
     - **NewUsersByMonth** and **RevenueByMonth**
     - **CumulativeRevenue** and **CumulativeCost**
     - **NetProfitByChannel** (for Waterfall)
     - **RetentionRate_Month1**, **RetentionRate_Month2**, **RetentionRate_Month3**, etc.

4. **Visualizations**  
   - **Overview Page**: KPI cards (Total Users, Total Revenue, CAC, LTV, ROI), line charts for monthly new users and revenue.
   - **Financial Performance Page**: Financial metrics (ARPU, MRR, ROI), waterfall chart for net profit by channel, cumulative revenue vs. cost.
   - **Acquisition Matrix**: Table showing new users, CAC, ROI by channel and month.
   - **Retention Matrix**: Heatmap of retention rates for cohorts across months.


