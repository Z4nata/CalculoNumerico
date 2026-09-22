# Cálculo Numérico

Atividades práticas da disciplina de Cálculo Numérico — Ciência da Computação, UNIFESP.

Cada atividade é um notebook em **Python** (NumPy, pandas, Matplotlib) que parte de um
problema físico e mede, com números e gráficos, quanto a representação numérica afeta o
resultado.

| Atividade | Tema | Abrir |
| --- | --- | --- |
| [I — Erros numéricos em biofluidodinâmica](Atividade_1.ipynb) | truncamento × arredondamento, propagação de erro, float32 × float64 | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_1.ipynb) |
| [II — Estabilidade numérica e overflow em CFD](Atividade_2.ipynb) | critério de estabilidade, overflow, refinamento de malha | [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Z4nata/CalculoNumerico/blob/main/Atividade_2.ipynb) |

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

## Como rodar

Clique em **Abrir no Colab** na tabela acima: roda no navegador, sem instalar nada.

Para rodar localmente:

```bash
pip install numpy pandas matplotlib pillow jupyter
jupyter notebook
```
