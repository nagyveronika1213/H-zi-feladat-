import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
np.random.seed(42)

# Generate sample dataset
n = 1000
data = {
    'Date': pd.date_range(start='2023-01-01', periods=n, freq='D'),
    'Category': np.random.choice(['A', 'B', 'C', 'D'], size=n),
    'Subcategory': np.random.choice(['X', 'Y', 'Z'], size=n),
    'Sales': np.random.uniform(100, 1000, size=n),
    'Quantity': np.random.randint(1, 50, size=n),
    'Discount': np.random.uniform(0, 0.5, size=n)
}
df = pd.DataFrame(data)
df.head()

# Plot Total Sales over Time
df_grouped_sales = df.groupby('Date')['Sales'].sum()
plt.figure(figsize=(10, 6))
plt.plot(df_grouped_sales.index, df_grouped_sales.values)
plt.title('Total Sales Over Time')
plt.xlabel('Date')
plt.ylabel('Sales')
plt.grid(True)
plt.show()

# Create a pivot table and visualize sales by category and subcategory
pivot_table = df.pivot_table(values='Sales', index='Category', columns='Subcategory', aggfunc='sum')
plt.figure(figsize=(10, 6))
sns.heatmap(pivot_table, annot=True, cmap='Blues')
plt.title('Sales by Category and Subcategory')
plt.show()

# Bar chart for total quantity sold by category
quantity_by_category = df.groupby('Category')['Quantity'].sum()
plt.figure(figsize=(8, 6))
quantity_by_category.plot(kind='bar', color='skyblue')
plt.title('Total Quantity Sold by Category')
plt.xlabel('Category')
plt.ylabel('Total Quantity Sold')
plt.show()

# Scatter plot to show Sales vs Quantity with Discount as color
plt.figure(figsize=(10, 6))
scatter = plt.scatter(df['Sales'], df['Quantity'], c=df['Discount'], cmap='viridis', alpha=0.7)
plt.colorbar(scatter, label='Discount')
plt.title('Sales vs Quantity with Discount')
plt.xlabel('Sales')
plt.ylabel('Quantity')
plt.show()

# Bar chart for average discount by category
avg_discount_by_category = df.groupby('Category')['Discount'].mean()
plt.figure(figsize=(8, 6))
avg_discount_by_category.plot(kind='bar', color='lightgreen')
plt.title('Average Discount by Category')
plt.xlabel('Category')
plt.ylabel('Average Discount')
plt.show()

