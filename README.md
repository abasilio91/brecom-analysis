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

  Como cenário hipotético temos que uma empresa do ramo de e-commerce, com grande volume de vendas mensais deseja identificar eventual(is) ponto(s) que configure(m) obstáculos a uma melhor performance nas vendas e, para isso, contratou a nossa empresa de consultoria para apontar problemas e propor soluções.

  A empresa contratante é a Olist Serviços Digitais, uma empresa que funciona como uma loja de departamentos dentro dos maiores marketplaces do país, onde os seus clientes não são apenas os compradores finais, mas as pessoas físicas e empresas que ofertam seus produtos através das lojas online da Olist.

  Em outros termos, a pessoa que deseja vender nas lojas online da Olist contrata um plano, em que é pago pelo contratante uma comissão a cada venda realizada, e a empresa contratada, a Olist, divulga esses produtos em todas as suas lojas naqueles principais marketplaces do Brasil, intermediando aspectos como o frete, por exemplo, evitando que o cliente tenha que gerenciar suas lojas virtuais em cada um dos marketplaces do mercado, como o Mercado Livre, Amazon, Americanas, dentre outros.

  Voltando ao cenário hipotético, nossa empresa de consultoria recebeu da Olist um dataset com aproximadamente 100 mil registros, referentes aos anos de 2016 a 2018, onde constam diversos dados sobre os pedidos realizados pelos clientes em suas lojas virtuais, como preços, produtos, status quanto à entrega, avaliações dos clientes, dados sobre os vendedores (contratantes da Olist), endereço do comprador, dentre outros.

  O trabalho da nossa empresa de consultoria foi iniciado tendo em vista duas hipóteses: (1) a implantação de um Centro de Distribuição poderia ser fator de otimização do tempo de entrega dos produtos e (2) as avaliações têm grande impacto sobre recompras e sobre o encorajamento à efetivação da compra por parte de visitantes das páginas onde estão expostos os produtos.
  
</details>

<details> 

  <summary> Metodologia </summary>

  Para a primeira hipótese (implantação de um Centro de Distribuição), decidimos que seria importante analisarmos a distribuição dos vendedores pelo país, contratantes da Olist, de onde partem os produtos vendidos nas lojas online, e a distribuição dos consumidores finais dos produtos, e para a segunda hipótese (impacto das avaliações dos clientes) decidimos pela realização de uma análise qualitativa dos comentários deixados pelos clientes em relação aos produtos comprados, inclusive o rating conferido por eles.
  
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

  Por fim, para avaliar a eficiência de entregas, foi realizada uma análise da contagem de vendas dentro e fora do prazo por estado, tanto por consumidor quanto por fornecedor [^5]. Nesta análise, foi observado que os estados com o maior número de consumidores e fornecedores (SP), é também o estado onde se concentram a maior quantidade de pedidos com atraso. Apesar de ser um resultado esperado pelo grande volume de vendas, era esperado também que, se fosse um problema de distribuição de produtos, os consumidores que residem mais afastados dos fornecedores experimentassem maiores problemas de entregas.

</details>

<details> 

  <summary> Conclusão </summary>

  Uma das sugestões levantadas no início do trabalho foi a da criação de Centros de Distribuição em diferentes localidades. No entanto, como foi observado que pela análise de contagem de vendas dentro e fora do prazo, os problemas de atraso ocorrem mesmo dentro de um mesmo estado e, por enquanto, não há evidências suficientes para corroborar o investimento neste tipo de empreendimento.

  Dado que existe um considerável gargalo no processo de entrega dos produtos e considerando discussões internas do grupo, chegou-se ao concenso que é melhor rever a forma como o prazo de entrega é calculado para as compras de forma que o prazo final informado seja maior daquele que é informado atualmente. É válido apontar que, para o usuário, a experência de receber uma entrega antes do prazo é extramente valiosa, portanto, é mais vantajoso informar um prazo de entrega maior com a possibilidade de recebimento antecipado do que informar um prazo de entrega curto, mas com alta possibilidade de atraso.

</details>

[^1]: Veja a aba `revisões` no arquivo `Ecommerce-ollist.pbix`.
[^2]: Veja a aba `media_palavras` no arquivo `Ecommerce-ollist.pbix`.
[^3]: Veja a aba `word_cloud_geral` no arquivo `Ecommerce-ollist.pbix`.
[^4]: Veja as abas `soma_relativa_score` e `soma_relativa_por_score` no arquivo `Ecommerce-ollist.pbix`.
[^5]: Veja a aba `contagem_vendas_prazo` no arquivo `Ecommerce-ollist.pbix`.
