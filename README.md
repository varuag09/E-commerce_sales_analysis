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
- Python 
- Pandas  
- Plotly  
- Seaborn (for correlation heatmaps)  
- Jupyter Notebook  

## 📊 Importing necessary Libraries

```python
# Importing Libraries
import pandas as pd
import plotly.express as px
import plotly.graph_objects as go
import plotly.io as pio
import plotly.colors as colors
pio.templates.default="plotly_white"
```

## Load Data and view
```python
data = pd.read_csv("Sample - Superstore.csv", encoding='latin-1')
data.head()
```

## Converting Data Columns
```python
data['Order Date'] = pd.to_datetime(data['Order Date'])
data['Ship Date'] = pd.to_datetime(data['Ship Date'])

data.info()
```

## Adding New Data-Based Columns
```python
data['Order Month']=data['Order Date'].dt.month
data['Order Year']=data['Order Date'].dt.year
data['Order Date of Week']=data['Order Date'].dt.dayofweek
```

## Monthly Sales Analysis

```python
sales_by_month = data.groupby('Order Month')['Sales'].sum().reset_index()
fig = px.line(sales_by_month,
             x='Order Month',
             y='Sales',
             title='Monthly Sales Analysis')
fig.show()
```
![E-commerce](https://github.com/varuag09/E-commerce_sales_analysis/blob/main/Monthly_sales_analysis.png)

## Sales Analysis by Category
```python
sales_by_category = data.groupby('Category')['Sales'].sum().reset_index()

fig = px.pie(sales_by_category,
            values='Sales',
            names='Category',
            hole=0.2,
            color_discrete_sequence=px.colors.qualitative.Pastel)

fig.update_traces(textposition='inside', textinfo='percent+label')
fig.update_layout(title_text='Sales Analysis by Category', title_font=dict(size=24))

fig.show()
```
![E-commerce](https://github.com/varuag09/E-commerce_sales_analysis/blob/main/Sales_analysis_category.png)

## Sales Analysis by Sub-Category
```python
sales_by_subcategory = data.groupby('Sub-Category')['Sales'].sum().reset_index()
fig = px.bar(sales_by_subcategory,
            x='Sub-Category',
            y='Sales',
            title='Sales Analysis by Sub-Category')
fig.show()
```
![E-commerce](https://github.com/varuag09/E-commerce_sales_analysis/blob/main/Sales_analysis_Sub_category.png)
## Monthly Profit Analysis
```python
profit_by_month = data.groupby('Order Month')['Profit'].sum().reset_index()
fig = px.line(profit_by_month,
             x='Order Month',
             y='Profit',
             title='Monthly Profit Analysis')
fig.show()
```
![E-commerce](https://github.com/varuag09/E-commerce_sales_analysis/blob/main/Monthly_profit_analysis.png)

## Profit Analysis by Category
```python
profit_by_category=data.groupby('Category')['Profit'].sum().reset_index()

fig = px.pie(profit_by_category,
            values='Profit',
            names='Category',
            hole=0.2,
            color_discrete_sequence=px.colors.qualitative.Pastel)

fig.update_traces(textposition='inside', textinfo='percent+label')
fig.update_layout(title_text='Profit Analysis by Category', title_font=dict(size=24))

fig.show()
```
![E-commerce](https://github.com/varuag09/E-commerce_sales_analysis/blob/main/Profit_Analysis_by_category.png)
## Profit Analysis by Sub-Category
```python
profit_by_subcategory = data.groupby('Sub-Category')['Profit'].sum().reset_index()
fig = px.bar(profit_by_subcategory,
             x='Sub-Category',
             y='Profit',
             title='Profit Analysis by Sub-Category')

fig.show()
```
![E-commerce]()
## Sales and Profit Analysis by Customer segment
```python
sales_profit_by_segment = data.groupby('Segment').agg({'Sales':'sum','Profit':'sum'}).reset_index()

color_palette = colors.qualitative.Pastel

fig =go.Figure()
fig.add_trace(go.Bar(x=sales_profit_by_segment['Segment'],
                    y=sales_profit_by_segment['Sales'],
                    name='Sales',
                    marker_color=color_palette[0]))

fig.add_trace(go.Bar(x=sales_profit_by_segment['Segment'],
                    y=sales_profit_by_segment['Profit'],
                    name='Profit',
                    marker_color=color_palette[1]))
fig.update_layout(title='Sales and Profit Analysis by Customer Segment',
                 xaxis_title='Customer Segment', yaxis_title='Amount')

fig.show()
```
![E-commerce]()
## Analyse Sales-to-Profit Ratio
```python
sales_profit_by_segment = data.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()
sales_profit_by_segment['Sales_to_Profit_Ratio'] = sales_profit_by_segment['Sales'] / sales_profit_by_segment['Profit']
print(sales_profit_by_segment[['Segment', 'Sales_to_Profit_Ratio']])
```
![E-commerce]()


## 👤 Author
Gaurav Kumar



