## Desafio
O desafio propõe que seja feita a previsão do crescimento do índice GDP de cada país para os anos entre 2024 e 2028. Posteriormente, os dados devem ser comparados com as previsões do Statista. 

#### Etapas de análise dos dados
A partir da coleta dos dados, por meio de um arquivo csv disponibilizado para o desafio, foi feita a análise e observação do conjunto de dados para entendimento de comportamentos intrínsecos dos dados, identificacação de padrões, tendências e possíveis anomalias.

Durante a análise inicial, foi possível compreender a natureza dos dados, o explorar sua estrutura, características e distribuições. Além disso, foi dedicada especial atenção à detecção de valores ausentes. A identificação precisa de tais valores foi crucial para garantir a qualidade dos resultados obtidos em análises subsequentes.

A partir disso, os dados de grupos de países com valores faltantes foram plotados em gráficos de linha para observação do comportamento ao longo do tempo. A ideia aqui também foi entender se, por fazer parte do mesmo grupo de países, poderiam apresentar comportamentos de tendência e sazonalidade semelhantes. 

#### Estratégias para preencher os dados faltantes

Após identificação dos países que apresentavam dados faltantes, foi considerada as seguintes estratégias para preenchimento dos valores nulos:

1.	Quando um país tinha apenas um ou dois dados faltantes, os campos nulos foram preenchidos com a média de todos os valores disponíveis para aquele país. Trata-se de um método confiável para esse tipo de situação.

2.	Dois novos agrupamentos de países foram considerados para esta etapa. Países que fizeram parte da antiga união soviética tinham informações do PIB a partir de 1991, com exceção de Belarus. Para este grupo, os valores do índice GPD foram preenchidos com o mesmo valor de Belarus para o ano de 1980.  Em seguida, foi feita uma interpolação dos valores ausentes para todos os países, com o objetivo de manter uma tendência de crescimento semelhante. 

4.	O mesmo método foi aplicado para o grupo de países que fizeram parte da antiga Iugoslávia, sendo que os dados foram preenchidos com informações do grupo Eastern Europe. 

4.	Para os demais países com dados faltantes, a substituição foi feita da seguinte forma: A partir do cálculo da média dos países do mesmo grupo, foi feita uma contagem para observar se o país tinha dados em sua maioria acima ou abaixo dessa média. Caso o resultado fosse acima da média, os valores nulos seriam preenchidos com a média do grupo somado ao desvio padrão do país. Por outro lado, se fosse abaixo da média do grupo, seria considerada a média do grupo subtraído o valor do desvio padrão do país.

#### Teste de estacionariedade	

Para a avaliação da estacionariedade dos dados, optamos por empregar o teste Augmented Dickey-Fuller (ADF). Os resultados revelaram que aproximadamente 81,9% dos dados apresentaram características estacionárias, enquanto 18,1% não demonstraram essa propriedade.

É importante destacar que, dada a natureza dos dados econômicos, a escolha de concentrar nossos esforços na modelagem baseada exclusivamente nos dados estacionários foi orientada pelo resultado do teste ADF. O fenômeno de estacionariedade denota que as propriedades estatísticas dos dados mantêm-se constantes ao longo do tempo, um aspecto essencial para viabilizar a aplicação de técnicas analíticas e, por conseguinte, garantir uma interpretação confiável dos resultados obtidos.

### Modelagem dos dados

Para esta etapa, foram usados dois modelos de análise de séries temporais, sendo eles: Simple Exponential Smoothing e Auto_Arima. Os modelos foram treinados com dados de 1980 a 2023 e testados com dados de 2024 a 2028.

### Métricas de performance

Para obter a performance de cada modelo foram utilizadas as seguintes métricas de avaliação: MAE (Erro Médio Absoluto) e RMSE (Raiz do Erro Quadrático Médio) O MAE foi utilizado como métrica principal, enquanto RMSE como métrica secundária.

Para análise de desempenho dos modelos, considerando cada país e região, as métricas de desempenho foram calculadas e avaliadas especificamente para cada caso. Como critério de seleção, optou-se por calcular a média do Erro Absoluto Médio (MAE) para todos os países e regiões. Essa abordagem possibilitou uma comparação abrangente entre os diferentes modelos, proporcionando uma visão geral da eficácia relativa de cada um. O modelo com a melhor performance foi o Simple Exponential Smoothing, portanto escolhido como modelo final. 

### Comparação os dados do Statista

Amostra de dados previstos pelo Statista:

