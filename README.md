# Sales-performance-analysis
pip install pandas matplotlib seaborn
# Importing libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

# Simulating sales data (replace this with actual file read if needed)
np.random.seed(42)

# Generating synthetic sales data
data = {
    "Order_ID": [f"ORD{1000 + i}" for i in range(1, 101)],
    "Date": pd.date_range(start="2023-01-01", periods=100, freq="D"),
    "Product": np.random.choice(["Product A", "Product B", "Product C", "Product D"], size=100),
    "Region": np.random.choice(["North", "South", "East", "West"], size=100),
    "Sales": np.random.randint(100, 1000, size=100),
    "Units_Sold": np.random.randint(1, 10, size=100)
}

sales_data = pd.DataFrame(data)

# Displaying the first few rows
sales_data.head()
# Check for missing values
sales_data.isnull().sum()

# Convert 'Date' to datetime
sales_data['Date'] = pd.to_datetime(sales_data['Date'])

# Check data types
sales_data.dtypes
# Calculate total sales per day
sales_by_date = sales_data.groupby("Date")["Sales"].sum()

# Plot total sales over time
plt.figure(figsize=(14, 7))
plt.plot(sales_by_date.index, sales_by_date.values, color="blue", label="Sales")
plt.title("Total Sales Over Time")
plt.xlabel("Date")
plt.ylabel("Sales ($)")
plt.grid(True)
plt.legend()
plt.show()
# Calculate total sales by region
sales_by_region = sales_data.groupby("Region")["Sales"].sum()

# Plot sales by region
plt.figure(figsize=(8, 6))
sns.barplot(x=sales_by_region.index, y=sales_by_region.values, palette="Set2")
plt.title("Sales Performance by Region")
plt.xlabel("Region")
plt.ylabel("Sales ($)")
plt.grid(True)
plt.show()
# Calculate total sales by product
sales_by_product = sales_data.groupby("Product")["Sales"].sum()

# Plot sales by product
plt.figure(figsize=(8, 6))
sns.barplot(x=sales_by_product.index, y=sales_by_product.values, palette="coolwarm")
plt.title("Sales Performance by Product")
plt.xlabel("Product")
plt.ylabel("Sales ($)")
plt.grid(True)
plt.show()
# Get top 5 products by total sales
top_5_products = sales_by_product.sort_values(ascending=False).head(5)

# Plot top 5 products
plt.figure(figsize=(8, 6))
sns.barplot(x=top_5_products.index, y=top_5_products.values, palette="Blues_d")
plt.title("Top 5 Products by Sales")
plt.xlabel("Product")
plt.ylabel("Sales ($)")
plt.grid(True)
plt.show()
# Resample data to get monthly sales
monthly_sales = sales_data.resample('M', on='Date')['Sales'].sum()

# Plot monthly sales performance
plt.figure(figsize=(14, 7))
monthly_sales.plot(kind='line', color="green", label="Monthly Sales")
plt.title("Sales Performance Over Time (Monthly)")
plt.xlabel("Month")
plt.ylabel("Sales ($)")
plt.grid(True)
plt.legend()
plt.show()
