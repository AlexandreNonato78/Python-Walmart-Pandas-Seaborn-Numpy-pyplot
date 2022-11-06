# Python-Walmart-Pandas-Seaborn-Numpy-pyplot

#Importar todas as bibliotecas que podem ser usadas import numpy as np import pandas as pd import matplotlib.pyplot as plt import seaborn as sns

from datetime import date, datetime

#Importar os dados e Mostrar as informações gerais do arquivo df = pd.read_csv('/content/sample_data/Walmart.csv', sep = ',') df.info()

#Checar os dados df.shape df.head()

#Renomear as colunas df.rename(columns = { 'Store':'Loja', 'Date':'Data', 'Weekly_Sales':'Vendas_na_Semana', 'Holiday_Flag':'Semana_com_Feriado', 'Temperature':'Temperatura', 'Fuel_Price':'Preco_Combustivel', 'Unemployment':'Desemprego' }, inplace = True) df

df['Data'] = pd.to_datetime(df['Data'], format = '%d-%m-%Y') df['Ano'] = df['Data'].dt.year df['Mês'] = df['Data'].dt.month df['Semana'] = df['Data'].dt.isocalendar().week df.head()

#Relação entre vendas e períodos semanais

plt.figure(figsize=(18,6)) sns.lineplot(data=df, x='Data', y='Vendas_na_Semana') plt.title('Vendas por semana - Média') plt.show()

df.describe(percentiles = [0.8, 0.9, 0.95, 0.99])

df.groupby(by='Loja').mean().sort_values(by='Vendas_na_Semana', ascending = False).head()

sns.histplot(data=df[df.Loja.isin([20,4,14,13,2])], x='Vendas_na_Semana', hue='Loja', palette='Blues')

#Preço médio de venda semanal por loja
