import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Carregar os dados (substituir 'dados.csv' pelo arquivo correto)
df = pd.read_csv('dados.csv')

# Exibir as primeiras linhas do dataset
print(df.head())

# Tratamento de dados
## Remover valores nulos
df.dropna(inplace=True)

## Converter colunas para formatos apropriados (exemplo: datas)
df['data'] = pd.to_datetime(df['data'])

# Análise Exploratória
## Estatísticas básicas
print(df.describe())

## Visualização de distribuição de vendas
plt.figure(figsize=(10,5))
sns.histplot(df['vendas'], bins=30, kde=True)
plt.title('Distribuição das Vendas')
plt.xlabel('Valor das Vendas')
plt.ylabel('Frequência')
plt.show()

# Cálculo de métricas importantes
## Ticket médio
ticket_medio = df['vendas'].mean()
print(f'Ticket Médio: R${ticket_medio:.2f}')

## Taxa de conversão (exemplo genérico, depende dos dados disponíveis)
if 'leads' in df.columns and 'clientes' in df.columns:
    taxa_conversao = (df['clientes'].sum() / df['leads'].sum()) * 100
    print(f'Taxa de Conversão: {taxa_conversao:.2f}%')

# Salvar dados tratados
## Criar um novo arquivo CSV com os dados limpos
df.to_csv('dados_tratados.csv', index=False)
print("Dados tratados salvos com sucesso!")
