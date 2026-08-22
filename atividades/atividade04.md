---
author: Programação para Ciência e Engenharia de Dados
marp: true
paginate: true
theme: default
title: Atividade 04 --- Diagnóstico e Limpeza de Dados
---

# Atividade 04

## Diagnóstico e melhoria de um dataset sujo

Nesta atividade você receberá uma base propositalmente problemática:

``` text
operacoes_equipamentos_sujo.csv
```

Sua missão será:

``` text
CARREGAR
   ↓
EXPLORAR
   ↓
DIAGNOSTICAR
   ↓
PLANEJAR
   ↓
LIMPAR
   ↓
VALIDAR
   ↓
COMPARAR
```

------------------------------------------------------------------------

# Objetivo

Ao final, você deverá ser capaz de:

-   reconhecer diferentes problemas de qualidade;
-   diferenciar diagnóstico de correção;
-   justificar decisões de limpeza;
-   utilizar pandas para corrigir problemas;
-   comparar a base antes e depois;
-   avaliar se a limpeza realmente melhorou os dados.

------------------------------------------------------------------------

# Regra principal

Não comece alterando os dados.

Primeiro:

``` text
OBSERVE
   ↓
IDENTIFIQUE
   ↓
DOCUMENTE
   ↓
DECIDA
   ↓
CORRIJA
```

Uma alteração sem justificativa pode introduzir um novo erro.

------------------------------------------------------------------------

# Parte 1 --- Carregamento

Carregue:

``` python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "operacoes_equipamentos_sujo.csv"
)

df.head()
```

Preserve uma cópia original:

``` python
df_original = df.copy()
```

------------------------------------------------------------------------

# Parte 2 --- Conhecendo a base

Execute:

``` python
df.shape
df.columns
df.dtypes
df.info()
```

Registre:

-   quantidade de linhas;
-   quantidade de colunas;
-   tipos identificados;
-   significado provável de cada coluna.

------------------------------------------------------------------------

# Parte 3 --- Inspeção visual

Observe:

``` python
df.head(15)
df.tail(15)
```

Depois visualize amostras aleatórias:

``` python
df.sample(10)
```

Liste os primeiros problemas que chamaram sua atenção.

Ainda não faça correções.

------------------------------------------------------------------------

# Parte 4 --- Valores ausentes

Execute:

``` python
df.isna().sum()
```

Responda:

1.  Quais colunas possuem valores ausentes?
2.  Quantos valores estão ausentes?
3.  Todo valor ausente deve ser removido?
4.  Que decisão você tomaria para cada coluna?

------------------------------------------------------------------------

# Parte 5 --- Duplicidades

Execute:

``` python
df.duplicated().sum()
```

Depois:

``` python
df[
    df.duplicated(
        keep=False
    )
]
```

Investigue também:

``` python
df["id_operacao"].duplicated().sum()
```

------------------------------------------------------------------------

# Duplicado significa erro?

Discuta:

> Duas linhas semelhantes são necessariamente duplicadas?

Considere:

``` text
mesmo equipamento
mesma data
mesmas horas
mesmo combustível
```

Isso pode representar:

-   duplicação indevida;
-   duas operações legítimas;
-   erro de identificação.

A decisão depende da **granularidade** e da chave do registro.

------------------------------------------------------------------------

# Parte 6 --- Padronização textual

Explore:

``` python
df["equipamento"].unique()
df["tipo"].unique()
df["operador"].unique()
df["obra"].unique()
df["status"].unique()
```

Depois:

``` python
df["equipamento"].value_counts(
    dropna=False
)
```

Faça o mesmo para outras colunas categóricas.

------------------------------------------------------------------------

# Parte 6 --- Diagnóstico

Procure problemas como:

``` text
ESC-01
esc-01
 ESC-01
ESC 03

Ativo
ativo
ATIVO
```

Responda:

> Quantas categorias parecem existir de fato e quantas o computador
> identifica?

------------------------------------------------------------------------

# Parte 7 --- Tipos inadequados

Observe:

``` python
df.dtypes
```

Pergunte:

> Quais colunas deveriam ser numéricas?

Tente investigar:

``` python
pd.to_numeric(
    df["horas_trabalhadas"],
    errors="coerce"
)
```

Não substitua a coluna ainda.

Compare o resultado com a coluna original.

------------------------------------------------------------------------

# Parte 8 --- Encontrando valores que não convertem

Uma estratégia:

