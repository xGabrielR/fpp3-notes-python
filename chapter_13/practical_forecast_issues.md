### Alguns problemas práticos em previsão


---


#### Weekly, daily e sub-daily data

---

**Dados semanais / Weekly**


Dados semanais são difíceis de trabalhar por causa do período sazonal (número de semanas no ano), além de ser grande não é um inteiro, pode variar em média 52.18 e muitas aproximações exigidas pelos métodos (dos que funcionam) são utilizadas com um período de 52 mas muitos deles não dão conta com um período sazonal muito grande, essa discussão foi citada e envolvida em detalhes no capítulo 10 e no capítulo 3.

Existem algumas ferramentas que podemos utilizar para trabalhar nesses conjuntos de dados, talvez a mais simples e fácil de implementar seja utilizar regressão dinâmica, entretanto é preciso limitar os componentes PDQ para (0, 0, 0) para que o Arima não tente trabalhar na sazonalidade e sim apenas no $\eta_t$ ou uma decomposição STL utilizando dados sazonalmente ajustados.

Por exemplo, utilizando regressão dinâmica, conseguimos obter um arima(0, 1, 1) com o seguinte código em R:

```r
gas_dhr = us_gasoline |> model(dhr=ARIMA(Barrels ~ PDQ(0,0,0) + fourier(K=6)))
```

O livro já traz a fórmula do par $K$ se séries de fourier utilizadas.

$$
y_t = bt + \sum_{j=1}^{6}
   \left[
     \alpha_j\sin\left(\frac{2\pi j t}{52.18}\right) +
     \beta_j\cos\left(\frac{2\pi j t}{52.18}\right)
   \right] +
   \eta_t
$$

Já para o STL, seguido da decomposição, segue o seguinte código em R:

```r
my_dcmp_spec = decomposition_model(
 STL(Barrels),
 ETS(season_adjust ~ season("N"))
)


us_gasoline |>
 model(stl_ets=my_dcmp_spec) |>
 forecast(h="2 years") |>
 autoplot(us_gasoline) +
 labs(
   y="Millions of barrels per day",
   title="Weekly US gasoline production"
)
```

A abordagem STL é preferível quando a sazonalidade muda ao longo do tempo. A abordagem de regressão harmônica dinâmica é preferível se existirem covariáveis que sejam preditores úteis, uma vez que estas podem ser adicionadas como regressores adicionais.


**Dados diários / Daily**

Dados diários ou sub-diários (de hora em hora, meia em meia hora, minuto a minuto...) são desafiadores pois envolvem múltiplos padrões de sazonalidade e precisamos de métodos que deem conta dessa complexa sazonalidade.

Se a série é relativamente pequena é possível lidar com modelos mais tradicionais como ETS e Arima, entretanto para longos períodos é importante testar modelos como o STL, dynamic harmonic regression ou Prophet, e é claro, podemos fazer ajustes de calendário ou ajustes de sazonalidade para lidar com isso caso seja possível no problema de negócio.

Já para incluir sazonalidades externas como estações do ano, holidays, etc, é possível utilizar as variáveis dummy citadas no capítulo 4.


#### Séries temporais de contagens

---

Todos os métodos discutidos no livro assumem que os dados têm um espaço amostral contínuo. Mas muitas vezes os dados vêm na forma de contagens. Por exemplo, podemos desejar prever o número de clientes que entram numa loja todos os dias. Poderíamos ter 0, 1, 2, clientes, mas não podemos ter 3,45693 clientes.

Na prática, isto raramente importa, desde que as nossas contagens sejam suficientemente grandes. Se o número mínimo de clientes for pelo menos 100, então a diferença entre um espaço amostral contínuo [100, ∞) e o espaço amostral discreto {100, 101, 102,...} não tem efeito perceptível em nossas previsões.

No entanto, se nossos dados contiverem contagens pequenas (0, 1, 2, ...) , então precisaremos usar métodos de previsão que sejam mais apropriados para um espaço amostral de inteiros não negativos. Tais modelos estão além do escopo do livro.

No entanto, existe um método simples que é utilizado neste contexto queé o "método de Croston", em homenagem ao seu inventor britânico, John Croston, e descrito pela primeira vez em Croston (1972). Este método também não lida adequadamente com a natureza da contagem dos dados, mas é usado com tanta frequência que vale a pena conhecê-lo.

Com o método de Croston, construímos duas novas séries a partir da nossa série temporal original, observando quais períodos contêm valores zero e quais períodos contêm valores diferentes de zero.

É definido $q_i$ para ser o valor $i$ésimo maior que zero e $a_i$ o tempo entre $q_{i-1}$ e $q_i$, após isso, o método de Croston irá previsoes SES (Simple Exponential Smoothing) para as duas novas séries.

Como o método é geralmente aplicado a séries temporais de demanda por itens, $q$ é frequentemente chamado de "demanda" e $a$ de "tempo entre chegadas".

Baseado na demanda $i$, e com os parâmetros de suavização $a_a$ e $a_q$, a próxima previsão dos dois componentes é dado pela fórmula do SES:

$$
\begin{align}
  \hat{q}_{i+1|i} & = (1-\alpha_q)\hat{q}_{i|i-1} + \alpha_q q_i, \tag{13.1}\\
  \hat{a}_{i+1|i} & = (1-\alpha_a)\hat{a}_{i|i-1} + \alpha_a a_i. \tag{13.2}
\end{align}
$$

A Fórumla para a previsão do h + 1 utilizando os componentes previstos é dado por:

$$
\begin{equation}\label{c2ratio}
  \hat{y}_{T+h|T} = \hat{q}_{j+1|j}/\hat{a}_{j+1|j}.
\end{equation}
$$

Por fim, o autor deixa a seguinte afirmação, *"There are no algebraic results allowing us to compute prediction intervals for this method, because the method does not correspond to any statistical model (Shenstone & Hyndman, 2005)."*
Existem outros métodos para previsão de time series intermitentes.

#### Combinação de Previsões

---

Existe um conceito em Machine Learning tradicional chamado stacking, onde, múltiplos modelos podem gerar uma previsão mais acurada, em time séries também é possível utilizar essa mesma técnica a fim de obter previsões mais acuradas.

"Os resultados foram praticamente unânimes: a combinação de múltiplas previsões leva a uma maior precisão das previsões.  Em muitos casos, é possível obter melhorias dramáticas no desempenho simplesmente calculando a média das previsões."


**Referências**


- [1] <a href="https://otexts.com/fpp3/practical.html">Fpp3 Book Practical Issues</a>.
- [2] <a href="https://forecastegy.com/posts/intermittent-time-series-forecasting-in-python/#intermittent-multiple-aggregation-prediction-algorithm-imapa">Forecastegy, Intermittent Forecast</a>