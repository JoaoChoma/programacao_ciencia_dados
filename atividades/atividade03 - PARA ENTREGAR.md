---
author: Programação para Ciência e Engenharia de Dados
marp: true
paginate: true
theme: default
title: Atividade 03 --- Vetorização, Carregamento e Exploração de Dados
---

# Atividade 03

## Vetorização, Carregamento e Exploração de Dados

Nesta atividade, você começará a trabalhar com um **conjunto de dados
real em formato tabular**.

O objetivo é percorrer três etapas:

``` text
VETORIZAÇÃO
     ↓
CARREGAMENTO
     ↓
EXPLORAÇÃO
```

------------------------------------------------------------------------

# Objetivos

Ao final da atividade, você deverá ser capaz de:

-   compreender a diferença entre processamento iterativo e vetorizado;
-   criar e manipular arrays NumPy;
-   carregar um arquivo CSV com pandas;
-   reconhecer um DataFrame;
-   investigar estrutura, tipos e conteúdo dos dados;
-   identificar problemas antes de iniciar a limpeza.

------------------------------------------------------------------------

# Arquivos utilizados

Utilize os arquivos fornecidos pelo professor:

``` text
operacoes.csv
equipamentos.csv
```

Nesta atividade, o arquivo principal será:

``` text
operacoes.csv
```

Não altere manualmente o arquivo CSV.

------------------------------------------------------------------------

# Parte 1 --- Preparação

Importe as bibliotecas:

``` python
import numpy as np
import pandas as pd
```

Apresente também as versões instaladas:

``` python
print(np.__version__)
print(pd.__version__)
```

------------------------------------------------------------------------

# Parte 2 --- Processamento tradicional

Considere:

``` python
horas = [8, 7, 10, 6, 9]
```

Crie uma nova lista contendo o dobro de cada valor.

Faça obrigatoriamente utilizando:

``` python
for
```

Estrutura inicial:

``` python
resultado = []

for valor in horas:
    # complete
```

------------------------------------------------------------------------

# Parte 2 --- Responda

Após executar:

``` python
resultado
```

responda:

1.  Quantas vezes o corpo do `for` foi executado?
2.  Quem controla explicitamente a repetição?
3.  O cálculo foi aplicado a um valor por vez ou ao conjunto inteiro?

------------------------------------------------------------------------

# Parte 3 --- Transformando em array

Transforme:

``` python
horas = [8, 7, 10, 6, 9]
```

em um array NumPy chamado:

``` python
horas_np
```

Depois apresente:

``` python
type(horas_np)
horas_np.ndim
horas_np.shape
horas_np.size
horas_np.dtype
```

------------------------------------------------------------------------

# Parte 3 --- Interprete

Explique com suas palavras:

-   o que significa `ndim`;
-   o que significa `shape`;
-   o que significa `size`;
-   o que significa `dtype`.

------------------------------------------------------------------------

# Parte 4 --- Vetorização

Agora calcule o dobro de todas as horas **sem utilizar `for`**.

Resultado esperado:

``` text
[16 14 20 12 18]
```

Utilize uma operação sobre o array inteiro.

------------------------------------------------------------------------

# Vetorização

Agora execute também:

``` python
horas_np + 1
horas_np * 2
horas_np / 2
horas_np ** 2
```

Observe que não escrevemos uma repetição explícita.

------------------------------------------------------------------------

# Parte 4 --- Novos vetores

Considere:

``` python
combustivel = np.array([
    95, 87, 150, 68, 115
])
```

Calcule:

``` text
consumo por hora
```

para todos os registros.

Fórmula:

``` text
                    combustível
consumo por hora = ─────────────
                       horas
```

Não utilize `for`.

------------------------------------------------------------------------

# Parte 4 --- Análise vetorizada

Utilizando apenas NumPy, descubra:

1.  total de horas;
2.  média de horas;
3.  maior quantidade de horas;
4.  menor quantidade de horas;
5.  consumo médio por hora.

Pesquise/utilize:

``` python
sum()
mean()
max()
min()
```

------------------------------------------------------------------------

# Parte 5 --- Máscara booleana

Queremos encontrar operações com mais de 8 horas.

Execute:

``` python
horas_np > 8
```

Observe o resultado.

------------------------------------------------------------------------

# Parte 5 --- Aplicando a máscara

Agora utilize a condição para recuperar somente os valores
correspondentes.

Resultado esperado:

``` text
[10  9]
```

Depois descubra:

> Quantas operações tiveram mais de 8 horas?

------------------------------------------------------------------------

# Parte 6 --- Reflexão sobre vetorização

Compare:

``` python
for valor in horas:
    ...
```