``` python
horas_convertidas = pd.to_numeric(
    df["horas_trabalhadas"],
    errors="coerce"
)

problemas_horas = (
    horas_convertidas.isna()
    &
    df["horas_trabalhadas"].notna()
)

df.loc[
    problemas_horas,
    ["id_operacao", "horas_trabalhadas"]
]
```

Repita a ideia para outras colunas numéricas.

------------------------------------------------------------------------

# Parte 9 --- Datas

Tente converter:

``` python
datas_convertidas = pd.to_datetime(
    df["data"],
    format="%d/%m/%Y",
    errors="coerce"
)
```

Investigue:

``` python
datas_convertidas.isna().sum()
```

Depois descubra quais valores provocaram problemas.

------------------------------------------------------------------------

# Parte 10 --- Valores numericamente suspeitos

Depois de produzir versões numéricas temporárias, investigue:

``` python
horas_convertidas.describe()
```

Pergunte:

-   horas negativas fazem sentido?
-   zero hora é possível?
-   28 horas em uma operação diária é possível?
-   combustível negativo faz sentido?
-   valores extremamente altos podem ser legítimos?

------------------------------------------------------------------------

# Outlier não significa erro

Um valor muito diferente pode ser:

``` text
ERRO
```

ou:

``` text
EVENTO REAL E RARO
```

Portanto:

> Não apague um outlier apenas porque ele é grande.

Primeiro avalie sua plausibilidade no domínio.

------------------------------------------------------------------------

# Parte 11 --- Produza o diagnóstico

Antes de limpar, crie uma tabela:

  -----------------------------------------------------------------------------------
  Problema       Coluna        Exemplo         Quantidade Ação        Justificativa
                                                          proposta    
  -------------- ------------- ----------- -------------- ----------- ---------------
  Padronização   equipamento   `esc-01`               ... ...         ...

  Ausência       horas         `NaN`                  ... ...         ...

  Tipo           horas         `"oito"`               ... ...         ...
  -----------------------------------------------------------------------------------

Inclua pelo menos **8 problemas** encontrados.

------------------------------------------------------------------------

# Parte 12 --- Planejamento da limpeza

Para cada problema, escolha conscientemente entre:

``` text
CORRIGIR
PADRONIZAR
CONVERTER
MARCAR COMO AUSENTE
REMOVER
MANTER
INVESTIGAR
```

Não existe uma única ação correta para todos os problemas.

------------------------------------------------------------------------

# Parte 13 --- Começando a limpeza

Trabalhe sobre uma cópia:

``` python
df_limpo = df_original.copy()
```

Não altere:

``` python
df_original
```

Isso permitirá comparar o antes e o depois.

------------------------------------------------------------------------

# Parte 14 --- Padronização textual

Exemplo:

``` python
df_limpo["equipamento"] = (
    df_limpo["equipamento"]
      .str.strip()
      .str.upper()
)
```

Faça tratamentos coerentes também para:

``` text
tipo
operador
obra
status
```

Cuidado:

> Padronizar não significa necessariamente colocar tudo em maiúsculas.

Escolha uma convenção e justifique.

------------------------------------------------------------------------

# Parte 15 --- Conversão numérica

Converta as colunas que deveriam ser numéricas.

Exemplo:

``` python
df_limpo["horas_trabalhadas"] = pd.to_numeric(
    df_limpo["horas_trabalhadas"],
    errors="coerce"
)
```

Repita quando necessário.

------------------------------------------------------------------------

# Parte 16 --- Conversão de datas

Converta:

``` python
df_limpo["data"] = pd.to_datetime(
    df_limpo["data"],
    format="%d/%m/%Y",
    errors="coerce"
)
```

Depois verifique:

``` python
df_limpo["data"].isna().sum()
```

------------------------------------------------------------------------

# Parte 17 --- Valores inválidos

Crie regras de domínio justificadas.

Por exemplo:

``` python
df_limpo.loc[
    df_limpo["horas_trabalhadas"] < 0,
    "horas_trabalhadas"
] = np.nan
```

Mas antes de aplicar outras regras, explique:

> Por que esse valor pode ser considerado inválido?

------------------------------------------------------------------------

# Parte 18 --- Duplicidades

Se concluir que existem duplicações reais, trate-as.

Exemplo:

``` python
df_limpo = df_limpo.drop_duplicates()
```

Depois:

``` python
df_limpo.duplicated().sum()
```

Não utilize `drop_duplicates()` sem explicar qual evidência sustenta a
decisão.

------------------------------------------------------------------------

# Parte 19 --- Valores ausentes

Depois das conversões e correções, execute novamente:

``` python
df_limpo.isna().sum()
```

Observe:

