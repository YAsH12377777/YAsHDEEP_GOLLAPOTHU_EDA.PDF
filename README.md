import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the datasets
customers = pd.read_csv('Customers.csv')
products = pd.read_csv('Products.csv')
transactions = pd.read_csv('Transactions.csv')

# Check basic info about each dataframe
print(customers.info())
print(products.info())
print(transactions.info())

# Data Cleaning
# Check for missing values
print(customers.isnull().sum())
print(products.isnull().sum())
print(transactions.isnull().sum())

# Handle missing data (if needed)
# customers.fillna('Unknown', inplace=True)  # Example for filling missing names
# transactions.dropna(subset=['CustomerID', 'ProductID'], inplace=True)  # Drop rows with missing IDs

# Convert date columns to datetime
customers['SignupDate'] = pd.to_datetime(customers['SignupDate'])
transactions['TransactionDate'] = pd.to_datetime(transactions['TransactionDate'])

# Summary statistics
print(customers.describe())
print(products.describe())
print(transactions.describe())

# Visualizations
# Transaction Value Distribution
sns.histplot(transactions['TotalValue'], kde=True)
plt.title('Distribution of Total Transaction Value')
plt.show()

# Product Price Distribution
sns.histplot(products['Price'], kde=True)
plt.title('Distribution of Product Prices')
plt.show()

# Transaction Trends Over Time
transactions.groupby('TransactionDate')['TotalValue'].sum().plot()
plt.title('Total Sales Over Time')
plt.xlabel('Date')
plt.ylabel('Total Sales')
plt.show()

# Product Category Distribution
sns.countplot(data=products, x='Category')
plt.title('Product Category Distribution')
plt.show()

# Insights - Generate from EDA findings
# Insight 1: The highest product price is $[value] with a significant skew towards lower prices.
# Insight 2: Transactions peak during specific months or seasons, indicating trends in customer purchasing behavior.
# Insight 3: Most customers are from the [Region], which indicates market dominance in that region.
# Insight 4: Customers signing up during specific months tend to generate more transactions.
# Insight 5: The average total value of a transaction is higher for [Product Category], suggesting premium products are in demand.
