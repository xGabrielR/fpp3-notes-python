### Caixa de Ferramentas

---

#### Tidy Workflow

---

O "Tidy" é um processo cíclico de desenvolvimento de projetos de time series.


Tidy -> [Visualize -> Specify -> Estimate -> Evaluate] -> Forecast


##### Data preparation (Tidy)

---

Tudo começa no Tidy, onde é a preparação do dado, isso envolve responder todas as perguntas do capítulo 1 a fim de montar o dataset ideal nesta etapa.
Após a definição das respostas para as perguntas do capítulo 1, iniciamos a preparação dos dados, como carregar os dados, identificar valores ausentes, identificar outliers, filtrar a serie, resumos estatísticos, e outros pré-processamentos.


```r
global_economy <- read.csv('data/file.csv', header=TRUE, sep=',',  stringsAsFactors=FALSE)


gdppc <- global_economy |> mutate(GDP_per_capita = GDP / Population)
```


##### Data Visualization (Visualize)

---

No capítulo 2 foi ensinado várias formas de visualizar os dados de time series, é uma etapa importante, desde para entender o conjunto de dados até para posteriormente selecionar transformações e estimadores adequados.


```r
gdppc |> filter(Country == 'Sweden')
     |> autoplot(GDP_per_capita) + labs(y="$US", title="GDP per capita for Sweden")
```


##### Define a Model (Specify)

---

Existem vários modelos que fazem previsões.
Modelos no Statsmodels do Python ou em Fable do R, especificamos uma fórmula (y ~ x), onde a variável resposta é especificada no y e a estrutura é especificada em x.
Neste caso abaixo em R é utilizado o TSLM (Time series linear model), a variável resposta é GDP_per_capita e está sendo modelado pela `trend()`.


```r
TSLM(GDP_per_capita ~ trend())
```


##### Train the Model (Estimate)

---

Após especificar o modelo, está na hora de treinar ele, em R é estimado pela função `model()`. A variável fit é um objeto do tipo `mable` (model table), ele automaticamente endereça múltiplas time series, pois neste dataset existem vários países e o modelo treinou com todos os países e é possível recuperar as previsões para cada um dos países.


```r
fit <- gdppc |> model(trend_model=TSLM(GDP_per_capita ~ trend()))
```


##### Check model performance (Evaluate)

---

Agora é necessário avaliar o modelo utilizando métricas de avaliação dos modelos e diagnósticos de regressão.


##### Produce forecasts (Forecast)

---

Para obter as previsões, utilizamos a função `forecast()` com um horizonte de previsão (h) que pode ser um número (3) ou uma string ("3 years"), o retorno vai ser um objeto do tipo `fable`.
Cada linha representa a previsão para cada um dos períodos, a coluna GDP_per_capita contém a distribuição de previsão e a coluna .mean contém o point forecast, que é a média da distribuição de previsão, ou $\hat{y_t}$.
E pode ser plotado com o autoplot.


```r
forecast_table <- fit |> forecast(h='3 years')


forecast_table |> filter(Country='Sweden')
              |> autoplot(gdppc) + labs(y='$US', title='GDP per capita for Sweden')
```
