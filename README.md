# TelecomX

![image](https://github.com/user-attachments/assets/63990d32-0a1b-4f0d-b03a-37bde8688784)

# Descrição do Projeto
Este projeto faz parte do **Challenge ONE Data Science da Alura**, focado na análise de dados de uma empresa de telecomunicações para entender e prever a **evasão de clientes (Churn)**. O objetivo é identificar os fatores que levam os clientes a cancelar seus serviços, fornecendo insights acionáveis para a empresa desenvolver estratégias eficazes de retenção.

# 📝 Etapas
- `Etapa 1`: **Extração e Carregamento dos Dados**
  Extração do conjunto de dados de uma fonte JSON e carregamento em um DataFrame pandas para processamento inicial.

  **Métodos utilizados:**
  * `pd.read_json()` para importar o dataset.
  * `pd.DataFrame()` para criar o DataFrame.

  ![image](https://github.com/user-attachments/assets/b4fe4ad6-6447-40b4-8bff-6ba823bcc34c)


- `Etapa 2`: **Normalização e Transformação Inicial**
  Normalização de colunas aninhadas e concatenação com o DataFrame principal para criar uma estrutura de dados plana e unificada.

  **Métodos utilizados:**
  * `pd.json_normalize()` para expandir as colunas JSON aninhadas (`customer`, `phone`, `internet`, `account`).
  * `pd.concat(axis=1)` para unir os DataFrames normalizados.
  * `.drop(columns=[...])` para remover as colunas aninhadas originais.

  ![image](https://github.com/user-attachments/assets/b1749c42-31c5-4605-a415-4b006516dc30)
  
  ![image](https://github.com/user-attachments/assets/ec6a702c-7202-4d0e-aa70-5a5b28ee5362)



- `Etapa 3`: **Tratamento de Dados Faltantes e Inconsistências**
  Identificação e tratamento de valores ausentes e inconsistências nas colunas chave para garantir a qualidade dos dados.

  **Métodos utilizados:**
  * `.isnull().sum()` para verificar valores nulos.
  * `df_final = df_final[df_final['Churn'] != '']` para remover linhas com churn vazio.
  * `.query()` para inspecionar dados específicos.
  * `.loc[idx, "Charges.Total"] = ...` para preencher valores faltantes em `Charges.Total`.
  * `.astype('float64')` para converter o tipo de dados de `Charges.Total`.

  ![image](https://github.com/user-attachments/assets/c7ba3792-3ce8-42c2-a9c0-cfd26f987ed3)
  
  ![image](https://github.com/user-attachments/assets/01773b73-9cf2-4e9d-9828-b980ef08a02c)



- `Etapa 4`: **Criação de Novas Variáveis**
  Criação de uma nova métrica para análise diária dos gastos dos clientes.

  **Métodos utilizados:**
  * Operações aritméticas simples para criar a coluna `Charges.diary` (posteriormente `gastos_diarios`).

  ![image](https://github.com/user-attachments/assets/c8b9298b-2ea3-497e-a566-dc8716eae7dd)


- `Etapa 5`: **Padronização e Renomeação de Colunas**
  Transformação de valores textuais para binários (0 e 1) e renomeação de todas as colunas para o português, visando maior clareza e facilidade de análise.

  **Métodos utilizados:**
  * `.replace({'Yes': 1, 'No': 0})` para mapear valores binários.
  * `.rename(columns={...})` para traduzir e padronizar os nomes das colunas.

  ![image](https://github.com/user-attachments/assets/dc7f9928-9fe4-46e8-971e-5a883c48adc4)

  ![image](https://github.com/user-attachments/assets/7ba103d1-5287-42b4-ad7a-bc2264e78b2d)



- `Etapa 6`: **Análise Descritiva dos Dados**
  Cálculo de métricas estatísticas para colunas numéricas e análise de frequência para colunas categóricas, fornecendo uma visão geral da distribuição dos dados.

  **Métodos utilizados:**
  * `.describe()` para estatísticas descritivas de colunas numéricas.
  * `.value_counts()` para contagem de frequência de categorias.
  * `.value_counts(normalize=True).mul(100)` para calcular porcentagens.

  ![image](https://github.com/user-attachments/assets/725c16fa-238c-452e-967a-6aad114f1389)

  ![image](https://github.com/user-attachments/assets/55ca70cb-f818-4974-8b40-2dcf41fd2f7a)



- `Etapa 7`: **Análise Exploratória do Churn: Variáveis Categóricas**
  Visualização da distribuição do Churn em relação a diferentes variáveis categóricas para identificar perfis de clientes com maior propensão à evasão.

  **Bibliotecas e métodos utilizados:**
  * `matplotlib.pyplot` para plotagem.
  * `seaborn.countplot()` para gráficos de barras agrupados.
  * Ajustes para exibição de números absolutos e porcentagens nas barras.

  ![image](https://github.com/user-attachments/assets/74cc5f0a-ad7f-497f-90df-79a3ae96ebb2)


  ---
  ### Gráfico de Distribuição de Churn
  * **Tipo:** Gráfico de Colunas
  * **Objetivo:** Visualizar a proporção de clientes que cancelaram e os que não cancelaram o serviço.

  ![image](https://github.com/user-attachments/assets/984073f9-b497-4a6c-8798-136c58a285a1)


  ---
  ### Gráficos de Churn por Variáveis Categóricas (Exemplos)
  * **Tipo:** Gráficos de Barras Verticais Agrupadas
  * **Objetivo:** Comparar as taxas de churn entre diferentes categorias (gênero, tipo de contrato, serviço de internet, método de pagamento, etc.).

  ![image](https://github.com/user-attachments/assets/3dcf8f8c-d1d5-48ab-8447-b1b91388ea72)


- `Etapa 8`: **Análise Exploratória do Churn: Variáveis Numéricas**
  Exploração da distribuição de variáveis numéricas (`meses_de_servico`, `gastos_mensais`, `gastos_totais`, `gastos_diarios`) em relação ao churn, utilizando histogramas e gráficos de densidade para identificar padrões.

  **Bibliotecas e métodos utilizados:**
  * `seaborn.histplot()` para histogramas.
  * `seaborn.kdeplot()` para gráficos de densidade (KDE).
  * Parâmetros `hue`, `multiple='stack'` e `fill=True` para comparação entre grupos.
 
  ![image](https://github.com/user-attachments/assets/92868e13-8894-4266-aea1-3f52b47d9b19)


  ---
  ### Gráficos de Churn por Variáveis Numéricas (Exemplos)
  * **Tipo:** Histogramas Superpostos e Gráficos de Densidade (KDE Plot)
  * **Objetivo:** Visualizar a forma e densidade das distribuições de variáveis numéricas para clientes que cancelaram e não cancelaram.

  ![image](https://github.com/user-attachments/assets/14ed71df-c507-4003-ab23-584e7db9aee9)

  ![image](https://github.com/user-attachments/assets/2478b7ba-52d3-4dbf-aede-3d407db0d017)



# 📈 Análise e Conclusão

A análise exploratória de dados revelou padrões cruciais sobre a evasão de clientes. Os principais insights incluem:

* **Contratos Mensais são de Alto Risco:** Clientes com contratos de mês a mês demonstram uma taxa de churn significativamente mais elevada, indicando menor fidelidade e maior flexibilidade para trocar de provedor.
* **Serviço de Fibra Óptica e Churn:** A alta taxa de churn entre usuários de Fibra Óptica sugere que, apesar de ser um serviço moderno, pode haver problemas de qualidade, instabilidade ou expectativas não atendidas que levam ao cancelamento.
* **Fase Crítica nos Primeiros Meses:** Clientes com um tempo de serviço menor (`meses_de_servico`) são mais propensos ao churn. A maioria dos cancelamentos ocorre nos primeiros meses de contrato, ressaltando a importância da experiência inicial do cliente.
* **Padrões de Gastos:** Clientes que cancelam tendem a ter **gastos totais mais baixos** (associado ao menor tempo de serviço) e uma concentração maior em **gastos mensais mais elevados** (na faixa de $70 a $100), o que pode indicar insatisfação com o custo-benefício ou a atratividade de ofertas concorrentes.
* **Métodos de Pagamento e Outros Fatores:** O uso de **cheque eletrônico** está associado a uma maior taxa de churn. Além disso, clientes **cidadãos seniores**, **sem parceiro** e **sem dependentes** também mostraram uma tendência ligeiramente maior a cancelar o serviço.
* **Gênero não é Fator Relevante:** A análise não encontrou uma correlação significativa entre o gênero do cliente e a probabilidade de churn.

Esses insights são fundamentais para a empresa, pois direcionam os esforços de retenção para os segmentos de clientes mais vulneráveis e os fatores de maior impacto.

# Recomendações

Com base nos achados da análise, são propostas as seguintes recomendações para reduzir a taxa de churn:

* **Programas de Fidelidade para Contratos Longos:** Desenvolver incentivos e ofertas exclusivas para que clientes de contratos mensais migrem para planos de maior duração (anual ou bianual), aumentando o vínculo e reduzindo a probabilidade de cancelamento.
* **Avaliação e Otimização do Serviço de Fibra Óptica:** Realizar uma auditoria na qualidade do serviço de Fibra Óptica, investigando as principais reclamações dos clientes e implementando melhorias para aumentar a satisfação.
* **Estratégia de Onboarding e Retenção para Novos Clientes:** Criar um programa de "boas-vindas" robusto para clientes nos primeiros meses de serviço, com acompanhamento proativo, suporte técnico dedicado e ofertas personalizadas para solidificar o relacionamento.
* **Análise de Precificação e Valor Percebido:** Reavaliar a estrutura de preços e os pacotes de serviços, especialmente para clientes com gastos mensais mais altos, garantindo que o valor percebido corresponda ao custo e que a empresa se mantenha competitiva.
* **Incentivo a Métodos de Pagamento Alternativos:** Promover métodos de pagamento mais convenientes e seguros, oferecendo pequenos bônus ou descontos para clientes que optarem por débito automático ou cartão de crédito em vez de cheque eletrônico.
* **Segmentação e Atendimento Personalizado:** Desenvolver campanhas de retenção segmentadas para grupos de risco, como cidadãos seniores ou clientes sem laços familiares, oferecendo suporte e benefícios que atendam às suas necessidades específicas.

# 🔨 Ferramentas e Aplicativos Utilizados

- ``Python``
- ``GoogleColab``
- ``Trello``

# 💻 Desenvolvedores
[<img loading="lazy" src="https://avatars.githubusercontent.com/u/201495780?s=96&v=4" width=115><br><sub>Pedro Rocha</sub>](https://github.com/Pedro-Rocha89)

