import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
df=pd.read_excel('/kaggle/input/hbl-dummy/Enhanced_Dummy_HBL_Data.xlsx')
df
account_type_counts = df['Account Type'].value_counts()
plt.figure(figsize=(8, 8))  
plt.pie(
    account_type_counts, 
    labels=account_type_counts.index, 
    autopct='%1.1f%%', 
    startangle=140,     
    colors=sns.color_palette('pastel')  
)
plt.title('Distribution of Account Types')
plt.show()
grouped_data = df.groupby(['Region', 'Transaction To'])['Credit'].sum().reset_index()
top_banks_per_region = (
    grouped_data.sort_values(['Region', 'Credit'], ascending=[True, False])
    .groupby('Region')
    .head(5)
)

plt.figure(figsize=(12, 8))
sns.barplot(
    data=top_banks_per_region,
    x='Region',
    y='Credit',
    hue='Transaction To',
    palette='pastel'
)
plt.title('Top 5 Beneficiary Banks with Highest Credit Transactions per Region')
plt.xlabel('Region')
plt.ylabel('Total Credit')
plt.legend(title='Beneficiary Bank', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()
transaction_data = df.groupby('Region')[['Credit', 'Debit']].sum()
plt.figure(figsize=(10, 6))
sns.heatmap(
    transaction_data,
    annot=True,          
    fmt='.2f',           
    cmap='YlGnBu',       
    cbar_kws={'label': 'Transaction Amount'} 
)plt.title('Transaction Intensity by Region')
plt.xlabel('Transaction Type')
plt.ylabel('Region')
plt.tight_layout()
plt.show()
def calculate_z_scores(series):
    return (series - series.mean()) / series.std()
df['Credit_Z'] = calculate_z_scores(df['Credit'])
df['Debit_Z'] = calculate_z_scores(df['Debit'])
credit_outliers = df[np.abs(df['Credit_Z']) > 3]
debit_outliers = df[np.abs(df['Debit_Z']) > 3]
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x='Credit', y='Debit', label='Normal Data', color='blue')
sns.scatterplot(data=credit_outliers, x='Credit', y='Debit', label='Credit Outliers', color='red')
sns.scatterplot(data=debit_outliers, x='Credit', y='Debit', label='Debit Outliers', color='green')
plt.title('Scatter Plot with Anomalies in Credit and Debit')
plt.xlabel('Credit')
plt.ylabel('Debit')
plt.legend()
plt.tight_layout()
plt.show()
plt.figure(figsize=(14, 6))
plt.subplot(1, 2, 1)
sns.boxplot(data=df, x='Account Type', y='Credit', palette='pastel')
plt.title('Distribution of Credit Transactions by Account Type')
plt.xlabel('Account Type')
plt.ylabel('Credit Amount')
plt.subplot(1, 2, 2)
sns.boxplot(data=df, x='Account Type', y='Debit', palette='muted')
plt.title('Distribution of Debit Transactions by Account Type')
plt.xlabel('Account Type')
plt.ylabel('Debit Amount')
plt.tight_layout()
plt.show()
region_grouped = df.groupby('Region')[['Credit', 'Debit']].sum()
region_grouped.plot(kind='bar', figsize=(12, 6), color=['blue', 'orange'])
plt.title('Credit and Debit Transaction Trends by Region')
plt.xlabel('Region')
plt.ylabel('Total Transaction Amount')
plt.xticks(rotation=45)
plt.legend(['Credit', 'Debit'])
plt.tight_layout()
plt.show()
account_type_grouped = df.groupby('Account Type')[['Credit', 'Debit']].sum()
plt.figure(figsize=(12, 6))
account_type_grouped.plot(
    kind='bar', 
    stacked=True, 
    figsize=(12, 6), 
    color=['blue', 'orange'], 
    edgecolor='black'
)
plt.title('Total Credit and Debit Amounts by Account Type')
plt.xlabel('Account Type')
plt.ylabel('Transaction Amount')
plt.xticks(rotation=45)
plt.legend(['Credit', 'Debit'], title='Transaction Type')
plt.tight_layout()
plt.show()
grouped_data = df.groupby(['Region', 'Account Type'])[['Credit', 'Debit']].sum().reset_index()
fig = px.treemap(
    grouped_data, 
    path=['Region', 'Account Type'], 
    values='Credit',  
    color='Credit',  
    color_continuous_scale='YlGnBu',  
    title="Treemap of Credit Transactions by Region and Account Type"
)
fig.show()
        
