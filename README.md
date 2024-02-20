# brecom-analysis

Estudo realizado como parte do curso de Ciência e Análise de Dados da #Ada-Tech.

## Participantes do projeto:
- [Adam Basilio](https://github.com/abasilio91)
- [Daniel Rodrigues](https://www.linkedin.com/in/danielrodrigues-ds/)
- [Gabriela Rodrigues](https://www.linkedin.com/in/gabrielarodriguesdados/)
- [Raphael Tsuchiya](https://github.com/raphaeltsuchiya)

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

<details> 
  <summary> Introdução </summary>

  
</details>

- Se apresentar como uma empresa (fictícia) de consultória que ficou responsável por analisar os dados de vendas da Olist (o que é Olist?) e propôr melhorias.
- Quem é a Olist?
- Comentar os dados.
- A princípio foi levantado duas hipóteses de melhoria. Objetivo?
  - O projeto de um Centro de Distribuição
  - O cálculo de probabilidade de recompras baseados nas avaliações

<details> 
  <summary> Metodologia </summary>

</details>
- Análise exploratória
- Análise descritiva dos dados
- Análise estatística

<details> 
  <summary> Resultados </summary>

  ### Limpeza dos dados

  Durante a etapa de exploração de dados foi verificado, em cada um das tabelas da base, se existiam valores faltantes (Nulls e NaN's) e valores duplicados. Para o primeiro caso, utilizou-se a função `isna()` juntamente com a função `value_counts()` do pacote Pandas. Para o último, o `value_counts()` numa coluna de identificação da tabela, e verificou-se se houveram valores repetidos. 

  Quanto a valores duplicados, nenhuma evidência foi encontrada. Quanto a valores nulos, foi observado algumas ocorrências nas tabelas `orders`, `order_reviews` e `products`, apenas. Na tabela `orders`, os valores nulos ocorreram nas colunas `order_approved_at`  `order_delivered_carrier_date` e `order_delivered_customer_date`. Considerando que esta tabela registra informações gerais sobre os pedidos, é de se esperar que existam valores nulos nestas colunas, uma vez que nem todo pedido já teve seu curso completo (aprovação, entrega à transportadora, entrega no destino final). Os valores nulos da tabela `order_reviews` ocorreram exclusivamente nas colunas `review_comment_title`  `review_comment_message`, o que também é de se esperar, visto que nem todos os usuários deixam comentários nas compras que fizeram. 

  Por fim, a tabela `products` teve valores nulos em todas as colunas. Foi observado também que os valores nulos ocorreram nas colunas de identificação dos produtos (categoria, nome, descrição, fotos, etc.) Visto que os produtos estão identificados apenas por um código de ID, fica impossível tentar determiná-los. Sendo assim, preferiu-se evitar utilizar a tabela `products` em análises.

  ### Análise descritiva dos dados
  
  Um dos objetivos do estudo foi de verificar a probabilidade de recompras baseado nas opiniões dadas pelos usuários. Para isso, focou-se nas informações vindas das tabelas `orders` e `orders_reviews`. A porcentagem de usuários que deixam comentários sobre os produtos é de cerca de 40%. As avaliações seguem proporções parecidas, independente se o usuário deixa ou não um comentário, sendo que cerca de 88% das avaliações são de 5, 4 ou 1 estrela. Entretanto, um número significativo dos comentários (10%), são feitos antes mesmo de o produto ser recebido. Nestes casos, as avaliações variam, majoritariamente, entre 5 e 1, enquanto que as avaliações com notas 2, 3 ou 4 seguem em proporções menores.[.^1]

  ### Análise estatística

</details>

<details> 
  <summary> Conclusão </summary>

  
</details>
- Rever a política de cálculo de prazo de entrega

[.^1]: Para a visualização dos dados descritos, veja a aba `revisões` no arquivo `Ecommerce-ollis.pbix`
