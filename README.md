# brecom-analysis

Estudo realizado como parte do curso de Ciência e Análise de Dados da #Ada-Tech.

### Participantes do projeto:
- [Adam Basilio](https://github.com/abasilio91)
- [Daniel Rodrigues](https://www.linkedin.com/in/danielrodrigues-ds/)
- [Gabriela Rodrigues](https://www.linkedin.com/in/gabrielarodriguesdados/)
- [Raphael Tsuchiya](https://github.com/raphaeltsuchiya)
- [Augusto Messias]()

## Contextualização

O objetivo do projeto foi desenvolver um estudo baseado em um conjunto de dados (dataset) do [Kaggle](https://www.kaggle.com/), com os seguintes requisitos:

- Preparação dos Dados e Verificação de Consistência: Neste tópico deve ser feita a verificação da consistência dos dados e caso necessário efetuar eventuais modificações na base de dados. Alguns dos procedimentos que podemos fazer aqui são: Remoção e/ou tratamento de valores faltantes, remoção de duplicatas, ajustes dos tipos de variáveis, análise de outliers entre outras;
- Análise Exploratória dos Dados: Para fazermos a modelagem, precisamos conhecer muito bem os dados que estamos trabalhando. Por isso, nesta parte do projeto vocês desenvolveram análises e gráficos a respeito dos dados que estão utilizando. Tente tirar ao máximo informações sobre as variáveis em si e suas relações com as demais;
- Conclusões sobre o Projeto: Para finalizar, descreva as suas conclusões sobre os dados, resultados obtidos e próximos passos.

## Base de dados selecionada

A base escolhida foi a "Brazilian E-Commerce Public Dataset by Olist", e por isso o nome do projeto: BR e-com Analysis. A base está disponível [nesse link](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).

## Inicialização

  O arquivo `brecom-analysis.ipynb` é o arquivo principal do projeto, visto que nele estão todas as análises feitas. Para reproduzir corretamente os resultados que serão mostrados aqui, o usuário precisa, primeiro, preparar o ambiente corretamente, seguindo os passos abaixo:

  <details>
    <summary> Fazendo o download da base do Kaggle (Standalone) </summary>
   
  - Entre no [link da API do Kaggle](https://www.kaggle.com/docs/api) e siga os procedimentos descritos na seção de **inicialização** para fazer o download do arquivo `kaggle.json`.
  - Crie uma pasta com o nome `.kaggle` no seu ambiente python e cole o arquivo `kaggle.json` dentro dessa pasta.
  - No arquivo `brecom-analysis.ipynb`, encontre o comando abaixo e substitua o caminho do download da base para um na sua máquina:
    
  ```
  !kaggle datasets download -d olistbr/brazilian-ecommerce -p D:\Adam\Estudos\ADA\tecprog\projeto\brecom-analysis\database --unzip    
  ```
  </details>

<details>
  <summary> Fazendo o download da base do Kaggle (Google Colab) </summary>
 
  - Entre no [link da API do Kaggle](https://www.kaggle.com/docs/api) e siga os procedimentos descritos na seção de **inicialização** para fazer o download do arquivo `kaggle.json`.
  - Utilize a sequência de comandos abaixo para criar uma pasta `.kaggle` no ambiente do Colab.
 
  ```
  !mkdir -p ~/.kaggle
  ```
  
  - Faça o upload do arquivo `kaggle.json` na pasta `content` do Colab.
  - Utilize a sequência de comandos abaixo para transferir o arquivo `kaggle.json` para a pasta `.kaggle`.
  
  ```
  !cp kaggle.json ~/.kaggle/
  !chmod 600 ~/.kaggle/kaggle.json
  ```
  
  - Utilize a sequência de comandos abaixo para fazer o download da base do kaggle para a pasta `database`.
 
  ```
  !mkdir /content/brecom-analysis/database
  %cd /content/brecom-analysis/database
  !kaggle datasets download -d olistbr/brazilian-ecommerce
  !unzip /content/brecom-analysis/database/brazilian-ecommerce.zip
  %cd ../
  ``` 
</details>

## Introdução