|   year |   Sub-Saharan Africa (Region) |   Western Hemisphere (Region) |   ASEAN-5 |   Advanced economies |   Emerging and Developing Asia |   Emerging and Developing Europe |   Emerging market and developing economies |   Euro area |   European Union |   Latin America and the Caribbean |   Major advanced economies (G7) |   Middle East and Central Asia |   Other advanced economies |   Sub-Saharan Africa |   World |
|-------:|-----------------------------:|-----------------------------:|----------:|--------------------:|-------------------------------:|----------------------------------------:|-----------------------------------:|------------:|----------------:|----------------------------------:|----------------------------:|-------------------------:|----------------------:|-----------------:|--------:|
|   2024 |                          4.1 |                          1.4 |       4.6 |                 1.4 |                            5.1 |                                     2.5 |                                4.2 |         1.4 |             1.6 |                               2.2 |                         1.1 |                     3.5 |                 2.2 |             4.2 |       3 |
|   2025 |                          4.1 |                          1.9 |       4.6 |                 1.8 |                            4.8 |                                     2.5 |                                4   |         1.9 |             2.2 |                               2.3 |                         1.7 |                     3.6 |                 2.3 |             4.1 |     3.2 |
|   2026 |                          4.1 |                          2.2 |       4.6 |                 1.9 |                            4.7 |                                     2.4 |                                4   |         1.7 |             2   |                               2.6 |                         1.8 |                     3.6 |                 2.3 |             4.2 |     3.2 |
|   2027 |                          4.3 |                          2.2 |       4.5 |                 1.8 |                            4.5 |                                     2.3 |                                3.9 |         1.5 |             1.8 |                               2.3 |                         1.7 |                     3.7 |                 2.2 |             4.3 |     3.1 |
|   2028 |                          4.3 |                          2.2 |       4.6 |                 1.8 |                            4.4 |                                     2.3 |                                3.9 |         1.4 |             1.7 |                               2.3 |                         1.6 |                     3.7 |                 2.3 |             4.4 |       3 |


Amostra de dados previstos pelo modelo:

O resultado final das previsões feitas pelo modelo são um tanto quanto mais conservadoras na comparação com o Statista, contudo, ambos seguem a mesma linha de tendência, principalmente quando observados os dados para grupos de países da Ásia e Américas, em que há maior previsão de crescimento do índice GDP, enquanto grupos de países da Europa, por exemplo, as precisões para as taxas de crescimento são inferiores, provavelmente porque estes grupos têm sido mais afetados pela guerra entre Rússia e Ucrânia, além dos impactos da Covid. 


|   year |   Sub-Saharan Africa (Region) |   Western Hemisphere (Region) |   ASEAN-5 |   Advanced economies |   Emerging and Developing Asia |   Emerging and Developing Europe |   Emerging market and developing economies |   Euro area |   European Union |   Latin America and the Caribbean |   Major advanced economies (G7) |   Middle East and Central Asia |   Other advanced economies |   Sub-Saharan Africa |   World |
|-------:|-----------------------------:|-----------------------------:|----------:|--------------------:|-------------------------------:|----------------------------------------:|-----------------------------------:|------------:|----------------:|----------------------------------:|----------------------------:|-------------------------:|----------------------:|-----------------:|--------:|
|   2024 |                         3.41 |                          2.03 |      4.23 |                 1.79 |                            6.17 |                                     2.55 |                                4.42 |         1.32 |             1.61 |                               1.97 |                         1.57 |                     3.29 |                 2.77 |             3.54 |     3.22 |
|   2025 |                         3.41 |                          2.03 |      4.23 |                 1.79 |                            6.17 |                                     2.55 |                                4.42 |         1.32 |             1.61 |                               1.97 |                         1.57 |                     3.29 |                 2.77 |             3.54 |     3.22 |
|   2026 |                         3.41 |                          2.03 |      4.23 |                 1.79 |                            6.17 |                                     2.55 |                                4.42 |         1.32 |             1.61 |                               1.97 |                         1.57 |                     3.29 |                 2.77 |             3.54 |     3.22 |
|   2027 |                         3.41 |                          2.03 |      4.23 |                 1.79 |                            6.17 |                                     2.55 |                                4.42 |         1.32 |             1.61 |                               1.97 |                         1.57 |                     3.29 |                 2.77 |             3.54 |     3.22 |
|   2028 |                         3.41 |                          2.03 |      4.23 |                 1.79 |                            6.17 |                                     2.55 |                                4.42 |         1.32 |             1.61 |                               1.97 |                         1.57 |                     3.29 |                 2.77 |             3.54 |     3.22 |



