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

## Relatório

<details> 

  <summary> Introdução </summary>

  - Se apresentar como uma empresa (fictícia) de consultória que ficou responsável por analisar os dados de vendas da Olist (o que é Olist?) e propôr melhorias.
  - Quem é a Olist?
  - Comentar os dados.
  - A princípio foi levantado duas hipóteses de melhoria. Objetivo?
    - O projeto de um Centro de Distribuição
    - O cálculo de probabilidade de recompras baseados nas avaliações
  
</details>

<details> 

  <summary> Metodologia </summary>

  - Análise exploratória
  - Análise descritiva dos dados

</details>

<details> 

  <summary> Resultados </summary>

  ### Limpeza dos dados

  Durante a etapa de exploração de dados foi verificado, em cada um das tabelas da base, se existiam valores faltantes (Nulls e NaN's) e valores duplicados. Para o primeiro caso, utilizou-se a função `isna()` juntamente com a função `value_counts()` do pacote Pandas. Para o último, o `value_counts()` numa coluna de identificação da tabela, e verificou-se se houveram valores repetidos. 

  Quanto a valores duplicados, nenhuma evidência foi encontrada. Quanto a valores nulos, foi observado algumas ocorrências nas tabelas `orders`, `order_reviews` e `products`, apenas. Na tabela `orders`, os valores nulos ocorreram nas colunas `order_approved_at`  `order_delivered_carrier_date` e `order_delivered_customer_date`. Considerando que esta tabela registra informações gerais sobre os pedidos, é de se esperar que existam valores nulos nestas colunas, uma vez que nem todo pedido já teve seu curso completo (aprovação, entrega à transportadora, entrega no destino final). Os valores nulos da tabela `order_reviews` ocorreram exclusivamente nas colunas `review_comment_title`  `review_comment_message`, o que também é de se esperar, visto que nem todos os usuários deixam comentários nas compras que fizeram. 

  Por fim, a tabela `products` teve valores nulos em todas as colunas. Foi observado também que os valores nulos ocorreram nas colunas de identificação dos produtos (categoria, nome, descrição, fotos, etc.) Visto que os produtos estão identificados apenas por um código de ID, fica impossível tentar determiná-los. Sendo assim, preferiu-se evitar utilizar a tabela `products` em análises.

  ### Análise descritiva dos dados
  
  Um dos objetivos do estudo foi de verificar a probabilidade de recompras baseado nas opiniões dadas pelos usuários. Para isso, focou-se nas informações vindas das tabelas `orders` e `orders_reviews`. A porcentagem de usuários que deixam comentários sobre os produtos é de cerca de 40%. As avaliações seguem proporções parecidas, independente se o usuário deixa ou não um comentário, sendo que cerca de 88% das avaliações são de 5, 4 ou 1 estrela. Entretanto, um número significativo dos comentários (10%), são feitos antes mesmo de o produto ser recebido. Nestes casos, as avaliações variam, majoritariamente, entre 5 e 1, enquanto que as avaliações com notas 2, 3 ou 4 seguem em proporções menores[^1]. 
  
  Também foi verificada o tamanho médio dos comentários deixados, separados pelo número de estrelas da 
  avaliação [^2]. Neste análise, ficou claro que os maiores comentários se encontram nas avalições com menores estrelas, ou seja, existe uma correção direta entre o nível de satisfação do usuário e a vontade de o usuário de comunicar sua experiência. 
  
  Para se ter um melhor entendimento dos comentários deixados nas publicações, foi gerou-se uma núvem de palavras e destacou-se as vinte palavras mais comuns[^3]. Foi observado que a palavra `produto` aparece com maior frequência em todos os casos, o que não agrega muita relevância. Entretanto, as palavras subsequentes incluem os termos "prazo", "entrega" e "chegou", o que apontam para uma grande relevância nos serviços de entrega e fretamento dos produtos. Além disso, alguns adjetivos e advérbios como "bem", "bom", "antes" também chegaram à lista das palavras mais frequentes. Isoladas, estas não nos dizem muito, mas levanta a questão estas palavras foram combinadas nas avaliações.

  Abaixo seguem alguns exemplos de comentários que trazem pelo menos umas das vinte palavras mais comuns:

  ```
  Vendedor confiável, produto ok e entrega antes do prazo.
  -------
  Recebi exatamente o que esperava. As demais encomendas de outros vendedores atrasaram, mas esta chegou no prazo.
  -------
  A entrega foi dividida em duas. Não houve comunicado do loja. Cheguei a pensar que só haviam enviado parte do produto. 
  -------
  Gostei da atenção com a entrega
  -------
  Produto perfeito, entrega rápida. Estou satisfeitíssima. 👏🏽
  --------
  Muito bom o produto, melhor que esperava e foi entregue no prazo, gostei bastante.
  ```

  Pelo exemplo acima, observa-se que as palavras mais comuns aparecem tanto em comentários bons quanto ruins. Dessa forma, também foi avaliado a frequência com que cada palavra aparecia nos comentários separados pela avaliação de estrelas que este recebeu [^4]. Esta análise mostra a distribuição das palavras nos comentários. Nestas distribuições, observa-se que o uso de adjetivos positivos como "bom" e "antes" aparecem entre as cinco mais comuns para avalições de 5 e 4 estrelas, jantamente com palavras relacionadas ao serviço de entrega. Nas avaliações neutras, (3 estrelas), os adjetivos ainda aparecem, porém caindo para as posições mais intermediárias. Enquanto isso, nas avalições mais baixas (1 e 2 estrelas), adjetivos, mesmo que negativos, quase não aparecem na lista, dando lugar para verbos de ação ("entergue", "veio", "recebi") e substantivos ("compras", "loja", "entrega").

  ### Análise estatística

</details>

<details> 

  <summary> Conclusão </summary>

  - Rever a política de cálculo de prazo de entrega
  
</details>

[^1]: Veja a aba `revisões` no arquivo `Ecommerce-ollist.pbix`.
[^2]: Veja a aba `media_palavras` no arquivo `Ecommerce-ollist.pbix`.
[^3]: Veja a aba `word_cloud_geral` no arquivo `Ecommerce-ollist.pbix`.
[^4]: Veja as abas `soma_relativa_score` e `soma_relativa_por_score` no arquivo `Ecommerce-ollist.pbix`.
