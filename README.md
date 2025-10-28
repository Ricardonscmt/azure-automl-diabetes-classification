# Projeto: Classificação de Diabetes com Azure Automated ML

Este projeto demonstra o uso do Azure Machine Learning (Azure ML) para treinar e avaliar múltiplos modelos de classificação usando a funcionalidade de Automated ML (AutoML). O objetivo é prever a probabilidade de um paciente ter diabetes com base em dados de saúde.

## Tecnologias Utilizadas

* **Microsoft Azure** (Azure Machine Learning)
* **Python**
* **Azure ML SDK (v2)**
* **Automated ML (AutoML)**
* **Jupyter Notebooks**
* **MLTable** (Ativos de Dados)

## O Processo

O fluxo de trabalho deste projeto cobriu todo o ciclo de vida inicial de um modelo, desde a configuração da nuvem até a análise do modelo.

1.  **Configuração do Ambiente**
    Criação do Workspace do Azure ML, Instância de Computação (para o notebook) e Cluster de Computação (para treinamento em escala).

2.  **Gerenciamento de Dados**
    Registro dos dados de diabetes como um **Ativo de Dados (Data Asset)** do tipo `MLTable`.
    * **Desafio de Depuração:** Durante o desenvolvimento, o job de AutoML falhou inicialmente com o erro `path can't be empty`. Isso foi resolvido adicionando uma etapa explícita no notebook para criar e registrar o `Data Asset` a partir dos arquivos locais usando o SDK, garantindo que o job pudesse localizar e consumir os dados para treinamento.

3.  **Treinamento com AutoML**
    Configuração e submissão de um job de AutoML para uma tarefa de Classificação. A métrica primária definida foi `AUC_weighted`, e o Azure foi configurado para testar e avaliar diversos algoritmos (como `LightGBM`, `XGBoost`, `RandomForest`, etc.) automaticamente.

4.  **Análise de Resultados**
    Revisão dos modelos treinados no Azure ML Studio, identificando o melhor modelo com base na métrica de desempenho
    
5.  **Explicabilidade do Modelo**
    Geração de explicações do modelo (baseadas em SHAP) para o melhor modelo. Esta etapa foi crucial para entender quais *features* (como `Glicose`, `Idade` e `IMC`) tiveram o maior impacto nas previsões do modelo.

