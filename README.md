# Otimização para minimizar a emissão de CO2 na rota das embarcações para alívio de plataformas.

#### Aluno: [Vinícius Alves da Silva](https://github.com/vinirio10)
#### Orientador: [Felipe Borges](https://github.com/FelipeBorgesC)

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/vinirio10/BIMaster-TCC).

---

### Resumo

Considerando o cenário atual no Brasil do alto consumo de combustíveis fósseis como fonte de energia, a descarbonização surge como uma potencial alternativa.

O presente estudo tem como objetivo otimizar a frota disponível, visando a menor emissão de CO2 nas rotas das embarcações de um porto até uma plataforma. Esse processo agrega valor ao negócio, além de contribuir com a saúde e meio ambiente.

### Abstract

Considering the current scenario in Brazil of high consumption of fossil fuels as an energy source, decarbonization emerges as a potential alternative.

The current study has the aim to optimize the available fleet of ships, aiming at lower CO2 emissions in the routes of ships from a port to a platform. This process adds value to the business, in addition to contributing to health and the environment.

### 1. Introdução

Para realizar o estudo foram utilizadas três disciplinas:
- Web Scraping: Após a seleção manual de forma aleatória de dez portos do site: https://navalportoestaleiro.com/portos-do-brasil-conheca-as-principais-instalacoes-portuarias-existentes-no-pais/ foi desenvolvido um código em Python (Scrapping_MarineTraffic.ipynb) aplicando a técnica de Web Scraping no site: https://www.marinetraffic.com/, para obter o posicionamento (latitude e longitude) de cada porto.
- Otimização: Foi desenvolvido um código em Python para esse problema de rota, tendo como função objetivo a minimização da emissão de CO2.
- Visualização de dados com Power BI: Foi desenvolvido o painel em Power BI para exibir geograficamente as rotas das Embarcações.

Os dados de Embarcações e Plataformas (incluíndo sua localização) são fictícios. 

### 2. Modelagem

No estudo, após a realização da raspagem de dados (Web Scraping) foi utilizado a GeographicLib API (https://geographiclib.sourceforge.io/html/python/code.html) para calcular a distância entre os pontos (Porto e Plataforma) em quilômetros (km) e depois foi feita a conversão para milhas náuticas (mn). O algoritmo utilizado para calcular a distância e traçar a rota, leva em consideração a criação de pontos intermediários (no mar), caso entenda que a reta simples entre origem (Porto) e destino (Plataforma) possa passar por terra.
O modelagem da otimização com algoritmo genético foi feita em Python (Otimização Python.ipynb) utilizando DEAP (https://deap.readthedocs.io/en/master/). Na toolbox ("caixa de ferramentas") após a realização de diversos testes, a combinação de parâmetros que obteve o melhor resultado foi:
- Geração de números aleatórios: random.sample
- Cruzamento: tools.cxOrdered
- Mutação: tools.mutShuffleIndexes
- Seleção: tools.selTournament
- Tamanho da população: Quinhentos indivíduos
- Quantidade de gerações: Cinquenta gerações

Além dos parâmetros acima, foi utilizada a classe HallOfFame para selecionar o melhor indivíduo da população durante o processo de evolução.

### 3. Resultados

Para demonstrar o ganho com a otimização, foi gerado um cenário inicial (Cenário Inicial.ipynb), onde foi definido visualmente qual seria a melhor rota para cada Embarcação.

Tanto no cenário inicial, quanto na otimização foi gerado no código Python, um arquivo de saída para ser carregado no Power BI. Para se chegar no cálculo da emissão de CO2 foram utilizadas as seguintes fórmulas:

Tempo = Distancia (cálculo citado na Modelagem do estudo) / Velocidade (informação da Embarcação) / 24 (horas por dia)

Emissao = Tempo * Consumo (informação da Embarcação) * 3.18 (transformação do consumo de combustível para emissão de CO2)

No Power BI (TCC.pbix), para exibir a rota foram criadas duas visões (cenário inicial e otimização) utilizando o componente Rout map (https://appsource.microsoft.com/en-us/product/power-bi-visuals/wa104380985).

Os resultados obtidos para cada cenário foram:
- Cenário inicial: ~3.98 toneladas de CO2
- Cenário otimizado: ~3.37 toneladas de CO2

### 4. Conclusões

Após as diversas rodadas para definir os melhores parâmetros e obter a melhor rota para atender a função objetivo (minimização da emissão de CO2), foi obtida uma redução de aproximadamente 15% na emissão de CO2 em comparação com o cenário inicial. Dito isto, entendemos que o modelo é válido e obviamente pode ser evoluido para atender premissas e restrições específicas de cada problema.

---

Matrícula: 211.101.188

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
