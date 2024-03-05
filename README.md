# bike-rental-prediction

## Escolha o Idioma / Choose Language
- [English](#english)
- [Português](#português)

## Versão em Português

## Predição de Aluguel de Bicicletas {#português}

## Visão Geral

Este repositório contém materiais para o módulo Microsoft Learn sobre Fundamentos de IA.

## Sumário
- [Explorar o Aprendizado de Máquina Automatizado no Azure Machine Learning](#explorar-o-aprendizado-de-máquina-automatizado-no-azure-machine-learning)
  - [Criar um Espaço de Trabalho no Azure Machine Learning](#criar-um-espaço-de-trabalho-no-azure-machine-learning)
  - [Utilizar aprendizado de máquina automatizado para treinar um modelo](#utilizar-aprendizado-de-máquina-automatizado-para-treinar-um-modelo)
  - [Revisar o melhor modelo](#revisar-o-melhor-modelo)
  - [Implantar e testar o modelo](#implantar-e-testar-o-modelo)
  - [Testar o serviço implantado](#testar-o-serviço-implantado)
  - [Limpeza](#limpeza)

## Navegação

- [Microsoft Learn](https://docs.microsoft.com/training/)
- [Repositório no GitHub](https://github.com/MicrosoftLearning/mslearn-ai-fundamentals)

## Pré-requisitos

- Conhecimento básico dos serviços do Azure.
- Assinatura do Azure.

## Explorar o Aprendizado de Máquina Automatizado no Azure Machine Learning

Neste exercício, você utilizará o recurso de aprendizado de máquina automatizado no Azure Machine Learning para treinar e avaliar um modelo de aprendizado de máquina. Em seguida, implantará e testará o modelo treinado.

**Estimativa de Tempo:** Aproximadamente 30 minutos.

### Criar um Espaço de Trabalho no Azure Machine Learning

Para usar o Azure Machine Learning, é necessário provisionar um espaço de trabalho no Azure Machine Learning em sua assinatura do Azure. Em seguida, você poderá usar o Azure Machine Learning Studio para trabalhar com os recursos em seu espaço de trabalho.

**Dica:** Se já tiver um espaço de trabalho no Azure Machine Learning, você pode usá-lo e pular para a próxima tarefa.

1. Faça login no [portal do Azure](https://portal.azure.com) usando suas credenciais da Microsoft.
2. Selecione **+ Criar um recurso**, procure por *Machine Learning* e crie um novo recurso **Azure Machine Learning** com as configurações especificadas.

    - Assinatura: Sua assinatura do Azure.
    - Grupo de recursos: Crie ou selecione um grupo de recursos.
    - Nome: Insira um nome exclusivo para o seu espaço de trabalho.
    - Região: Selecione a região geográfica mais próxima.
    - Conta de armazenamento, Cofre de chaves, Insights de aplicativo: Observe os novos recursos padrão que serão criados para o seu espaço de trabalho.
    - Registro de contêineres: Nenhum (criado automaticamente ao implantar um modelo em um contêiner).

3. Selecione **Revisar + criar**, em seguida, selecione **Criar**. Aguarde a criação do seu espaço de trabalho e vá para o recurso implantado.
4. Selecione **Iniciar o studio** ou acesse [Azure Machine Learning Studio](https://ml.azure.com?azure-portal=true) e faça login.

No Azure Machine Learning Studio, você deve ver o espaço de trabalho recém-criado. Se não estiver vendo, selecione **Todos os espaços de trabalho** no menu à esquerda e, em seguida, selecione o espaço de trabalho que acabou de criar.

### Utilizar Aprendizado de Máquina Automatizado para Treinar um Modelo

O aprendizado de máquina automatizado permite que você experimente vários algoritmos e parâmetros para treinar vários modelos e identificar o melhor para seus dados.

**Citação:** Os dados usados neste exercício são derivados do [Capital Bikeshare](https://www.capitalbikeshare.com/system-data) e são usados de acordo com o [contrato de licença de dados](https://www.capitalbikeshare.com/data-license-agreement) publicado.

1. No [Azure Machine Learning Studio](https://ml.azure.com?azure-portal=true), visualize a página **Automated ML** em **Authoring**.
2. Crie um novo trabalho de Automated ML com as configurações especificadas.

    **Configurações básicas:**
    - Nome do trabalho: mslearn-bike-automl
    - Nome do experimento: mslearn-bike-rental
    - Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
    - Tags: nenhum

    **Tipo de tarefa e dados:**
    - Selecione o tipo de tarefa: Regressão
    - Selecione o conjunto de dados: Crie um novo conjunto de dados com as configurações especificadas.

        - Tipo de dado:
            - Nome: bike-rentals
            - Descrição: Dados históricos de aluguel de bicicletas
            - Tipo: Tabular

        - Fonte de dados:
            - De arquivos da web

        - URL da web:
            - URL da web: https://aka.ms/bike-rentals
            - Pular validação de dados: Não selecione

        - Configurações:
            - Formato do arquivo: Delimitado
            - Delimitador: Vírgula
            - Codificação: UTF-8
            - Cabeçalhos de coluna: Somente o primeiro arquivo possui cabeçalhos
            - Pular linhas: Nenhum
            - Conjunto de dados contém dados de várias linhas: Não selecione

        - Esquema:
            - Incluir todas as colunas, exceto Path
            - Revisar os tipos detectados automaticamente

        Selecione **Criar**. Após a criação do conjunto de dados, selecione o conjunto de dados **bike-rentals** para continuar a enviar o trabalho Automated ML.

    **Configurações da tarefa:**
    - Tipo de tarefa: Regressão
    - Conjunto de dados: bike-rentals
    - Coluna de destino: Aluguéis (inteiro)
    - Configurações de  configuração adicional:

        - Métrica primária: Erro quadrático médio normalizado
        - Explicar o melhor modelo: Não selecionado
        - Usar todos os modelos suportados: Não selecionado (você restringirá o trabalho a tentar apenas alguns algoritmos específicos.)
        - Modelos permitidos: Selecione apenas RandomForest e LightGB


##________________________________________________________________________________________________________________________________
## English Version

## Rental Bike Prediction {#english}

## Overview

This repository contains materials for the Microsoft Learn module on AI Fundamentals.

## Table of Contents
  - [Explore Automated Machine Learning in Azure Machine Learning](#explore-automated-machine-learning-in-azure-machine-learning)
  - [Create an Azure Machine Learning workspace](#create-an-azure-machine-learning-workspace)
  - [Use automated machine learning to train a model](#use-automated-machine-learning-to-train-a-model)
  - [Review the best model](#review-the-best-model)
  - [Deploy and test the model](#deploy-and-test-the-model)
  - [Test the deployed service](#test-the-deployed-service)
  - [Clean-up](#clean-up)

## Navigation

- [Microsoft Learn](https://docs.microsoft.com/training/)
- [GitHub Repository](https://github.com/MicrosoftLearning/mslearn-ai-fundamentals)

## Prerequisites

- Basic knowledge of Azure services.
- Azure subscription.

## Explore Automated Machine Learning in Azure Machine Learning

In this exercise, you’ll use the automated machine learning feature in Azure Machine Learning to train and evaluate a machine learning model. You’ll then deploy and test the trained model.

**Time Estimate:** Approximately 30 minutes.

### Create an Azure Machine Learning workspace

To use Azure Machine Learning, you need to provision an Azure Machine Learning workspace in your Azure subscription. Then you’ll be able to use Azure Machine Learning studio to work with the resources in your workspace.

**Tip:** If you already have an Azure Machine Learning workspace, you can use that and skip to the next task.

1. Sign into the [Azure portal](https://portal.azure.com) using your Microsoft credentials.
2. Select **+ Create a resource**, search for *Machine Learning*, and create a new **Azure Machine Learning** resource with the specified settings.

    - Subscription: Your Azure subscription.
    - Resource group: Create or select a resource group.
    - Name: Enter a unique name for your workspace.
    - Region: Select the closest geographical region.
    - Storage account, Key vault, Application insights: Note the default new resources that will be created for your workspace.
    - Container registry: None (created automatically on deploying a model to a container).

3. Select **Review + create**, then select **Create**. Wait for your workspace to be created, and then go to the deployed resource.
4. Select **Launch studio** or navigate to [Azure Machine Learning studio](https://ml.azure.com?azure-portal=true) and sign in.

In Azure Machine Learning studio, you should see your newly created workspace. If not, select **All workspaces** in the left-hand menu and then select the workspace you just created.

### Use automated machine learning to train a model

Automated machine learning enables you to try multiple algorithms and parameters to train multiple models and identify the best one for your data.

**Citation:** The data used in this exercise is derived from [Capital Bikeshare](https://www.capitalbikeshare.com/system-data) and is used in accordance with the published data [license agreement](https://www.capitalbikeshare.com/data-license-agreement).

1. In [Azure Machine Learning studio](https://ml.azure.com?azure-portal=true), view the **Automated ML** page under **Authoring**.
2. Create a new Automated ML job with the specified settings.

    **Basic settings:**
    - Job name: mslearn-bike-automl
    - New experiment name: mslearn-bike-rental
    - Description: Automated machine learning for bike rental prediction
    - Tags: none

    **Task type & data:**
    - Select task type: Regression
    - Select dataset: Create a new dataset with the specified settings.

        - Data type:
            - Name: bike-rentals
            - Description: Historic bike rental data
            - Type: Tabular

        - Data source:
            - From web files

        - Web URL:
            - Web URL: https://aka.ms/bike-rentals
            - Skip data validation: Do not select

        - Settings:
            - File format: Delimited
            - Delimiter: Comma
            - Encoding: UTF-8
            - Column headers: Only first file has headers
            - Skip rows: None
            - Dataset contains multi-line data: Do not select

        - Schema:
            - Include all columns other than Path
            - Review the automatically detected types

        Select **Create**. After the dataset is created, select the **bike-rentals** dataset to continue to submit the Automated ML job.

    **Task settings:**
    - Task type: Regression
    - Dataset: bike-rentals
    - Target column: Rentals (integer)
    - Additional configuration settings:

        - Primary metric: Normalized root mean squared error
        - Explain best model: Unselected
        - Use all supported models: Unselected (You’ll restrict the job to try only a few specific algorithms.)
        - Allowed models: Select only RandomForest and LightGBM — normally you’d want to try as many as possible, but each model added increases the time it takes to run the job.

    - Limits: Expand this section

        - Max trials: 3
        - Max concurrent trials: 3
        - Max nodes: 3
        - Metric score threshold: 0.085 (so that if a model achieves a normalized root mean squared error metric score of 0.085 or less, the job ends.)
        - Timeout: 15
        - Iteration timeout: 15
        - Enable early termination: Selected

    - Validation and test:

        - Validation type: Train-validation split
        - Percentage of validation data: 10
        - Test dataset: None

    **Compute:**
    - Select compute type: Serverless
    - Virtual machine type: CPU
    - Virtual machine tier: Dedicated
    - Virtual machine size: Standard_DS3_V2*
    - Number of instances: 1

        *If your subscription restricts the VM sizes available to you, choose any available size.

3. Submit the training job. It starts automatically.
4. Wait for the job to finish. It might take a while — now might be a good time for a coffee break!

### Review the best model

When the automated machine learning job has completed, you can review the best model it trained.

1. On the **Overview** tab of the automated machine learning job, note the best model summary.
    ![Best Model Summary](/mslearn-ai-fundamentals/Instructions/Labs/media/use-automated-machine-learning/complete-run.png)

    **Note:** You may see a message under the status “Warning: User specified exit score reached…”. This is an expected message. Please continue to the next step.

2. Select the text under **Algorithm name** for the best model to view its details.
3. Select the **Metrics** tab and select the **residuals** and **predicted_true** charts if they are not already selected.

    Review the charts which show the performance of the model. The **residuals** chart shows the residuals (the differences between predicted and actual values) as a histogram. The **


### References:

[Explore Automated Machine Learning in Azure Machine Learning](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html)
[Explore Azure AI Services](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html)
