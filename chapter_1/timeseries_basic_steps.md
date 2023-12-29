### As etapas básicas de uma tarefa de previsão


---


#### O'Que Podemos Prever ?


---


As previsões são necessárias em todos os momentos e em muitas áreas, pois ajudam na tomada de decisão. Desde prever se o sol vai aparecer amanhã até a demanda de energia, produtos, etc. No entanto, existem coisas que são mais fáceis de prever do que outras. Para identificarmos o que podemos prever, existem algumas perguntas que precisam ser respondidas, são elas:


1. O quão bem conhecemos os fatores que contribuem para o'que queremos prever;
2. Quantos dados existem disponíveis;
3. O Quão similar o passado é com o presente dos dados;
4. As previsões podem afetar aquilo que estamos tentando prever;


Exemplo 1, Previsão do sol amanhã, depende de algumas perspectivas, se for apenas o sol ou se é a previsão de um tempo nublado, chuvoso ou não, assumindo que é apenas a previsão do sol independente de outros fatores, então as quatro características já podem ser descritas:


1. Previsões do tempo de vida do sol, historicamente desde o início sempre aparece.
2. Muitos dados históricos.
3. Sempre.
4. Outros fatores que contribuem para a previsão se vai aparecer o sol amanhã ou não, depende da pergunta, se for uma pergunta relacionada ao dia "limpo", sem nuvens, podemos prever se vai chover amanhã ou não, essa é uma das previsões que afetam aquilo que queremos prever.


Exemplo 2 (Livro), Previsões de curto prazo da demanda / procura de eletricidade residencial também podem ser precisas pois os quatro fatores são normalmente satisfeitos.


1. Existem alguns fatores, como a temperatura, variação de calendário e condições econômicas.
2. Geralmente existem vários anos de dados sobre a procura de eletricidade e também da temperatura.
3. Para previsões de curto prazo é razoável assumir que as previsões futuras são bem similares às do passado mais próximo.
4. Outros fatores que contribuem para a previsão da demanda de eletricidade, uma das previsões é o preço da eletricidade que não depende da demanda (requer análises se essa afirmação do livro é aplicada em todos os casos) e outras variáveis de previsão que podem ser incluídas.


*"Desde que tenhamos as competências necessárias para desenvolver um bom modelo que ligue a demanda de eletricidade e as principais variáveis ​​determinantes, as previsões podem ser notavelmente precisas, pois não é apenas lançar uma moeda para cima boas previsões captam os padrões e relações que existam nos dados históricos, assim conseguimos extrapolar e prever o futuro."*


Por outro lado, previsões como taxa de câmbio, ações, criptomoedas... Apenas uma das condições é satisfeita, que é a quantidade de dados disponíveis. Contudo, não temos uma boa compreensão dos fatores que afetam essas variáveis a serem previstas ou temos alguma ideia de quais são mas podem ser muitos, o futuro pode ser muito diferente do passado, algum evento possa acontecer, por exemplo o BTC que teve uma explosão dado a um evento que foi a compra de uma corretora próximo da metade do ano em 2023, se não tivesse esse evento externo poderíamos ter um indicativo do preço do BTC dado a os três meses passados que foram "bem parecidos".
Existem hipóteses como o "Efficient Market" que dizem respeito às previsões da taxa de câmbio, que é como prever cara ou coroa em uma moeda.


Aqui estão alguns exemplos de coisas que podemos prever ordenados pela sua dificuldade.


1. Tempo que o Sol irá nascer amanhã.
2. Tempo que o cometa Halley vai aparecer.
3. A temperatura máxima amanhã.
4. Demanda de eletricidade diária para os próximos 3 dias.
5. Quantidade total de remédios farmacêuticos vendidos para o próximo mês.
6. Preço da Ação do Google amanhã.
7. Taxa de câmbio entre US e AUS para a próxima semana.
8. Preço da ação do Google para os próximos 6 meses.




#### Previsão, Metas e Planejamento


---


Previsão: Prever o futuro com maior precisão possível tendo em conta todas as informações disponíveis anteriormente citadas.


Metas: São oque você gostaria que acontecesse. As metas deveriam estar vinculadas a previsões e planos, mas nem sempre isso ocorre. Muitas vezes, as metas são definidas sem qualquer plano sobre como alcançá-las e sem previsões sobre se serão realistas.


Planejamento: Envolve determinar ações necessárias para que as previsões correspondam às metas.


Previsões de curto prazo: Agendamento de produtos, transporte e previsões de demanda.


Previsões de Médio Prazo: Necessidades futuras de recursos (matéria-prima), contratação de máquinas e equipamentos.


Previsões de Longo Prazo: Planejamento estratégico, oportunidades do mercado, fatores ambientais e recursos internos.




#### Determinar Oque Prever


---


Nos estágios iniciais de um projeto de previsão, é necessário saber oque você quer prever.


1. Prever as vendas nível produto, um grupo de produto ou as vendas totais ?


Também é necessário entender mais duas coisas, o intervalo de previsão que vai ser considerado (curto prazo, médio prazo ou longo prazo) e de quanto em quanto tempo as previsões eram realizadas, responder essas perguntas é importante tanto para organizar a automação quanto para selecionar métodos específicos para cada intervalo.




