# 📊 E-commerce Sales Analysis

This project provides an exploratory data analysis (EDA) of an e-commerce dataset using **Python**, **Pandas**, and **Plotly**.  
The goal is to analyze sales trends, category performance, and extract business insights using visualizations.

## 📁 Dataset Used
- **Sample - Superstore.csv**
- Contains transactional data with fields like `Order Date`, `Ship Date`, `Sales`, `Category`, `Sub-Category`, and `Region`.

## 📝 Analysis Highlights
- Data Cleaning and Date Conversion  
- Descriptive Statistics and Data Overview  
- Creation of Time-Based Features (Month, Year, Weekday)  
- Monthly Sales Trend Analysis  
- Sales Analysis by Product Category  
- Correlation Heatmap  

## 🛠️ Technologies & Libraries Used
- Python 3.x  
- Pandas  
- Plotly  
- Seaborn (for correlation heatmaps)  
- Jupyter Notebook  

## 📊 Sample Code Snippets

```python
# Importing Libraries
import pandas as pd
import plotly.express as px
import plotly.io as pio

pio.templates.default = "plotly_white"

# Load Data
data = pd.read_csv("Sample - Superstore.csv", encoding='latin-1')

# Data Cleaning
data['Order Date'] = pd.to_datetime(data['Order Date'])
data['Ship Date'] = pd.to_datetime(data['Ship Date'])

# Feature Engineering
data['Month'] = data['Order Date'].dt.to_period('M')
data['Weekday'] = data['Order Date'].dt.day_name()

# Monthly Sales Analysis
monthly_sales = data.groupby('Month')['Sales'].sum().reset_index()

fig = px.line(monthly_sales, x='Month', y='Sales', title='Monthly Sales Trend')
fig.show()
```

## 💻 How to Run
1. Clone the repository  
2. Place `Sample - Superstore.csv` in the project folder  
3. Open the Jupyter Notebook and execute the cells  
4. Explore insights through interactive charts  

## 📄 License
This project is open-source under the [MIT License](LICENSE).

## 👤 Author
- [Your Name]



