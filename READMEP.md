[\[English\]](README.md) [\[Português\]](#predição-de-dados-usando-o-azure-machine-learning)
_______________________________________________________________________________________________________________________________________
# Predição de Dados Usando o Azure Machine Learning

## Sumário
  - [Explorando o Aprendizado de Máquina Automatizado no Azure Machine Learning](#explorando-o-aprendizado-de-máquina-automatizado-no-azure-machine-learning)
  - [Passo 1: Criar um Espaço de Trabalho no Azure Machine Learning](#passo-1-criar-um-espaço-de-trabalho-no-azure-machine-learning)
  - [Passo 2: Utilizar o aprendizado de máquina automatizado para treinar um modelo](#passo-2-utilizar-o-aprendizado-de-máquina-automatizado-para-treinar-um-modelo)
  - [Passo 3: Revisar o melhor modelo](#passo-3-revisar-o-melhor-modelo)
  - [Passo 4: Implantar e testar o modelo](#passo-4-implantar-e-testar-o-modelo)
  - [Passo 5: Testar o serviço implantado](#passo-5-testar-o-serviço-implantado)
  - [Passo 6: Limpeza](#passo-6-limpeza)

## Explorando o Aprendizado de Máquina Automatizado no Azure Machine Learning

Este tutorial é baseado na documentação oficial da Microsoft e em seus tutoriais. Este documento serve de guia no processo de explorar aprendizado de máquina automatizado no Azure Machine Learning. Você aprenderá como treinar, avaliar, implantar e testar um modelo de aprendizado de máquina usando o Azure Machine Learning studio. Vamos utilizar o arquivo de dados referente ao aluguel de bicicletas diário. O arquivo formato csv está em anexo neste repositório, existem outros arquivos csv anexos que também podem ser utilizados para fins didáticos.

## Passo 1: Criar um espaço de trabalho no Azure Machine Learning

Para usar o Azure Machine Learning, é necessário provisionar um espaço de trabalho no Azure em sua assinatura. Siga estes passos:

1. Faça login no [portal do Azure](https://portal.azure.com) usando suas credenciais da Microsoft.
2. Selecione **+ Criar um recurso**, pesquise por **Machine Learning** e crie um novo recurso **Azure Machine Learning** com as seguintes configurações:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie ou selecione um grupo de recursos.
   - **Nome**: Insira um nome exclusivo para o seu espaço de trabalho.
   - **Região**: Selecione a região geográfica, considere a próximidade e o custo de serviço na escolha.
   - **Conta de armazenamento**, **Cofre de chaves**, **Application Insights**: Anote os novos recursos padrão que serão criados para o seu espaço de trabalho.
   - **Registro de contêiner**: Nenhum (será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).

3. Selecione **Revisar + criar**, em seguida, selecione **Criar**. Aguarde a criação do seu espaço de trabalho (pode levar alguns minutos) e vá para o recurso implantado.
4. Selecione **Iniciar o estúdio** (ou abra uma nova guia do navegador e acesse [https://ml.azure.com](https://ml.azure.com), e faça login no Azure Machine Learning studio usando sua conta da Microsoft).
5. No Azure Machine Learning studio, você deverá ver o espaço de trabalho recém-criado. Se não, selecione **Todos os espaços de trabalho** no menu à esquerda e depois selecione o espaço de trabalho que você acabou de criar.

## Passo 2: Utilizar o aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automático permite que você experimente vários algoritmos e parâmetros para treinar vários modelos. Neste exercício, você usará um conjunto de dados com detalhes históricos de aluguel de bicicletas para prever o número de aluguéis de bicicletas. Siga estes passos:

1. No [Azure Machine Learning studio](https://ml.azure.com), vá para a página **Automated ML** em **Authoring**.
2. Crie um novo trabalho de Automated ML com as seguintes configurações:

      
   - **Basic settings**:
     - **Job name**: mslearn-bike-automl
     - **New experiment name**: mslearn-bike-rental
     - **Description**: Automated machine learning for bike rental prediction
     - **Tags**: none
   - **Task type & data**:
     - **Select task type**: Regression
     - **Select dataset**: Create a new dataset with the following settings:
       - **Data type**:
         - **Name**: bike-rentals
         - **Description**: Historic bike rental data
         - **Type**: Tabular
       - **Data source**:
         - Select **From web files**
       - **Web URL**:
         - **Web URL**: `https://aka.ms/bike-rentals`
         - **Skip data validation**: do not select
       - **Settings**:
         - **File format**: Delimited
         - **Delimiter**: Comma
         - **Encoding**: UTF-8
         - **Column headers**: Only first file has headers
         - **Skip rows**: None
         - **Dataset contains multi-line data**: do not select
       - **Schema**:
         - Incluir todas as colunas exceto **Path**
         - Revise os tipos detectados automaticamente
     - Selecione **Create**. Depois do dataset ser criado, selecione o **bike-rentals** dataset para continuar a enviar a tarefa ML Automatizada.
   - **Task settings**:
     - **Task type**: Regression
     - **Dataset**: bike-rentals
     - **Target column**: Rentals (integer)
     - **Additional configuration settings**:
       - **Primary metric**: Normalized root mean squared error
       - **Explain best model**: Não selecionado
       - **Use all supported models**: Não selecionado. *Você restringirá o trabalho para tentar apenas alguns algoritmos específicos.*
       - **Allowed models**: *Selecione somente* **RandomForest** and **LightGBM** — *a escolha de muitos parâmetros pode onerar muito em tempo de processamento da tarefa*
     - **Limits**: Expand this section
       - **Max trials**: 3
       - **Max concurrent trials**: 3
       - **Max nodes**: 3
       - **Metric score threshold**: 0.085 (*deste modo, se um modelo atingir uma pontuação métrica de erro quadrático médio normalizado de 0,085 ou menos, o trabalho será encerrado.*)
       - **Timeout**: 15
       - **Iteration timeout**: 15
       - **Enable early termination**: Selected
     - **Validation and test**:
       - **Validation type**: Train-validation split
       - **Percentage of validation data**: 10
       - **Test dataset**: None
   - **Compute**:
     - **Select compute type**: Serverless
     - **Virtual machine type**: CPU
     - **Virtual machine tier**: Dedicated
     - **Virtual machine size**: Standard_DS3_V2* 
     - **Number of instances**: 1
       
    \* *If your subscription restricts the VM sizes available to you, choose any available size.*
   
3. Envie o trabalho de treinamento. Ele começará automaticamente.
4. Aguarde a conclusão do trabalho. Isso pode levar algum tempo.

## Passo 3: Revisar o melhor modelo

Quando o trabalho de aprendizado de máquina automático for concluído, revise o melhor modelo treinado:

1. Na guia **Visão geral** do trabalho de aprendizado de máquina automático, observe o resumo do melhor modelo.

![image](https://github.com/G10van1/bike-rental-prediction/assets/17678389/6ca502ce-2bc2-41fc-a2ce-dd249bac2351)


2. Selecione o texto sob **Nome do algoritmo** para o melhor modelo para visualizar seus detalhes.
3. Selecione a guia **Métricas** e revise os gráficos **residuais** e **predicted_true**.

## Passo 4: Implantar e testar o modelo

1. Na guia **Modelo** para o melhor modelo, selecione **Implantar** e use a opção **Serviço da Web** para implantar o modelo com as configurações especificadas.

   ```
    Name: predict-rentals
    Description: Predict cycle rentals
    Compute type: Azure Container Instance
    Enable authentication: Selected
   ```
   
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
   
```json
 {
   "Results": [
     444.27799000000000
   ]
 }
```

O teste usou os dados de entrada e o modelo que você treinou para retornar o número previsto de aluguéis.

Vamos revisar o que foi feito. Você usou um conjunto de dados históricos de aluguel de bicicletas para treinar um modelo. O modelo prevê o número de locações de bicicletas esperados num determinado dia, com base em características sazonais e meteorológicas.
     
## Passo 6: Limpeza

O serviço da web que você criou está hospedado em uma Instância de Contêiner do Azure. Se você não pretende experimentar mais, siga estas etapas para limpar:

No Azure Machine Learning studio, na guia Pontos de extremidade, selecione o ponto de extremidade predict-rentals. Em seguida, selecione Excluir e confirme que deseja excluir o ponto de extremidade.

Para excluir seu espaço de trabalho:

No portal do Azure, na página Grupos de recursos, abra o grupo de recursos que você especificou ao criar seu espaço de trabalho no Azure Machine Learning.
Clique em Excluir grupo de recursos, digite o nome do grupo de recursos para confirmar que deseja excluí-lo e selecione Excluir.
Agora você explorou com sucesso o aprendizado de máquina automático no Azure Machine Learning. 

## Referências:

- [Explore Automated Machine Learning in Azure Machine Learning](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html)
- [Explore Azure AI Services](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html)
- [Microsoft Learn](https://docs.microsoft.com/training/)
- [Microsoft GitHub Repository](https://github.com/MicrosoftLearning/mslearn-ai-fundamentals)
