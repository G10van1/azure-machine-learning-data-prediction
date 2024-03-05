# bike-rental-prediction

## Escolha o Idioma / Choose Language
- [English](#rental-bike-prediction)
- [Português](#predição-de-aluguel-de-bicicletas)

________________________________________________________________________________________________________________________________

## Versão em Português

## Predição de Aluguel de Bicicletas

## Visão Geral

Este repositório contém materiais para o módulo Microsoft Learn sobre Fundamentos de IA.

## Sumário
  - [Explorando o Aprendizado de Máquina Automatizado no Azure Machine Learning](#explorando-o-aprendizado-de-máquina-automatizado-no-azure-machine-learning)
  - [Passo 1: Criar um Espaço de Trabalho no Azure Machine Learning](#passo-1:-criar-um-espaço-de-trabalho-no-azure-machine-learning)
  - [Passo 2: Utilizar o aprendizado de máquina automatizado para treinar um modelo](#passo-2:-utilizar-o-aprendizado-de-máquina-automatizado-para-treinar-um-modelo)
  - [Passo 3: Revisar o melhor modelo](#passo-3:-revisar-o-melhor-modelo)
  - [Passo 4: Implantar e testar o modelo](#passo-4:-implantar-e-testar-o-modelo)
  - [Passo 5: Testar o serviço implantado](#passo-5:-testar-o-serviço-implantado)
  - [Passo 6: Limpeza](#passo-6:-limpeza)

# Explorando o Aprendizado de Máquina Automatizado no Azure Machine Learning

Este tutorial guia você pelo processo de explorar aprendizado de máquina automático no Azure Machine Learning. Você aprenderá como treinar, avaliar, implantar e testar um modelo de aprendizado de máquina usando o Azure Machine Learning studio. O exercício completo é esperado levar aproximadamente **30 minutos** para ser concluído.

## Passo 1: Criar um espaço de trabalho no Azure Machine Learning

Para usar o Azure Machine Learning, é necessário provisionar um espaço de trabalho no Azure em sua assinatura. Siga estes passos:

1. Faça login no [portal do Azure](https://portal.azure.com) usando suas credenciais da Microsoft.
2. Selecione **+ Criar um recurso**, pesquise por **Machine Learning** e crie um novo recurso **Azure Machine Learning** com as seguintes configurações:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie ou selecione um grupo de recursos.
   - **Nome**: Insira um nome exclusivo para o seu espaço de trabalho.
   - **Região**: Selecione a região geográfica mais próxima.
   - **Conta de armazenamento**, **Cofre de chaves**, **Application Insights**: Anote os novos recursos padrão que serão criados para o seu espaço de trabalho.
   - **Registro de contêiner**: Nenhum (será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).

3. Selecione **Revisar + criar**, em seguida, selecione **Criar**. Aguarde a criação do seu espaço de trabalho (pode levar alguns minutos) e vá para o recurso implantado.
4. Selecione **Iniciar o estúdio** (ou abra uma nova guia do navegador e acesse [https://ml.azure.com](https://ml.azure.com), e faça login no Azure Machine Learning studio usando sua conta da Microsoft).
5. No Azure Machine Learning studio, você deverá ver o espaço de trabalho recém-criado. Se não, selecione **Todos os espaços de trabalho** no menu à esquerda e depois selecione o espaço de trabalho que você acabou de criar.

## Passo 2: Utilisar o aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automático permite que você experimente vários algoritmos e parâmetros para treinar vários modelos. Neste exercício, você usará um conjunto de dados com detalhes históricos de aluguel de bicicletas para prever o número de aluguéis de bicicletas. Siga estes passos:

1. No [Azure Machine Learning studio](https://ml.azure.com), vá para a página **Automated ML** em **Authoring**.
2. Crie um novo trabalho de Automated ML com as seguintes configurações:
   - **Configurações básicas**:
     - **Nome do trabalho**: mslearn-bike-automl
     - **Nome do novo experimento**: mslearn-bike-rental
     - **Descrição**: Aprendizado de máquina automático para previsão de aluguel de bicicletas
     - **Tags**: Nenhum
   - **Tipo de tarefa e dados**:
     - **Selecionar tipo de tarefa**: Regressão
     - **Selecionar conjunto de dados**: Crie um novo conjunto de dados chamado **bike-rentals** de arquivos da web com a URL [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals) e as configurações especificadas.
   - **Configurações de tarefa**:
     - Configure o tipo de tarefa, conjunto de dados, coluna alvo e configurações adicionais conforme especificado.
   - **Computação**:
     - Configure o tipo de computação, tipo de máquina virtual, camada, tamanho e número de instâncias.

3. Envie o trabalho de treinamento. Ele começará automaticamente.
4. Aguarde a conclusão do trabalho. Isso pode levar algum tempo.

## Passo 3: Revisar o melhor modelo

Quando o trabalho de aprendizado de máquina automático for concluído, revise o melhor modelo treinado:

1. Na guia **Visão geral** do trabalho de aprendizado de máquina automático, observe o resumo do melhor modelo.
2. Selecione o texto sob **Nome do algoritmo** para o melhor modelo para visualizar seus detalhes.
3. Selecione a guia **Métricas** e revise os gráficos **residuais** e **previsto_real**.

## Passo 4: Implantar e testar o modelo

1. Na guia **Modelo** para o melhor modelo, selecione **Implantar** e use a opção **Serviço da Web** para implantar o modelo com as configurações especificadas.
2. Aguarde o início da implantação - isso pode levar alguns segundos.
3. Aguarde o **Status da implantação** mudar para **Concluído**. Isso pode levar de 5 a 10 minutos.

## Passo 5: Testar o serviço implantado

Agora você pode testar o serviço implantado:

1. No Azure Machine Learning studio, no menu à esquerda, selecione **Pontos de extremidade** e abra o ponto de extremidade de tempo real **predict-rentals**.
2. Na página do ponto de extremidade de tempo real **predict-rentals**, visualize a guia **Testar**.
3. Na painel **Dados de entrada para testar o ponto de extremidade**, substitua o JSON modelo pelo seguinte conjunto de dados de entrada:

```json
{
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
}
```

4. Clique no botão Testar.
5. Analise os resultados do teste, que incluem o número previsto de aluguéis com base nas características de entrada.
     
## Passo 6: Limpeza

O serviço da web que você criou está hospedado em uma Instância de Contêiner do Azure. Se você não pretende experimentar mais, siga estas etapas para limpar:

No Azure Machine Learning studio, na guia Pontos de extremidade, selecione o ponto de extremidade predict-rentals. Em seguida, selecione Excluir e confirme que deseja excluir o ponto de extremidade.

Para excluir seu espaço de trabalho:

No portal do Azure, na página Grupos de recursos, abra o grupo de recursos que você especificou ao criar seu espaço de trabalho no Azure Machine Learning.
Clique em Excluir grupo de recursos, digite o nome do grupo de recursos para confirmar que deseja excluí-lo e selecione Excluir.
Agora você explorou com sucesso o aprendizado de máquina automático no Azure Machine Learning. Para mais detalhes, visite o repositório GitHub.

## Referências:

[Explore Automated Machine Learning in Azure Machine Learning](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html)

[Explore Azure AI Services](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html)

________________________________________________________________________________________________________________________________

## English Version

## Rental Bike Prediction

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