#### Previsão de Dados e Métodos


---


Previsão *Qualitativa* Quando não temos dados ou os mesmos não são relevantes para a previsão.
Previsão *Quantitativa*: Pode ser aplicada quando duas condições são verdadeiras:


1. Dados numéricos passados estão disponíveis;
2. É razoável assumir que padrões do passado continuarão no futuro.


"Tudo oque é observado sequencialmente ao longo do tempo é um Time Series".


Existem alguns métodos de previsão, são eles:


1. O primeiro método mais simples é utilizar o comportamento da própria série levando em conta outras variáveis.
2. O segundo método são os modelos explanatórios, eles ajudam a explicar a como a variação das outras variáveis implica na previsão, por exemplo: DE (Demanda de Energia) = f(temperatura, populações, dia do ano, mês, semana..., erro), o termo "erro" diz respeito a variações aleatórias e efeitos relevantes de outras variáveis que não foram incluídas.
3. O terceiro método são os modelos "mistos" que envolvem a junção dos dois outros métodos descritos acima, mas também são chamados de "dynamic regression models".


Nota, se você for utilizar um modelo explanatório, você precisa prever todas as variáveis utilizadas para realizar as previsões, isso pode ser bastante complexo, essas variáveis (Exogenous variables) podem ser várias, desde budget de marketing até o índice do mês (0: Janeiro, 1: Fevereiro...)




#### Uma tarefa de previsão geralmente envolve cinco etapas básicas.


---


**Etapa 1: definição do problema.**


Muitas vezes, essa é a parte mais difícil da previsão. Definir o problema cuidadosamente requer uma compreensão da maneira como as previsões serão usadas, quem exige as previsões e como a função de previsão se encaixa na organização que exige as previsões. Um "forecaster" precisa passar um tempo conversando com todos que estarão envolvidos na coleta de dados, manutenção de bancos de dados e uso das previsões para planejamento futuro.


**Etapa 2: Coletando informações.**


Sempre são necessários pelo menos dois tipos de informações: (a) dados estatísticos e (b) a experiência acumulada das pessoas que coletam os dados e usam as previsões. Frequentemente será difícil obter dados históricos suficientes para poder ajustar um bom modelo estatístico. Nesse caso, os métodos de previsão usando conhecimento e julgamento podem ser usados. Ocasionalmente, dados antigos serão menos úteis devido a alterações estruturais no sistema que está sendo previsto; então podemos optar por usar apenas os dados mais recentes. No entanto, lembre-se de que bons modelos estatísticos lidarão com melhorias e mudanças nos sistemas; não jogue fora bons dados desnecessariamente.


**Etapa 3: Análise preliminar (exploratória).**


Sempre comece com os gráficos dos dados. Existem padrões consistentes? Existe uma tendência significativa? A sazonalidade é importante? Existe evidência da presença de ciclos de negócios? Existem discrepâncias nos dados que precisam ser explicados por pessoas com conhecimento especializado? Quão fortes são as relações entre as variáveis disponíveis para análise? Várias ferramentas foram desenvolvidas para ajudar nessa análise.


**Etapa 4: Escolhendo e ajustando modelos.**


O melhor modelo a ser usado depende da disponibilidade de dados históricos, da força das relações entre a variável de previsão e quaisquer variáveis explicativas, e a maneira pela qual as previsões devem ser usadas. É comum comparar dois ou três modelos em potencial. Cada modelo é em si um construto artificial que se baseia em um conjunto de premissas (explícitas e implícitas) e geralmente envolve um ou mais parâmetros que devem ser estimados usando os dados históricos conhecidos.


**Etapa 5: Usando e avaliando um modelo de previsão.**


Depois que um modelo é selecionado e seus parâmetros estimados, o modelo é usado para fazer previsões. O desempenho do modelo só pode ser avaliado adequadamente após a disponibilização dos dados para o período de previsão. Vários métodos foram desenvolvidos para ajudar na avaliação da precisão das previsões.


#### Notações / Explicações


---


O Intervalo de Previsão é uma lista de variáveis $y_{t}$ com "alta probabilidade".


A Random Variable, oque tu quer prever: $y_{t}$.


Distribuição de Previsão: $\mathcal{I}$.


A Variável aleatória $y_{t}$ dado que sabemos $\mathcal{I}$: $y_{t}|\mathcal{I}$.


Forecast Variance: $var[y_{t}|\mathcal{I}]$.


Se pegarmos o valor médio de todos os possíveis valores de $y_{t}$ da distribuição de previsão, chegamos no valor médio de previsão: $\hat{y}_t$. Isso é útil, pois se escrevermos $\hat{y}_{t|t-1}$, isso significa a previsão de $y_{t}$ levando em conta todas as observações anteriores $(y_1,\dots,y_{t-1})$.


Podemos pensar a notação acima utilizando passos em $h$, ou seja, $\hat{y}_{T+h|T}$ isso significa a previsão de $y_{T+h}$ levando em conta todas as observações anteriores $y_1,\dots,y_T$ em $h$ passos no tempo $T$.


**Referências**


- [1] <a href="https://otexts.com/fpp3/intro.html">Fpp3 Book Getting Started Chapter!</a>.