com:

``` python
horas_np * 2
```

Responda:

1.  Qual código expressa mais diretamente a operação matemática?
2.  Em qual solução a repetição fica explícita?
3.  O que significa dizer que uma operação foi **vetorizada**?

------------------------------------------------------------------------

# Parte 7 --- Carregamento dos dados

Agora começaremos a trabalhar com dados armazenados em arquivo.

Carregue:

``` text
operacoes.csv
```

utilizando pandas.

Estrutura:

``` python
df = pd.read_csv(
    "caminho/do/arquivo/operacoes.csv"
)
```

Ajuste o caminho de acordo com a localização do arquivo no Colab/Drive.

------------------------------------------------------------------------

# Parte 7 --- Primeira inspeção

Execute:

``` python
df
```

Depois:

``` python
type(df)
```

Responda:

> Qual estrutura do pandas foi criada por `read_csv()`?

------------------------------------------------------------------------

# Parte 8 --- Primeiras linhas

Execute:

``` python
df.head()
```

Depois:

``` python
df.head(10)
```

E:

``` python
df.tail()
```

Responda:

1.  O que `head()` apresenta?
2.  O que `tail()` apresenta?
3.  Por que esses comandos são úteis em bases grandes?

------------------------------------------------------------------------

# Parte 9 --- Dimensão da base

Execute:

``` python
df.shape
```

Registre o resultado:

``` text
Quantidade de linhas: ______

Quantidade de colunas: ______
```

Explique:

> O que uma linha representa neste conjunto de dados?

------------------------------------------------------------------------

# Parte 10 --- Conhecendo as colunas

Execute:

``` python
df.columns
```

Liste os nomes encontrados.

Depois escolha três colunas e explique o que você acredita que cada uma
representa.

------------------------------------------------------------------------

# Parte 11 --- Tipos dos dados

Execute:

``` python
df.dtypes
```

Monte uma pequena tabela:

  Coluna   Tipo identificado
  -------- -------------------
  ...      ...
  ...      ...

------------------------------------------------------------------------

# Parte 11 --- Questão importante

Observe especialmente:

``` text
horas_trabalhadas
```

Responda:

> O tipo identificado pelo pandas é o que você esperava?

Se não for, **não corrija ainda**.

Formule uma hipótese para explicar o resultado.

------------------------------------------------------------------------

# Parte 12 --- `info()`

Execute:

``` python
df.info()
```

Utilizando a saída, identifique:

-   quantidade de registros;
-   quantidade de colunas;
-   tipos encontrados;
-   colunas com valores ausentes.

------------------------------------------------------------------------

# Parte 13 --- Estatísticas descritivas

Execute:

``` python
df.describe()
```

Observe as colunas numéricas.

Identifique:

-   média;
-   mínimo;
-   máximo;
-   quantidade de valores.

------------------------------------------------------------------------

# Parte 13 --- Investigue

Responda:

1.  Existe algum mínimo que parece estranho?
2.  Existe algum máximo que merece atenção?
3.  Todos os dados aparecem em `describe()`?
4.  Por que algumas colunas não aparecem?

------------------------------------------------------------------------

# Parte 14 --- Incluindo dados não numéricos

Execute:

``` python
df.describe(
    include="all"
)
```

Compare com:

``` python
df.describe()
```

Responda:

> O que mudou?

------------------------------------------------------------------------

# Parte 15 --- Valores ausentes

Execute:

``` python
df.isna()
```

Depois:

``` python
df.isna().sum()
```

Registre as colunas que possuem valores ausentes.

------------------------------------------------------------------------

# Parte 15 --- Interprete

Para cada coluna com valores ausentes, responda:

> A ausência parece impedir imediatamente a análise?

Não substitua nem remova valores ainda.

Nesta etapa estamos apenas **explorando**.

------------------------------------------------------------------------

# Parte 16 --- Duplicidades

Execute:

``` python
df.duplicated()
```

Depois:

``` python
df.duplicated().sum()
```

Responda:

> Existem registros duplicados?

------------------------------------------------------------------------

# Parte 16 --- Visualizando duplicados

Caso existam, tente:

``` python
df[
    df.duplicated(
        keep=False
    )
]
```

Observe os registros.

Não utilize ainda:

``` python
drop_duplicates()
```

------------------------------------------------------------------------

# Parte 17 --- Valores únicos

Escolha a coluna:

``` python
equipamento
```

e execute:

``` python
df["equipamento"].unique()
```

Depois:

``` python
df["equipamento"].nunique()
```

------------------------------------------------------------------------

# Parte 17 --- Investigue

Observe cuidadosamente os valores.

Responda:

