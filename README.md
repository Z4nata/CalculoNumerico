# Cálculo Numérico

Atividades práticas da disciplina de Cálculo Numérico — Ciência da Computação, UNIFESP.

Cada atividade é um notebook em **Python** (NumPy, pandas, Matplotlib) que parte de um
problema físico e mede, com números e gráficos, quanto a representação numérica afeta o
resultado.

| Atividade | Tema | Abrir |
| --- | --- | --- |
| [I — Erros numéricos em biofluidodinâmica](Atividade_1.ipynb) | truncamento × arredondamento, propagação de erro, float32 × float64 | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_1.ipynb) |
| [II — Estabilidade numérica e overflow em CFD](Atividade_2.ipynb) | critério de estabilidade, overflow, refinamento de malha | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_2.ipynb) |
| [III — Zeros de funções](atividade_3.ipynb) | bisseção, Newton e secante, critérios de parada e casos de falha | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/atividade_3.ipynb) |
| [IV — Animação da eliminação de Gauss](Atividade_4.ipynb) | eliminação sem pivoteamento, multiplicadores, retrossubstituição | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_4.ipynb) |
| [V — Sistemas lineares](Atividade_5.ipynb) | forma Ax = b, eliminação de Gauss, classificação de sistemas, balanço térmico | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_5.ipynb) |

## Atividade I — Erros numéricos em biofluidodinâmica

- **Truncar × arredondar:** compara os dois em vários valores e números de casas decimais.
- **Pressão arterial:** mede se guardar as medidas como inteiros preserva a média e a
  variabilidade da amostra.
- **Vazão num tubo fino (Hagen-Poiseuille):** como a vazão depende de r⁴, um erro pequeno no
  raio é amplificado cerca de quatro vezes na vazão (dQ/Q ≈ 4·dr/r). O notebook mostra isso
  numa varredura do raio.
- **Nanocateter:** repete a análise em escala de nanômetros e compara `float32` com `float64`
  à medida que a variação relativa do raio diminui.
- Fecha com um quadro-síntese e uma animação do efeito.

## Atividade II — Estabilidade numérica e overflow em CFD simplificado

Simulação do perfil de velocidade de um fluido entre placas (difusão explícita):

- **Estabilidade:** calcula antes de rodar se cada caso respeita o limite
  r = ν·Δt/Δy² ≤ 1/2, e confirma na simulação.
- **Overflow:** nos casos instáveis, acompanha max|u| crescer até o limite de cada tipo
  (~10³⁸ no `float32`, ~10³⁰⁸ no `float64`).
- **Refinamento de malha:** dobrar os pontos da malha torna instável um Δt que antes era
  estável; o notebook encontra um novo Δt que funciona.
- **Verificação:** compara o perfil final com a solução estacionária analítica, com erro
  máximo da ordem de 10⁻⁹ m/s.

## Atividade III — Zeros de funções

Bisseção, Newton e secante aplicados a quatro funções (x² − 2, x³ − x − 2, e⁻ˣ − x e
x³ − 2x + 2):

- **Implementação:** critério de parada com |x<sub>k+1</sub> − x<sub>k</sub>| e
  |f(x<sub>k+1</sub>)| abaixo da tolerância e tratamento das falhas de cada método
  (f(a)·f(b) > 0, f'(x) ≈ 0, denominador nulo na secante, limite de iterações).
- **Tabela:** raiz, resíduo final e número de iterações de cada método em cada função.
- **Animações:** as iterações da bisseção, de Newton e da secante desenhadas sobre o gráfico
  da função.

## Atividade IV — Animação da eliminação de Gauss

Resolve um sistema 3×3 por eliminação de Gauss e retrossubstituição e gera um GIF que
explica cada passo:

![Animação da eliminação de Gauss](animacoes/eliminacao_gauss.gif)

- **Eliminação:** destaca o pivô de cada coluna, calcula o multiplicador
  m<sub>ik</sub> = a<sub>ik</sub>/a<sub>kk</sub> e anima a operação L<sub>i</sub> ← L<sub>i</sub> − m<sub>ik</sub>·L<sub>k</sub>,
  com a conta de cada elemento.
- **Retrossubstituição:** resolve o sistema triangular de baixo para cima e preenche o vetor
  solução.
- **Verificação:** confere a solução no sistema original e compara com `numpy.linalg.solve`.
- Para animar outro sistema, basta trocar `A` e `b` no início do notebook.

## Atividade V — Sistemas lineares

Lista de exercícios resolvida à mão e em Python, com teoria e dicas da linguagem em cada passo:

- **Forma matricial:** monta A, x e b de sistemas 2×2 e 3×3.
- **Eliminação de Gauss manual:** matriz aumentada em cada etapa, multiplicadores e
  retrossubstituição (solução x = 2, y = 3, z = −1).
- **Número de soluções:** classifica sistemas como única, infinitas ou nenhuma solução pela
  matriz escalonada e pelo posto (Rouché–Capelli).
- **Implementação:** função `eliminacao_gauss` sem pivoteamento, comparada com
  `numpy.linalg.solve`, e um exemplo de pivô nulo mostrando a limitação do método.
- **Balanço térmico:** sistema tridiagonal diagonalmente dominante (T₁ = T₂ = T₃ = 5).

## Como rodar

Clique em **Abrir no Colab** na tabela acima: roda no navegador, sem instalar nada.

Para rodar localmente:

```bash
pip install numpy pandas matplotlib pillow jupyter
jupyter notebook
```