> A quantidade de ausentes pode ter aumentado.

Por quê?

Porque valores inválidos podem ter sido convertidos para `NaN`.

------------------------------------------------------------------------

# Parte 20 --- Antes × Depois

Compare:

``` python
print(
    "Original:",
    df_original.shape
)

print(
    "Limpo:",
    df_limpo.shape
)
```

Compare também:

``` python
df_original.dtypes
df_limpo.dtypes
```

------------------------------------------------------------------------

# Parte 21 --- Compare categorias

Antes:

``` python
df_original[
    "equipamento"
].value_counts(
    dropna=False
)
```

Depois:

``` python
df_limpo[
    "equipamento"
].value_counts(
    dropna=False
)
```

Faça o mesmo para outras categorias relevantes.

------------------------------------------------------------------------

# Parte 22 --- Compare a qualidade

Monte uma tabela final:

  Indicador                       Antes   Depois
  ----------------------------- ------- --------
  Registros                         ...      ...
  Duplicados                        ...      ...
  Ausentes                          ...      ...
  Equipamentos distintos            ...      ...
  Datas inválidas                   ...      ...
  Valores numéricos inválidos       ...      ...

------------------------------------------------------------------------

# Parte 23 --- O dataset melhorou?

Não responda apenas:

> Sim.

Explique **em que sentido** houve melhoria.

Considere:

-   consistência;
-   completude;
-   validade;
-   unicidade;
-   tipos adequados;
-   facilidade de análise.

------------------------------------------------------------------------

# Parte 24 --- Houve perda de informação?

Toda limpeza possui consequências.

Responda:

1.  Alguma linha foi removida?
2.  Algum valor original foi substituído?
3.  Algum valor virou `NaN`?
4.  Alguma decisão envolveu incerteza?
5.  Seria necessário consultar a fonte dos dados?

------------------------------------------------------------------------

# Parte 25 --- Salve o resultado

Exporte:

``` python
df_limpo.to_csv(
    "operacoes_equipamentos_limpo.csv",
    index=False
)
```

Você deverá entregar:

``` text
operacoes_equipamentos_limpo.csv
```

junto com o notebook.

------------------------------------------------------------------------

# Desafio Final

## Auditoria da limpeza

Imagine que outra pessoa realizou a limpeza e afirmou:

> "Agora os dados estão corretos."

Sua tarefa é demonstrar isso com evidências.

Produza pelo menos **6 verificações automáticas**.

------------------------------------------------------------------------

# Exemplos de verificações

``` python
df_limpo.duplicated().sum()
```

``` python
df_limpo[
    "equipamento"
].unique()
```

``` python
df_limpo[
    "horas_trabalhadas"
].dtype
```

``` python
df_limpo.isna().sum()
```

Crie outras verificações de acordo com suas decisões.

------------------------------------------------------------------------

# Relatório final

Em uma célula Markdown, escreva:

``` text
1. Principais problemas encontrados

2. Decisões de limpeza realizadas

3. Problemas corrigidos

4. Problemas que permaneceram

5. Informações que exigiriam consulta à fonte

6. Evidências de melhoria da qualidade

7. Limitações da limpeza realizada
```

------------------------------------------------------------------------

# Critérios de avaliação

| Critério | Valor |
|---|---:|
| Exploração sistemática | 1,0 |
| Identificação dos problemas | 1,5 |
| Diagnóstico e justificativas   | 1,5 |
|Padronização e conversão | 1,5 |
| Tratamento de inválidos, ausentes e duplicados | 1,5 |
| Comparação antes × depois  | 1,5 |
| Validação automática da limpeza | 1,0 | 
| Organização do notebook   | 0,5 |
| **Total** | **10,0** |

------------------------------------------------------------------------

# O aprendizado central

Limpeza de dados não é:

``` text
APAGAR TUDO QUE PARECE ESTRANHO
```

É:

``` text
DADO BRUTO
    ↓
DIAGNÓSTICO
    ↓
REGRA JUSTIFICADA
    ↓
TRATAMENTO
    ↓
VALIDAÇÃO
    ↓
DADO MAIS CONFIÁVEL
```

------------------------------------------------------------------------

# Próximo passo

Depois de preparar os dados:

``` text
DADOS LIMPOS
    ↓
TRANSFORMAÇÃO
    ↓
NOVAS VARIÁVEIS
    ↓
AGREGAÇÃO
    ↓
ANÁLISE
    ↓
INTERPRETAÇÃO
```

A limpeza não é o objetivo final.

Ela prepara os dados para que as análises posteriores sejam mais
confiáveis.