1.  Existem códigos aparentemente iguais escritos de formas diferentes?
2.  Espaços podem estar causando diferenças?
3.  Letras maiúsculas e minúsculas podem interferir?
4.  Quantos equipamentos parecem existir de fato?

------------------------------------------------------------------------

# Parte 18 --- Frequências

Execute:

``` python
df["equipamento"].value_counts()
```

Depois faça o mesmo para:

``` python
df["obra"].value_counts()
```

Responda:

> O que `value_counts()` ajuda a descobrir durante a exploração?

------------------------------------------------------------------------

# Parte 19 --- Selecionando uma Series

Execute:

``` python
df["equipamento"]
```

Depois:

``` python
type(
    df["equipamento"]
)
```

Responda:

> Por que o resultado não é um DataFrame?

------------------------------------------------------------------------

# Parte 20 --- Selecionando um DataFrame

Execute:

``` python
df[
    [
        "equipamento",
        "horas_trabalhadas",
        "combustivel_litros"
    ]
]
```

Verifique:

``` python
type(
    df[
        [
            "equipamento",
            "horas_trabalhadas",
            "combustivel_litros"
        ]
    ]
)
```

------------------------------------------------------------------------

# Parte 21 --- Exploração dirigida

Sem limpar ou modificar os dados, tente responder:

1.  Quantos registros existem?
2.  Quantas colunas existem?
3.  Quais colunas possuem valores ausentes?
4.  Existem duplicidades?
5.  Existem problemas aparentes nos códigos dos equipamentos?
6.  Existem valores de horas que parecem inválidos?
7.  Existem datas que parecem suspeitas?
8.  Qual coluna apresenta o problema de tipo mais evidente?

------------------------------------------------------------------------

# Parte 22 --- Relatório de qualidade

Crie uma célula Markdown no notebook com:

``` text
RELATÓRIO INICIAL DOS DADOS

Dimensão:
...

Valores ausentes:
...

Duplicidades:
...

Problemas de padronização:
...

Tipos inadequados:
...

Valores suspeitos:
...

Problemas que precisam ser investigados:
...
```

------------------------------------------------------------------------

# Desafio --- Exploração sem limpeza

Um erro comum é começar imediatamente a modificar os dados.

Nesta atividade você **não deverá** utilizar:

``` python
dropna()
fillna()
drop_duplicates()
replace()
astype()
pd.to_numeric()
```

O objetivo é:

> descobrir e documentar os problemas antes de decidir como tratá-los.

------------------------------------------------------------------------

# Desafio Final

## Produza um diagnóstico da base

Utilizando apenas operações de **carregamento e exploração**, produza um
diagnóstico contendo:

1.  dimensão da base;
2.  nomes das colunas;
3.  tipos;
4.  quantidade de ausentes por coluna;
5.  quantidade de duplicados;
6.  valores únicos de `equipamento`;
7.  frequência de registros por equipamento;
8.  estatísticas das colunas numéricas;
9.  pelo menos **quatro problemas ou situações que merecem
    investigação**.

------------------------------------------------------------------------

# Entrega

Entregue um notebook `.ipynb` contendo:

-   códigos executados;
-   resultados das células;
-   respostas em células Markdown;
-   diagnóstico final.

O notebook deve permitir acompanhar seu raciocínio.

------------------------------------------------------------------------

# Critérios de avaliação

| Critério | Valor |
|---|---:|
| Carregamento correto do CSV | 1,0 |
| Uso de `head`, `tail`, `shape`, `columns` e `dtypes` | 1,5 |
| Uso de `info`, `describe`, `isna` e `duplicated`  | 1,5 |
| Exploração de valores únicos e frequências | 1,0 |
| Diagnóstico e interpretação dos problemas | 1,0 |
| Organização do notebook   | 0,5 |
| **Total** | **10,0** |

# O que esta atividade está avaliando?

``` text
LISTA
  ↓
ARRAY NUMPY
  ↓
VETORIZAÇÃO
  ↓
CARREGAMENTO DO CSV
  ↓
DATAFRAME
  ↓
EXPLORAÇÃO
  ↓
DIAGNÓSTICO
```

------------------------------------------------------------------------

# Regra fundamental

Nesta etapa:

``` text
NÃO CORRIJA PRIMEIRO
        ↓
OBSERVE
        ↓
DESCREVA
        ↓
IDENTIFIQUE
        ↓
FORMULE HIPÓTESES
        ↓
DEPOIS DECIDA COMO LIMPAR
```

A próxima etapa será justamente:

``` text
DIAGNÓSTICO
     ↓
LIMPEZA
     ↓
TRANSFORMAÇÃO
```
